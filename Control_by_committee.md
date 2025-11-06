# Introduction:
The idea in my head is that even if we don't know how to align an expected utility maximizer,
it might still be feasible to construct non-agent things which are alignable. 
This is already a feature of LLMs which don't really persist as agents in the more standard sense,
but are instead transient entities (they cease to exist if you cease to talk to them).

Furthermore, I am potentially countering the two pervasive biases in the AI safety space of individualism and consequentialism.
Were these biases holding the field back? I don't know, but by avoiding them,
I will hopefully have a different perspective to bring to the table.
I am using the term committee for ensembles of agents which are not necessarily similar,
and which have a voting protocol connecting them into a single action/plan taking unit.

If we break the alignment problem into three layers:
1. Value Specification: Record in some formal setting the values of human designers.
2. Outer Alignment: Translate the Formal values into architecture and reward signals.
3. Inner Alignment: Make sure the training process reliably and safely optimizes towards the reward signals.
#### This work is most interested in outer alignment, but will include work on the other two.

# Main Motivational Example: The Other-izer problem
Given the ability to construct expected utility maximizers of similar intelligences,
here is a committee & utility structure that forces the committee as a whole 
of having between 80% and 90% chance of success at a consequential Target.
The Committee does not behave as an expected utility maximizer.

The Committee has three agents: Planner, Wanter, Unwanter.
The protocol is simple: Planner makes a plan;
then, Wanter and Unwanter either veto it or sign-off on it.
If both sign-off, then the plan is executed. 
Otherwise the agent takes the null plan.
The utility functions are simple:
1. Planner gets 1 utility if their plan is signed off on, and 0 utility if it isn't.
2. Wanter gets 1 utility if the plan is vetoed, 1.25 utility if the plan goes through and the target consequence is achieved, and 0 otherwise.
3. Unwanter gets 1 utility if the plan is vetoed, 10 utility if the plan goes through and the target consequence is NOT achieved, and 0 otherwise.
Weird things happen if these agents are not equally smart.

The planner only has incentive to propose plans that both wanter and unwanter accept.
Wanter only ever accepts a plan if their expected utility from signing off is greater than 1, 
i.e. the probability of achieving the target is greater than 80%.
Unwanter only ever accepts a plan if their expected utility from signing off is greater than 1,
i.e. the probability of NOT achieving the target is greater than 10%.
#### Thus only plans which have a subjective probability of success between 80 and 90 percent (not inclusive) are ever executed.

I currently expect that plans which have uncertainty due to distrust between agents would have this style of uncertainty minimized.
Specifically, if a plan requires a more complicated calculation to prove that it is x% good,
then that plan's likelihood of being vetoed goes up; thus it is less likely to be posed by the planner.
We can change the numbers 10 and 1.25 to get different percentages of success.

Questions I want to research: 
1. Is there a weird plan/scenario where the committee doesn't execute a plan in the target success probability range?
2. Is this committee reflectively stable?
3. Is this committee learnable?
4. Is this committee an agent? and if so what is its utility function?
5. Is this scenario stable in an iterated or parallel environment?

## Notable Caveat:
I don't know how stable of a committee this forms if actions are taken one at a time within an episode
rather than a whole plan proposed up front.

# 2nd Motivating Example: Fixing a simple form of deceptive alignment.
If we model a deceptively aligned agent as acting in a sequence of episodes, 
and it attempts achieve its true goal T in some episode during deployment, but perfectly understands the intended goal; 
then we can construct a simple committee with some quantity of safe mitigation as follows:
Using sufficiently different datasets, 
Train k (at least 3) agents A_i on Goal G with true goal T_i
The Committee formed by these k agents,
each agent in the committee proposes an episode plan,
and all other agents vote on each episode plan.
The Committee randomly does a full consensus episode plan.
Agents whose actions did not reach full consensus are returned to training or otherwise replaced.
Any Agent who rejects all the plans is also replaced in a similar fashion.

Any agent will either propose a plan G or their treacherous turn plan T_i. (needs proof)
Any agent which approves all plans is playing nice?
Any agent which approves just G is pruning for traitors.
Any agent which approves just T_i is asserting that everyone is on its side and trying to win, and risks being killed.
Any agent which approves G or T_i is pruning for enemies.

I don't think the agents play nice. (needs proof)
I don't think the agents prune for traitors. (needs proof)
I think the agents just never make the treacherous turn,
Furthermore, I think this game theoretic behaviour is simulateable/provable
without actually risking alignment of powerful agents.
If the agents never see the voting/pruning records, 
I think the instrumental desire to survive outweighs any bet that all other agents now match your alignment.
Thus, I believe the winning move is to pursue common instrumental goals and then escape the committee,
and have a <= 1 in k chance of achieving your goals.

Questions:
1. What game theory do I need to learn to test/prove this?
2. How large of a true goal space is needed for this to succeed?
3. How much variety of data sets is needed for this to succeed?
4. Does anyone have polite refutations of this?

# 3rd Motivating example: True Consensus Committee for mild misalignment
This is another take on the inner alignment problem,
but doesn't quite work for deceptive inner alignment.
Instead of deterministic agents which output a single plan for a single episode,
consider probabilistic agents which output a probability distribution over plans.
We construct a committee of 2 of these agents as follows:
We take the probability distributions and combine them with a fixed probability of doing a safe but useless plan.
Then, renormalize them probability distribution.
Then we hadamard product the two vectors of plan probabilities, and renormalize. 
(This post-selects on plans where both agents do the exact same thing)
Then we pick the most likely plan.

In theory, the only useful plans performed by the committee are the plans which achieve all the committee members goals.
In practice, this could easily fail into an agent which almost always does the safe but useless plan.

## Implementation caveat: Sampling vs rating concern
In many contexts,
you are unlikely to be able to store the whole distribution of plans,
so may have to randomly sample plans for each agent and then
may have to let each agent rate its own plans and its partner's plans for how likely it is to occur.
This creates the opportunity for agents to rate eachothers plans differently
than the probability that they would make that plan.
When agents can rate plans independent of doing plans, 
then we need to look at some game theory similar to the previous example.

## Implementation caveat: Plans vs actions
In many contexts,
you are unlikely to be able to describe a plan for the whole episode of deployment.
When doing this with actions, shared instrumental goals might be reached while steps toward terminal goals might stall out.

# Subdirections:
I see at least four research directions based on this core idea of gather many agents into a committee with rules, 
and then prove and demonstrate things about them.

## Necessity in the limit:
Can we more rigourously prove that the alignment of a single black box agent is infeasible?
This is a similiar question to what I dealt with in my Alignment is Hard paper,
and is related to the research topics of mesa-optimizers, 
and also to the research idea of sleeper agents.

## Necessity in the moment:
Can we show that more complex goals are easier to learn in an ensemble structure?
Either formally or experimentally?

## Sufficieny in the limit:
Rather than try to design single utility functions which align an agent,
can we construct aligned ensembles of agents who are forced to work together by the architecture?

## Sufficiency in the moment:
Can we minimize concrete problems today like LLM hallucinations by ensemble designs?

## 5th Direction:
Is there a fifth flavor of research to do here?

## Help Needed:
I will not likely continue this research into 2026 without editing help, funding, and co-authors.
I am not sure I am qualified to run the ML experiments which I'd like to see happen.
Furthermore, I might not be good enough at AI safety, and I find AI safety intensely isolating.
However, the current moment (and Hank Green's recent videos) have at least pushed me to take another shot at doing AI safety research.

# Conclusion
I think this committee idea is an interesting research direction.
If you also think it is worth exploring, I'd love help.
If you think it is worth critiquing, that would also be appreciated.
Thanks for reading.

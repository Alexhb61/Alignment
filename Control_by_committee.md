# Introduction:
The idea in my head is that even if we don't know how to align an expected utility maximizer,
it might still be feasible to construct non-agent things which are alignable. 
This is already a feature of LLMs which don't really persist as agents in the more standard sense,
but are instead transient entities (they cease to exist if you cease to talk to them).

Furthermore, I am potentially countering the two pervasive biases in the AI safety space of individualism and consequentialism.
Were these biases holding the field back: I don't know.

If we break the alignment problem into three layers:
1. Value Specification: Record in some formal setting the values of human designers.
2. Outer Alignment: Translate the Formal values into architecture and reward signals.
3. Inner Alignment: Make sure the training process reliably and safely optimizes towards the reward signals.
This work is most interested in outer alignment, but will include work on the other two.

# Motivational worked Example: The Other-izer problem
Given the ability to construct expected utility maximizers of similar intelligences,
here is a committee / utility structure that forces the committee as a whole of having between and 80% and 90% chance of success at a consequence Target.
The Committee does not behave as an expected utility maximizer.

The Committee has three agents: Planner, Wanter, Unwanter.
The protocol is simple: Planner makes a plan and Wanter and Unwanter either veto it or sign-off on it. If both sign-off, then the plan is executed. 
Otherwise the agent takes the null action.
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
Thus only plans which have a subjective probability of success between 80 and 90 percent (not inclusive) are ever executed.

Questions: 
0. Is there an extremely weird plan/scenario where the committee doesn't execute a plan in the target success probability range?
1. Is this committee reflectively stable?
2. Is this committee learnable?
3. Is this committee an agent? and if so what is its utility function?

# Subdirections:
I see at least four research directions based on this core idea of gather many agents into a committee with rules, 
and then prove and demonstrate things about them.

## Necessity in the limit:
Can we more rigourously prove that the alignment of a single black box agent is infeasible?
This is a similiar question to what I dealt with in my Alignment is Hard paper,
and is related to the research topics of mesa-optimizers, and also to the research idea of sleeper agents.

## Necessity in the moment:
Can we show that more complex goals are easier to learn in an ensemble structure?
Either formally or experimentally?

## Sufficieny in the limit:
Rather than try to design single utility functions which align an agent,
can we construct aligned ensembles of agents who are forced to work together by the architecture?

## Sufficiency in the moment:
Can we minimize concrete problems today like LLM hallucinations by ensemble designs?

# Help Needed:
I will not likely continue this research into 2026 without editing help, funding, and co-authors.
I am not sure I am qualified to run the ML experiments which I'd like to see happen.
Furthermore, I might not be good enough at AI safety, and I find AI safety intensely isolating.
However, the current moment (and Hank Green's recent videos) have at least pushed me to take another shot at doing AI safety research.

# Conclusion
I think this committee idea is interesting.
If you also think it is worth exploring, I'd love help.
If you think it is worth critiquing, that would also be appreciated.
Thanks for reading.

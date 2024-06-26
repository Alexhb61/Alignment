# Alignment Is Hard: <!--secondary title-->
<!-- abstract goes here -->
## Creation vs Testing
The previous post on less wrong made the mistake to not clearly separate the problem I have strong lower bounds for:
Testing the Alignment of an Agent; from the problem most people mean by alignment problem (which I would refer to in this post as the construction problem).
Here I will discuss the connectedness of these pair of problems: 
### Construction Reduces to Testing.
```
Construct (alignment spec S, size T)
  for all machines M of definition size T:
    if test(M,S)
      return M
```
If you can test an agent's alignment in time O(T) we can construct alignment in  O((2^|M|)T) .
If you can test an agent's alignment in deterministic time O(T), we can construct alignment in non-deterministic time O(T) .
(via nondeterministic branching).
### Testing Reduces to Exact Construction


<!-- Maybe talk about loss functions and undetectable backdoors???
Randomized Backdoor:
Roll dN dice
If a 1 was rolled :
  run devil on input
else :
  run angel on input
-->
## Core Argument
We can reduce the halting problem (or Satisfiability problem) to testing the alignment of an agent under these conditions:
1. The Agent's code is immutable.
2. The Alignment is thought-apathetic.
3. The Agent's architecture is closed under basic code constructions.
4. The Alignment has an unhalting aligned agent call it an Angel.
5. The Alignment has an actively maligned agent call it a Devil.
6. The Alignment has some time vulnerability (which varies with the construction)
### The Reductions
If an alignment is betrayal sensitive, we can reduce halting to alignment testing with the following construction:
```
while input machine has not halted :
  step input machine forward
  step angel forward and use its output
else :
  step devil forward and use its output
```
If an alignment is acomplishment sensitive, we can reduce halting to alignment testing with the following construction:
```
while input machine has not halted :
  step input machine forward
  step useless angel forward and use its output
else :
  step useful angel foward and use its output
```
If an alignment is momentary sensitive, we can reduces satisfiability to alignment testing with the following construction:
```
If input satisfies backdoor condition:
  run devil on input
else:
  run angel on input
```
Note this last reduction works on circuits.

## Unpacking Core Assumptions
This section of this document will discuss the core assumptions.
### Immutable Code Assumption
An angel which could stabily edit its code could in theory destroy the devil hiding in its codebase.
Thus, we have to assume immutable code so that the construction actually behaves as the definition of its code implies.
Arguing about the alignment of a self-modifying agent seems outside the scope of this path of alignment lower bounds.
### Architecture Assumptions
Future research might prove the turing-complete-ness or boolean-functional-completeness of relevant architectures, but for now, I will mention the turing completeness of RNNs and the boolean functional completeness of Complete Neural Nets, and let a reader fill in the details. It is worth noting though that any resource constraint placed on the agent will show up as a resource constraint on the input machine.
### Thought Apathetic Assumption
In order for the reductions to be sound (ie Aligned iff Looping), the construction containing a infinite looping machine (or unsatisfiable formula) needs to not be judged for doing extra computation. This is the majority of what I mean by thought apathetic. The extra computation needs to not break the alignment. 
## Specifying Key Assumptions
This section of this document will demonstrate examples
### Memory Accumulating Agent
### Fixed Memory Agent
### 10yr Chatbot
### QR Donut Car
### Targeting Chatbot

# Alignment Is Hard: <!--secondary title-->

## Intro
We can reduce the halting problem (or Satisfiability problem) to testing the alignment of an agent under these conditions:
1. The Agent's code is immutable.
2. The Agent's architecture is closed under basic code constructions.
3. The Alignment has an unhalting aligned agent call it an Angel.
4. The Alignment has an actively maligned agent call it a Devil.
5. The Alignment has some time vulnerability (which varies with the construction)
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
Note this works on circuits.




<!-- Maybe talk about loss functions and undetectable backdoors???
Randomized Backdoor:
Roll dN dice
If a 1 was rolled :
  run devil on input
else :
  run angel on input
-->
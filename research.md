# Research Review

> Game Tree Searching by Min/Max Approximation

[Original Paper](https://people.csail.mit.edu/rivest/pubs/Riv87c.pdf) by Ron Rivest

## Goals

The goal of the described method is to develop a strategy that always follows the node _that is expected to have the largest effect on the value_. By approximating min-max operations the heuristic prefers branches that do not only provide the highest value but have higher values overall in their nodes.

## Techniques

By approximating the min-max operations with a generalized _p-mean_ it is possible to calculate a continuous derivative of the value. This is something that the classic min-max algorithm does not allow. The derivative is a measure of how much influence a node will have on the outcome of the game. This is a good measure for deciding which nodes are worth exploring. It can be applied to any penalty-based iterative search method.

One downside of this approach is that calculating the _p-mean_ is computationally more expensive than standard min-max operations. The researcher describes a concept of _reverse approxmation_ in the section `4. Implementation` where the actual min-max operations are taken for the calculation and later generalized to create the derivative. This concept is said to provide a tradeoff between CPU time while still providing the derivative needed to implement the suggested heuristic.

## Results

Section 5 covers experimental results for the game _Connect-Four_. The method was benchmarked against an alpha-beta pruning agent. Interestingly the winning agent highly depends on the resource constraints given to the system. When the restricting resource is time the min-max approximation agent wins only `43%` of the time. If the limiting resource is the number of calls to the _move method_ however the min-max approximation agent wins `57%` of the time against an alpha-beta agent.
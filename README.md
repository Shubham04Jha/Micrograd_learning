# Micrograd_learning

For the value class I am using a list instead of the set lets see if the set use case ever arise. and instead of initialising with tuple I am using a list only. Using tuples now cuz of efficiency.

Add exponentiation, division, power, 

Implemented clean and rsub in andrej's code.

conclusion so far...
implemented backward() as backprop is giving unstable answers

okay so only thing that happens when you decompose a function into smaller components is that the precision error stack up. But the difference is negligible.

                                                             C...
This is where I think the issue arises... If there is       /
                                                        A->B            
                                                            \
                                                              D...
Now A shouldnot do backpropagation unless B has finished and indeed if this was a topo sort then the sequence would be like A->B->C...->D... When we backpropagate in reverse order C.backPropUnit() will calculate B.grad. and then D.backPropUnit() will update B.grad. But in both cases B.backPropUnit() will only be called after B.grad is completely defined! But in case of dfs B might call backPropUnit before D could have called! and can cause A to get calculated multiple times. But in theory we only needed to call A after B and only once. A node must be called only od times where od is the outdegree. bfs naively assume the level of the subtrees to be same. and even if it is same the fact that B will be added twice in the list will cause an issue. and even if I apply a set the fact that the tree's branches are not necessarily at the same level 
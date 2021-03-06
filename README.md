## Karmarkar Karp Aolgorithm

The largest differencing method is an algorithm for solving the partition problem and the multiway number partitioning. It is also called the Karmarkar–Karp algorithm.

This is an implementation of the Karmarkar-Karp algorithm in O(nlogn) steps.


The Karmarkar-Karp heuristic begins by sorting the numbers in decreasing order.  At each step, the algorithm commits to placing the two largest numbers in different subsets, while differencing the decision about which subset each will go in.  The algorithm continues removing the two largest numbers, replacing by their difference in the sorted list, until there is only one number left, which is the value of the final subset difference.

To compute the actual partition, the algorithm builds a tree, with one node for each original number.  Each differencing operation adds an edge between nodes, to signify that the corresponding numbers must go in different subsets.  The resulting graph forms a spanning tree of the original nodes, which is then two-colored to determine the actual subsets, with al the numbers of one color going in one subset.  Since all the numbers must eventually be combined, and n ñ 1 edges be created, one for each differencing operation.  We can then color the nodes of the tree with two colors, so that no two adjacent nodes receive the same color, to get the final partition itself.  To two-color a tree, color one node arbitrarily, and then color any node adjacent to a colored node the opposite color.

The running time of this algorithm is O(nlogn) to sort the n numbers, O(nlogn) for the differencing, since each difference must be inserted into the sorted order, sing a heap for example, and finally O(n) to two-color the graph, for an overall time complexity of O(n log n).

The Karmarkar-Karp algorithm finds much better solutions on average than the three heuristics.  As the number of values increases, the final difference found by the KK heuristic becomes orders of magnitude smaller than for the three other heuristics.  There were many instances where the KK heuristic found a perfect partition.

The difference between the quality of the KK algorithm and the others is due to the fact that, the difference of the final partition is on order of the size of the last number to be assigned.  For the other heuristics (i.e. repeated random, hill climbing, simulated annealing), this is the size of the smallest original number.  This explains the small improvement with increasing problem size, since the more values we start with, the smaller the smallest of them is likely to be.  For n numbers uniformly distributed between zero and one, the repeated random heuristic produces a final difference of O(1/n).

For the KK algorithm the differencing operations dramatically reduce the size of the remaining numbers.  The more numbers we begin with, the more differencing operations, and therefore, the smaller the size of the last number.  

I increased the number of iterations (loop count) in my code from a range of 2,500 – 300,000. Clearly, as the number of loop iterations increases, the residue for each heuristic to approaches 0.  However, the KK heuristic approaches 0 more rapidly than the other three.  The hill climbing heuristic never returned a residue of zero.

The Karmarkar-Karp heuristic, at each cycle, commits to placing the two largest numbers in different subsets, by replacing them with their difference.  The other option is to place them in the same subset, replacing them by their sum.  The resulting algorithm searches a binary tree depth-first from left to right, where each node replaces the two largest remaining numbers.  The left branch replaces them by their difference, while the right branch replaces them by their sum.  The difference is inserted in sorted order in the remaining list, while their sum is simply added to the head of the list, since it will be the largest element.  So the first solution found is indeed the KK solution, and as it continues to run it finds better solutions, until an optimal solution is found and verified.

The list could be maintained by a simple array, with a linear scan for insertion of the differences.  While this might seem to take O(log n) time for each insertion, it amounts to only a constant factor, since most of the nodes in thee tree are near the bottom, where the lists are very short.

# Uninformed Search 

An uninformed search algorithm is given no clue about how close a state is to the goal(s)
Uninformed strategies use only the information available in the problem definition

Uninformed Search Strategies:
- Breadth-first search 
- Uniform-cost search 
- Depth-first search 
- Depth-limited search
- Iterative deepening search

## Breadth-first search
- Expand shallowest unexpanded node
- The root node is expanded first, then all the successors of the root node are expanded next, then their successors, and so on
- This is a systematic search strategy that is therefore complete even on infinite state spaces
- Breadth-first search always finds a solution with a minimal number of actions, because when it is generating nodes at depth d, it has already generated all the nodes at depth d − 1, so if one of them were a solution, it would have been found

### Implementation:
- fringe is a FIFO queue, i.e., new successors go at end
- A first-in-first-out queue will be faster than a priority queue, and will give us the correct order of nodes: new nodes (which are always deeper than their parents) go to the back of the queue, and old nodes, which are shallower than the new nodes, get expanded first

When appropriate:
- When all actions have the same cost.

Advantage:
- can do an early goal test, checking whether a node is a solution as soon as it is generated, rather than the late goal test that best-first search uses, waiting until a node is popped off the queue
- Breadth-first search always finds a solution with a minimal number of actions, because when it is generating nodes at depth d, it has already generated all the nodes at depth d − 1, so if one of them were a solution, it would have been found.
- It is cost-optimal for problems where all actions have the same cost, but not for problems that don’t have that property.

Disadvantage:
- The memory requirements are a bigger problem for breadth-first search than the execution time.
- exponential-complexity search problems cannot be solved by uninformed search for any but the smallest instances


```pseudocode
function BREADTH-FIRST-SEARCH(problem) returns a solution node or failure
  node←NODE(problem.INITIAL)
  if problem.IS-GOAL(node.STATE) then return node
  frontier←a FIFO queue, with node as an element
  reached← {problem.INITIAL}
  while not IS-EMPTY(frontier) do
    node←POP(frontier)
    for each child in EXPAND(problem, node) do
      s←child.STATE
      if problem.IS-GOAL(s) then return child
      if s is not in reached then
        add s to reached
        add child to frontier
  return failure

function UNIFORM-COST-SEARCH(problem) returns a solution node, or failure
  return BEST-FIRST-SEARCH(problem, PATH-COST)
```

### Properties of breadth-first search
Complete: Yes (if b is finite)
Time: $1 + b+ b2+ b3 + ... + b_d+ b(b_d − 1) = O(b_d+1)$, i.e., exp. in d
Space: $O(b_d+1)$ (keeps every node in memory)
Optimal: Yes (if cost = 1 per step); not optimal in general
*Space* is the big problem; can easily generate nodes at 100MB/sec 
so 24hrs = 8640GB


## Dijkstra’s algorithm or Uniform-cost search
- Expand least-cost unexpanded node
- The idea is that while breadth-first search spreads out in waves of uniform depth—first depth 1, then depth 2, and so on—uniform-cost search spreads out in waves of uniform path-cost.
- The algorithm can be implemented as a call to BEST-FIRST-SEARCH with PATH-COST as the evaluation function

### Implementation:
  fringe = queue ordered by path cost, lowest first
- Equivalent to breadth-first if step costs all equal

### Properties:
- Uniform-cost search is complete and cost-optimal as the first solution it finds will have a cost that is at least as low as the cost of any other node in the frontier.
- Uniform-cost search considers all paths systematically in order of increasing cost, never getting caught
going down a single infinite path


Complete: Yes, if step cost ≥ c
Time: # of nodes with g ≤ cost of optimal solution, $O(b^{fC^∗}/cl)$
where $C^∗$ is the cost of the optimal solution
Space: # of nodes with g ≤ cost of optimal solution, $O(b^{fC^∗}/cl)$
Optimal: Yes—nodes expanded in increasing order of $g(n)$


## Depth-first search
- Expand deepest unexpanded node
- Depth-first search always expands the deepest node in the frontier first.
- Implemented as a call to BEST-FIRST-SEARCH where the evaluation function f is the negative of the depth.
- It is usually implemented not as a graph search but as a tree-like search that does not keep a table of reached states.

- Implementation:
  fringe = LIFO queue, i.e., put successors at front

The search proceeds immediately to the deepest level of the search tree, where the nodes have no successors.
The search then “backs up” to the next deepest node that still has unexpanded successors.

Depth-first search is not cost-optimal as it returns the first solution it finds, even if it is not cheapest.
For finite state spaces that are trees it is efficient and complete; for acyclic state spaces it may end up expanding the same state many times via different paths, but will (eventually) systematically explore the entire space.
In cyclic state spaces it can get stuck in an infinite loop.
in infinite state spaces, depth-first search is not systematic as it can get stuck going down an infinite path, even if there are no cycles
Thus, depth-first search is incomplete.


### Properties of depth-first search
Complete: No: fails in infinite-depth spaces, spaces with loops 
  Modify to avoid repeated states along path
    ⇒ complete in finite spaces
Time: $O(b^m)$: terrible if m is much larger than d
  but if solutions are dense, may be much faster than breadth-first
Space: $O(bm)$, i.e., linear space! 
Optimal: No


## Depth-limited search
- depth-first search with depth limit l, 
- i.e., nodes at depth l have no successors

### Recursive implementation:
```
function Depth-Limited-Search( problem,limit) returns soln/fail/cutoff
  Recursive-DLS(Make-Node(Initial-State [problem]),problem,limit)

function Recursive-DLS(node,problem,limit) returns soln/fail/cutoff
  cutoff-occurred? ←false
  if Goal-Test(problem,State[node]) then return node
  else if Depth[node] = limit then return cutoff
  else for each successor in Expand(node,problem) do 
    result ← Recursive-DLS(successor,problem,limit) 
    if result = cutoff then cutoff-occurred? ←true
    else if result /= failure then return result
  if cutoff-occurred? then return cutoff else return failure
```

A variant of depth-first search called backtracking search uses even less memory.
In backtracking, only one successor is generated at a time rather than all successors; each partially expanded node remembers which successor to generate next. 
In addition, successors are generated by modifying the current state description directly rather than allocating memory for a brand-new state
With backtracking we also have the option of maintaining an efficient set data structure for the states on the current path, allowing us to check for a cyclic path in O(1) time rather than O(m)
Backtracking is critical to the success of many problems with large state descriptions, such as robotic assembly


## Depth-limited search
Depth-limited search search, is a version of depth-first search, in which there is a depth limit $l$ that prevents it from going down an infinite path.
The depth limit, $l$, and treat all nodes at depth $l$ as if they had no successors.
The time complexity is $O(b^l)$ and the space complexity is $O(bl)$
It is important to set $l$ as setting it to low would cause the algorithm to fail to reach the solution, making it incomplete again.
And setting it too high would cause inefficencies.

## Iterative deepening search
In depth-limited search, A poor choice for $l$ would cause the algorithm to fail to reach the solution, making it incomplete again
Iterative deepening search solves the problem of picking a good value for $l$ by trying all values: first 0, then 1, then 2, and so on—until either a solution is found, or the depth-limited search returns the failure value rather than the cutoff value.
Iterative deepening combines many of the benefits of depth-first and breadth-first search.



```
function Iterative-Deepening-Search( problem) returns a solution
  inputs: problem, a problem
  for depth ← 0 to ∞ do
    result ← Depth-Limited-Search( problem, depth)
    if result /= cutoff then return result
  end
```

Like depth-first search, its memory requirements are modest: O(bd) when there is a solution, or O(bm) on finite state spaces with no solution. 
Like breadth-first search, iterative deepening is optimal for problems where all actions have the same cost, and is complete on finite acyclic state spaces, or on any finite state space when we check nodes for cycles all the way up the path

### Properties of iterative deepening search
Complete: Yes
Time: $(d+ 1)b^0 + db^1 + (d− 1)b^2 + .. . + b^d = O(b^d)$
Space: $O(bd)$
Optimal: Yes, if step cost = 1
  Can be modified to explore uniform-cost tree



$N(IDS) = (d)b^1 + (d −1)b^2 + (d −2)b^3 ··· +b^d$
$N(BFS) = (d)b^1 + (d −1)b^2 + (d −2)b^3 ··· +b^d$

Numerical comparison for b= 10 and d = 5, solution at far right leaf:


$N (IDS) = 50 + 400 + 3, 000 + 20, 000 + 100, 000 = 123, 450$
$N (BFS) = 10 + 100 + 1, 000 + 10, 000 + 100, 000 + 999, 990 = 1, 111, 100$

- IDS does better because other nodes at depth d are not expanded 
- BFS can be modified to apply goal test when a node is generated

# Repeated states
Failure to detect repeated states can turn a linear problem into an exponential one!

## Bidirectional search
An alternative approach called bidirectional search, Which simultaneously searches forward from the initial state and backwards from the goal state(s)

```
function BIBF-SEARCH(problemF , fF , problemB, fB) returns a solution node, or failure
  nodeF ←NODE(problemF .INITIAL) // Node for a start state
  nodeB←NODE(problemB.INITIAL) // Node for a goal state
  frontierF ←a priority queue ordered by fF , with nodeF as an element
  frontierB←a priority queue ordered by fB, with nodeB as an element
  reachedF ←a lookup table, with one key nodeF.STATE and value nodeF
  reachedB←a lookup table, with one key nodeB.STATE and value nodeB
  solution←failure
  while not TERMINATED(solution, frontierF , frontierB) do
    if fF (TOP(frontierF )) < fB(TOP(frontierB)) then
      solution←PROCEED(F, problemF frontierF , reachedF , reachedB, solution)
    else solution←PROCEED(B, problemB, frontierB, reachedB, reachedF , solution)
  return solution

function PROCEED(dir, problem, frontier, reached, reached2, solution) returns a solution
  // Expand node on frontier; check against the other frontier in reached2.
  // The variable “dir” is the direction: either F for forward or B for backward.
  node←POP(frontier)
  for each child in EXPAND(problem, node) do
    s←child.STATE
    if s not in reached or PATH-COST(child) < PATH-COST(reached[s]) then
      reached[s]←child
      add child to frontier
      if s is in reached2 then
        solution2←JOIN-NODES(dir, child, reached2[s]))
        if PATH-COST(solution2) < PATH-COST(solution) then
          solution←solution2
  return solution
```

There are many different versions of bidirectional search, just as there are many different unidirectional search algorithms.
Although there are two separate frontiers, the node to be expanded next is always one with a minimum value of the evaluation function, across either frontier.






# Uninformed Search 

An uninformed search algorithm is given no clue about how close a state is to the goal(s)
Uninformed strategies use only the information available in the problem definition

Uninformed Search Strategies:
- Breadth-first search 
- Uniform-cost search 
- Depth-first search 
- Depth-limited search
- Iterative deepening search

### Breadth-first search
- Expand shallowest unexpanded node
- The root node is expanded first, then all the successors of the root node are expanded next, then their successors, and so on
- This is a systematic search strategy that is therefore complete even on infinite state spaces
- Breadth-first search always finds a solution with a minimal number of actions, because when it is generating nodes at depth d, it has already generated all the nodes at depth d − 1, so if one of them were a solution, it would have been found

Implementation:
- fringe is a FIFO queue, i.e., new successors go at end
- A first-in-first-out queue will be faster than a priority queue, and will give us the correct order of nodes: new nodes (which are always deeper than their parents) go to the back of the queue, and old nodes, which are shallower than the new nodes, get expanded first

When appropriate:
- When all actions have the same cost.

Disadvantage:
- The memory requirements are a bigger problem for breadth-first search than the execution time.
- exponential-complexity search problems cannot be solved by uninformed search for any but the smallest instances

Properties of breadth-first search
Complete: Yes (if b is finite)
Time: $1 + b+ b2+ b3 + ... + b_d+ b(b_d − 1) = O(b_d+1)$, i.e., exp. in d
Space: $O(b_d+1)$ (keeps every node in memory)
Optimal: Yes (if cost = 1 per step); not optimal in general
*Space* is the big problem; can easily generate nodes at 100MB/sec 
so 24hrs = 8640GB

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

### Dijkstra’s algorithm or Uniform-cost search
- Expand least-cost unexpanded node

Implementation:
  fringe = queue ordered by path cost, lowest first
- Equivalent to breadth-first if step costs all equal

Complete: Yes, if step cost ≥ c
Time: # of nodes with g ≤ cost of optimal solution, $O(b^{fC^∗}/cl)$
where $C^∗$ is the cost of the optimal solution
Space: # of nodes with g ≤ cost of optimal solution, $O(b^{fC^∗}/cl)$
Optimal: Yes—nodes expanded in increasing order of $g(n)$

Depth-first search
- Expand deepest unexpanded node
- Implementation:
  fringe = LIFO queue, i.e., put successors at front

Properties of depth-first search
Complete: No: fails in infinite-depth spaces, spaces with loops 
  Modify to avoid repeated states along path
    ⇒ complete in finite spaces
Time: $O(b^m)$: terrible if m is much larger than d
  but if solutions are dense, may be much faster than breadth-first
Space: $O(bm)$, i.e., linear space! 
Optimal: No


Depth-limited search
- depth-first search with depth limit l, 
- i.e., nodes at depth l have no successors

Recursive implementation:
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

Iterative deepening search
```
function Iterative-Deepening-Search( problem) returns a solution
  inputs: problem, a problem
  for depth ← 0 to ∞ do
    result ← Depth-Limited-Search( problem, depth)
    if result /= cutoff then return result
  end
```

Properties of iterative deepening search
Complete: Yes
Time: $(d+ 1)b^0 + db^1 + (d− 1)b^2 + .. . + b^d = O(b^d)$
Space: $O(bd)$
Optimal: Yes, if step cost = 1
  Can be modified to explore uniform-cost tree
Numerical comparison for b= 10 and d = 5, solution at far right leaf:
$N (IDS) = 50 + 400 + 3, 000 + 20, 000 + 100, 000 = 123, 450$
$N (BFS) = 10 + 100 + 1, 000 + 10, 000 + 100, 000 + 999, 990 = 1, 111, 100$

- IDS does better because other nodes at depth d are not expanded 
- BFS can be modified to apply goal test when a node is generated

# Repeated states
Failure to detect repeated states can turn a linear problem into an exponential one!




Informed (Heuristic) 
- Informed search methods have access to a heuristic function $h(n)$ that estimates the cost of a solution from $n$.

Graph search

```
function Graph-Search( problem, fringe) returns a solution, or failure
  closed ← an empty set
  fringe ← Insert (Make-Node(Initial-State [problem]),fringe)
  loop do
    if fringe is empty then return failure
    node ← Remove-Front(fringe)
    if Goal-Test(problem,State[node]) then return node
    if State[node] is not in closed then
      add State[node] to closed
      fringe ← InsertAl l(Expand(node,problem),fringe)
  end
```

Search Strategies
- Greedy search
- A* Search

Greedy best-first search
- Greedy best-first search is a form of best-first search that expands first the node with the lowest h(n) value—the node that appears to be closest to the goal—on the grounds that this is likely to lead to a solution quickly. So the evaluation function f(n) = h(n)
- Greedy search expands the node that appears to be closest to goal
- It uses an Evaluation function h(n) (heuristic)
  * It gives the estimate of cost from n to the closest goal

Properties of greedy search
Complete: No–can get stuck in loops, 
  e.g., Iasi → Neamt → Iasi → Neamt →
Complete in finite space with repeated-state checking
Time: $O(b^m)$, but a good heuristic can give dramatic improvement 
Space: $O(b^m)$—keeps all nodes in memory
Optimal: No

A* Search
- 
Idea: avoid expanding paths that are already expensive

Evaluation function: 
$$
f (n) = g(n) + h(n)
$$ 
Where:
- $g(n)$ = cost so far to reach n
- $h(n)$ = estimated cost to goal from n
- $f(n)$ = estimated total cost of path through n to goal

A key property is admissibility
A∗ search uses an admissible heuristic
i.e., $h(n) ≤ h∗(n)$ where $h∗(n)$ is the *true cost* from n. (Also require $h(n) ≥ 0$, so $h(G) = 0$ for any goal G.)
- an admissible heuristic is one that never overestimates the cost to reach a goal.
- An admissible heuristic is therefore optimistic.

A* is cost-optimal, which we can show with a proof by contradiction.
Suppose the optimal path has cost $C*$, but the algorithm returns a path with cost $C' > C*$.
The there must be some node $n$ which is on the optimal path and is unexpanded (because if all the nodes on the optimal path had been expanded, then we would have returned that optimal solution). So then, using the notation g* (n) to mean the cost of the optimal path from the start to n, and h*(n) to mean the cost of the optimal path from n to the nearest goal, we have



Optimality of A ∗ (standard proof)
Suppose some suboptimal goal $G_2$ has been generated and is in the queue. Let $n$ be an unexpanded node on a shortest path to an optimal goal $G_1$.

$f(G_2) = g(G2)$ since $h(G_2)$ = 0$\
$f(G_2) > g(G1)$ since $G_2$ is suboptimal\
$f(G_2) ≥ f(n)$ since $h$ is admissible

Since $f(G_2) > f(n)$, A∗ will never select $G_2$ for expansion


Properties of A∗
Complete: Yes, unless there are infinitely many nodes with f ≤ f (G)
Time: Exponential in [relative error in h × length of soln.] 
Space: Keeps all nodes in memory
Optimal: Yes—cannot expand $f_{i+ 1}$ until $f_i$ is finished 
A∗ expands all nodes with $f(n) < C∗$
A∗expands some nodes with $f(n) = C∗$
A∗expands no nodes with $f(n) > C∗$


Heuristic Function:

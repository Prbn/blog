# Search Algorithms
A search algorithm takes a search problem as input and returns a solution, or an indication of failure
It is important to understand the distinction between the state space and the search tree.

## State Space
The state space describes the (possibly infinite) set of states in the world, and the actions that allow transitions from one state to another.

## Search Tree
- The search tree describes paths between these states, reaching towards the goal. 
- The search tree may have multiple paths to (and thus multiple nodes for) any given state, but each node in the tree has a unique path back to the root (as in all trees).

## Tree search algorithms
Basic idea:
offline, simulated exploration of state space by generating successors of already-explored states (a.k.a. expanding states)

```
function Tree-Search( problem, strategy) returns a solution, or failure 
  initialize the search tree using the initial state of problem
  loop do
    if there are no candidates for expansion then return failure 
    choose a leaf node for expansion according to strategy
    if the node contains a goal state then return the corresponding solution
    else expand the node and add the resulting nodes to the search tree
  end
```

Implementation: states vs. nodes
A **state** is a (representation of) a physical configuration
A **node** is a data structure constituting part of a search tree includes parent, children, depth, path cost g(x)
**States** do not have parents, children, depth, or path cost!

The Expand function creates new nodes, filling in the various fields and using the SuccessorFn of the problem to create the corresponding states

Implementation: general tree search

```
function Tree-Search( problem, fringe) returns a solution, or failure 
  fringe ← Insert (Make-Node(Initial-State [problem]),fringe) 
  loop do
    if fringe is empty then return failure
    node ← Remove-Front(fringe)
    if Goal-Test(problem,State(node)) then return node 
    fringe ← InsertAl l(Expand(node,problem),fringe)
```

```
function Expand( node, problem) returns a set of nodes
  successors← the empty set
  for each action,result in Successor-Fn(problem,State [node]) do
    s ← a new Node
    Parent-Node[s]← node; Action[s]← action; State [s]← result
    Path-Cost[s] ← Path-Cost[node] + Step-Cost(node,action,s)
    Depth[s]← Depth[node] + 1 
    add s to successors
  return successors
```

Search strategies
- A strategy is defined by picking the order of node expansion
- Strategies are evaluated along the following dimensions: 
  * completeness—does it always find a solution if one exists? 
  * time complexity—number of nodes generated/expanded 
  * space complexity—maximum number of nodes in memory 
  * optimality—does it always find a least-cost solution?

Time and space complexity are measured in terms of 
  * b—maximum branching factor of the search tree 
  * d—depth of the least-cost solution
  * m—maximum depth of the state space (may be ∞)


### Best-first search
It is a general approach in which we choose a node, $n$, with minimum value of some evaluation function, $f(n)$.
On each iteration we choose a node on the frontier with minimum $f(n)$ value, return it if its state is a goal state, and otherwise apply EXPAND to generate child nodes
Each child node is added to the frontier if it has not been reached before, or is re-added if it is now being reached with a path that has a lower path cost than any previous path
The algorithm returns either an indication of failure, or a node that represents a path to a goal.

*The best-first search algorithm, and the function for expanding a node.*
```pseudocode
function BEST-FIRST-SEARCH(problem,f) returns a solution node or failure
  node←NODE(STATE=problem.INITIAL)
  frontier←a priority queue ordered by f , with node as an element
  reached←a lookup table, with one entry with key problem.INITIAL and value node
  while not IS-EMPTY(frontier) do
    node←POP(frontier)
    if problem.IS-GOAL(node.STATE) then return node
    for each child in EXPAND(problem, node) do
      s←child.STATE
      if s is not in reached or child.PATH-COST < reached[s].PATH-COST then
        reached[s]←child
        add child to frontier
  return failure

function EXPAND(problem, node) yields nodes
  s←node.STATE
  for each action in problem.ACTIONS(s) do
    s′ ←problem.RESULT(s, action)
    cost←node.PATH-COST + problem.ACTION-COST(s, action,s′)
    yield NODE(STATE=s′, PARENT=node, ACTION=action, PATH-COST=cost)
```



### Search data structure
Search algorithms require a data structure to keep track of the search tree.
A node in the tree is represented by a data structure with four components:
- node.STATE: the state to which the node corresponds;
- node.PARENT: the node in the tree that generated this node;
- node.ACTION: the action that was applied to the parent’s state to generate this node;
- node.PATH-COST: the total cost of the path from the initial state to this node. In mathematical formulas, we use g(node) as a synonym for PATH-COST.

A data structure is require to store the frontier. 
The appropriate choice is a queue of some kind, because the operations on a frontier are:
- IS-EMPTY(frontier) returns true only if there are no nodes in the frontier.
- POP(frontier) removes the top node from the frontier and returns it.
- TOP(frontier) returns (but does not remove) the top node of the frontier.
- ADD(node, frontier) inserts node into its proper place in the queue

Three kinds of queues are used in search algorithms:
- A **priority queue** first pops the node with the minimum cost according to some evaluation function, f . It is used in best-first search
- A **FIFO queue** or first-in-first-out queue first pops the node that was added to the queue first
- A **LIFO queue** or last-in-first-out queue (also known as a stack) pops first the most recently added node

###  Redundant paths

**Redundant paths** occur when multiple paths lead to the same state, causing inefficiencies in search algorithms. This is often caused by **cycles** (repeated states in loops) or alternative, less efficient paths to a destination.

Key strategies to handle redundant paths include:

1. **Remembering Reached States**: Algorithms like **best-first search** track all previously visited states, allowing the search to eliminate worse paths, but this requires more memory.

2. **Not Checking for Redundant Paths**: In some problems where revisiting states is rare or impossible, memory can be saved by not tracking reached states, though this may slow down the search by exploring redundant paths.

3. **Cycle Detection**: A compromise that eliminates **cycles** without storing all visited states. This checks if a state has been visited earlier in the same path, preventing infinite loops and some redundancy.

**Graph search** tracks visited states to avoid redundancy, while **tree-like search** does not, offering lower memory usage but slower performance due to redundant path exploration.

### Measuring Problem-Solving Performance

To evaluate and compare search algorithms, several criteria are used to assess their performance. These include:

1. **Completeness**:
   - The algorithm guarantees finding a solution if one exists by systematically exploring all reachable states.

2. **Cost Optimality**:
   - The algorithm finds the solution with the lowest path cost compared to others.
   - A cost-optimal algorithm ensures that the solution found minimizes the total cost compared to other solutions.

3. **Time Complexity**:
   - Measures how long the algorithm takes to find a solution, either in time or by counting explored states and actions.
   - This can be measured in terms of actual time (seconds) or more abstractly by counting the number of states and actions the algorithm explores.

4. **Space Complexity**:
   - The memory required to store states and paths during the search process.
   - Space complexity refers to the amount of memory the algorithm needs to store intermediate states and paths during the search process.

In infinite state spaces, algorithms must avoid infinite loops and explore systematically. Time and space complexity depend on factors like solution depth, path length, and branching factor.

## Uninformed Search 
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

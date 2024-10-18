# Search Algorithms
A search algorithm takes a search problem as input and returns a solution, or an indication of failure
It is important to understand the distinction between the state space and the search tree.

## State Space and Search Tree
- We consider algorithms that superimpose a search tree over the state-space graph, forming various paths from the initial state, trying to find a path that reaches a goal state.
- Each node in the search tree corresponds to a state in the state space and the edges in the search tree correspond to actions. The root of the tree corresponds to the initial state of the problem.

It is important to understand the distinction between the state space and the search tree.

## State Space
The state space describes the (possibly infinite) set of states in the world, and the actions that allow transitions from one state to another.

## Search Tree
- The search tree describes paths between these states, reaching towards the goal. 
- The search tree may have multiple paths to (and thus multiple nodes for) any given state, but each node in the tree has a unique path back to the root (as in all trees).

## Tree search algorithms
Basic idea is to simulated exploration of state space by generating successors of already-explored states (a.k.a. expanding states)
We can expand the node, by considering the available ACTIONS for that state, using the RESULT function to see where those actions lead to, and generating a new node (called a child node or successor node) for each of the resulting states. Now the next step is to choose which of these child nodes to consider next. This is the essence of search—following up one option now and putting the others aside for later. This is called the frontier of the search tree. A state is **reached** if it has had a node generated for it.
The **frontier** separates two regions of the state-space graph: an interior region where every state has been expanded, and an exterior region of states that have not yet been reached.


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

![Tree_search_example](https://raw.githubusercontent.com/Prbn/prbn.github.io/refs/heads/main/_resource/Tree_search_exampl_GIF.gif)

### Implementation: states vs. nodes
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
- A strategy is defined by picking the *order of node expansion*
- Strategies are evaluated along the following dimensions: 
  * completeness—does it always find a solution if one exists? 
  * time complexity—number of nodes generated/expanded 
  * space complexity—maximum number of nodes in memory 
  * optimality—does it always find a least-cost solution?

Time and space complexity are measured in terms of 
  * b—maximum branching factor of the search tree 
  * d—depth of the least-cost solution
  * m—maximum depth of the state space (may be ∞)


# Best-first search
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



## Search data structure
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

##  Redundant paths

**Redundant paths** occur when multiple paths lead to the same state, causing inefficiencies in search algorithms. This is often caused by **cycles** (repeated states in loops) or alternative, less efficient paths to a destination.

Key strategies to handle redundant paths include:

1. **Remembering Reached States**: Algorithms like **best-first search** track all previously visited states, allowing the search to eliminate worse paths, but this requires more memory.

2. **Not Checking for Redundant Paths**: In some problems where revisiting states is rare or impossible, memory can be saved by not tracking reached states, though this may slow down the search by exploring redundant paths.

3. **Cycle Detection**: A compromise that eliminates **cycles** without storing all visited states. This checks if a state has been visited earlier in the same path, preventing infinite loops and some redundancy.

**Graph search** tracks visited states to avoid redundancy, while **tree-like search** does not, offering lower memory usage but slower performance due to redundant path exploration.

## Measuring Problem-Solving Performance

To evaluate and compare search algorithms, several criteria are used to assess their performance. These include:

1. **Completeness**:
   - The algorithm guarantees finding a solution if one exists by systematically exploring all reachable states.
   - An algorithm is said to be **complete** if it guarantees finding a solution if one exists.

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



## Graph search

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

## Tree search
A strategy is defined by picking the order of node expansion

```
function Tree-Search( problem, fringe) returns a solution, or failure 
  fringe ← Insert(Make-Node(Initial-State[problem]), fringe) 
  loop do
    if fringe is empty then return failure
    node ← Remove-Front(fringe)
    if Goal-Test[problem] applied to State(node) succeeds return node 
    fringe ← InsertAll(Expand(node, problem), fringe)
```


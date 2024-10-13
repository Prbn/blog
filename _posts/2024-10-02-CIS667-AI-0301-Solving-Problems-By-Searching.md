# Problem-solving agents

When the correct action to take is not immediately obvious, an agent may need to to plan ahead: to consider a sequence of actions that form a path to a goal state. Such an agent is called a problem-solving agent, and the computational process it undertakes is called search

Problem-solving agents use atomic representations. Where, states of the world are considered as wholes, with no internal structure visible to the problem-solving algorithms. 
Agents that use factored or structured representations of states are called planning agents


Restricted form of general agent
```
function Simple-Problem-Solving-Agent( percept) returns an action
  static: seq, an action sequence, initially empty
    state, some description of the current world state
    goal, a goal, initially null
    problem, a problem formulation
  state ← Update-State(state, percept)
  if seq is empty then
    goal← Formulate-Goa l(state)
    problem ← Formulate-Problem(state, goal) 
    seq← Search( problem)
  action ← Recommendation(seq,state) 
  seq← Remainder(seq,state)
  return action
```

Note: this is offline problem solving; solution executed “eyes closed.” 
Online problem solving involves acting without complete knowledge.

Example Problems

Example: Romania


four-phase problem-solving process
- Goal formulation
- Problem formulation
- Search
- Execution


Goal formulation
Goals organize Gbehavior by limiting the objectives and hence the actions to be considered.

Problem formulation
The agent devises a description of the states and actions necessary to reach the goal—an abstract model of the relevant part of the world. 

Search
Before taking any action in the real world, the agent simulates sequences of actions in its model, searching until it finds a sequence of actions that reaches the goal.
Such a sequence is called a solution. 
The agent might have to simulate multiple sequences that do not reach the goal, but eventually it will find a solution.

Execution
The agent can now execute the actions in the solution, one at a time.

Search problems and solutions
A search problem can be defined formally as follows: 
- A set of possible states that the environment can be in.
- The initial state that the agent starts in
- A set of one or more goal states.
- The actions available to the agent. Given a state $s$, ACTIONS(s) returns a finite set of actions that can be executed in $s$.
- A transition model, which describes what each action does. RESULT($s, a$) returns the Transition model state that results from doing action $a$ in state $s$.
- An action cost function, denoted by ACTION-COST($s,a,s′$) when we are programming Action cost function or $c(s,a,s′)$ when we are doing math, that gives the numeric cost of applying action a in state s to reach state $s′$.

* A sequence of actions forms a path, and a solution is a path from the initial state to a goal Path state. 
* We assume that action costs are additive; that is, the total cost of a path is the sum of the individual action costs. 
* An optimal solution has the lowest path cost among all solutions.
* The state space can be represented as a graph in which the vertices are states and the directed edges between them are actions.

### Formulating problems

**Abstraction**: The process of removing detail from a representation

**Level of abstraction**:
- The abstraction is valid if we can elaborate any abstract solution into a solution in the more detailed world
- The abstraction is useful if carrying out each of the actions in the solution is easier than the original problem
- The choice of a good abstraction involves removing as much detail as possible while retaining validity and ensuring that the abstract actions are easy to carry out.

#### Standardized problems
A standardized problem is intended to illustrate or exercise various problem-solving methods.

Single-state problem formulation
A problem is defined by four items:
1. Initial State
2. Successor function
3. goal test
4. path cost

A solution is a sequence of actions leading from the initial state to a goal state

Selecting a state space
- Real world is absurdly complex
- state space must be abstracted for problem solving
- Each abstract action should be “easier” than the original problem!

**Example: vacuum world state space graph**

states: [integer dirt and robot locations (ignore dirt amounts etc.)]
actions: [Left, Right, Suck, NoOp]
goal test: [no dirt]
path cost: [1 per action (0 for NoOp]


**Example: The 8-puzzle (sokoban puzzle)**

states: integer locations of tiles (ignore intermediate positions) 
actions: move blank left, right, up, down (ignore unjamming etc.) 
goal test: = goal state (given)
path cost: 1 per move

Note: optimal solution of n-Puzzle family is NP-hard


Example: robotic assembly

states: real-valued coordinates of robot joint angles parts of the object to be assembled
actions: continuous motions of robot joints
goal test: complete assembly with no robot included!
path cost: time to execute

Real-world problems
A real-world problem is one whose solutions people actually use, and whose formulation is idiosyncratic, not standardized, because, for example, each robot has different sensors that produce different data.

Search Algorithms
A search algorithm takes a search problem as input and returns a solution, or an indication of failure

1. Tree search algorithms
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


Uninformed Search 

Uninformed strategies use only the information available 
in the problem definition

Uninformed Search Strategies:
- Breadth-first search 
- Uniform-cost search 
- Depth-first search 
- Depth-limited search
- Iterative deepening search

Breadth-first search
- Expand shallowest unexpanded node

Implementation:
  - fringe is a FIFO queue, i.e., new successors go at end

Properties of breadth-first search
Complete: Yes (if bis finite)
Time: $1 + b+ b2+ b3 + ... + b_d+ b(b_d − 1) = O(b_d+1)$, i.e., exp. in d
Space: $O(b_d+1)$ (keeps every node in memory)
Optimal: Yes (if cost = 1 per step); not optimal in general
*Space* is the big problem; can easily generate nodes at 100MB/sec 
so 24hrs = 8640GB

Uniform-cost search
- Expand least-cost unexpanded node
- Implementation:
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

Greedy search
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
Idea: avoid expanding paths that are already expensive

Evaluation function: 
$$
f (n) = g(n) + h(n)
$$ 
Where:
- $g(n)$ = cost so far to reach n
- $h(n)$ = estimated cost to goal from n
- $f(n)$ = estimated total cost of path through n to goal

A∗ search uses an admissible heuristic
i.e., $h(n) ≤ h∗(n)$ where $h∗(n)$ is the *true cost* from n. (Also require $h(n) ≥ 0$, so $h(G) = 0$ for any goal G.)

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




# Constraint Satisfaction Problems

## Defining Constraint Satisfaction Problems

A constraint satisfaction problem (CSP) consists of three components, X, D, and C:
- **X** is a set of variables, ${X_1, X_2 ….. X_n}$.
- **D** is a set of domains, ${D_1, D_2, …. , D_n}$, one for each variable
- **C** is a set of constraints that specify allowable combination of values

CSPs deal with assignments of values to variables.
- A complete assignment is one in which every variable is assigned a value, and a solution to a CSP is a consistent, complete assignment.
- A partial assignment is one that leaves some variables unassigned.
- Partial solution is a partial assignment that is consistent

Standard search problem:
  *state* is a “black box”—any old data structure that supports goal test, eval, successor

CSP: 
  *state* is defined by variables X_i with values from domain D_i
  *goal test* is a set of constraints specifying allowable combinations of values for subsets of variables

- Simple example of a formal representation language
- Allows useful general-purpose algorithms with more power than standard search algorithms

## Constraint graph

Binary CSP: each constraint relates at most two variables
Constraint graph: nodes are variables, arcs show constraints

General-purpose CSP algorithms use the graph structure to speed up search. E.g., Tasmania is an independent subproblem!

## Varieties of CSPs

**Discrete variables**
  finite domains; size $d ⇒ O(d^n)$ complete assignments
  - e.g., Boolean CSPs, incl. Boolean satisfiability (NP-complete)
  infinite domains (integers, strings, etc.)
  - e.g., job scheduling, variables are start/end days for each job
  - need a constraint language, e.g., $StartJob_1+ 5 ≤ StartJob_3$
  - linear constraints solvable, nonlinear undecidable

**Continuous variables**
  - Example: start/end times for Hubble Telescope observations
  - linear constraints solvable in poly time by LP methods

 ## Varieties of constraints

- **Unary constraints** involve a single variable
- **Binary constraints** involve pairs of variables
- **Higher-order constraints** involve 3 or more variables
  * Example: cryptarithmetic column constraints
- **Preferences (soft constraints)** often representable by a cost for each variable assignment
    → constrained optimization problems
  * Example: red is better than green

## Real-world CSPs

- Assignment problems
  * e.g., who teaches what class
- Timetabling problems
  * e.g., which class is offered when and where?
- Hardware configuration
- Spreadsheets
- Transportation scheduling
- Factory scheduling
- Floorplanning

Notice that many real-world problems involve real-valued variables

## Standard search formulation (incremental)


## Backtracking search

**psudocode**
```
function Backtracking-Search(csp) returns solution/failure
  return Recursive-Backtracking({ }, csp)
function Recursive-Backtracking(assignment, csp) returns soln/failure
  if assignment is complete then return assignment
  var ← Select-Unassigned-Variable(Variables[csp], assignment, csp)
  for each value in Order-Domain-Values(var, assignment, csp) do
    if value is consistent with assignment given Constraints[csp] then
      add {var = value} to assignment
      result← Recursive-Backtracking(assignment, csp)
      if result /= failure then return result
      remove {var = value} from assignment
  return failure
```


### Minimum remaining values

- choose the variable with the fewest legal values

### Degree heuristic

- Tie-breaker among MRV variables
- Degree heuristic: choose the variable with the most constraints on remaining variables

### Least constraining value

Given a variable, choose the least constraining value:
  the one that rules out the fewest values in the remaining variables

- Combining these heuristics makes 1000 queens feasible

### Forward checking

Idea: Keep track of remaining legal values for unassigned variables Terminate search when any variable has no legal values


### Constraint propagation

Forward checking propagates information from assigned to unassigned variables, but doesn’t provide early detection for all failures:

Constraint propagation repeatedly enforces constraints locally

### Arc consistency

Simplest form of propagation makes each arc consistent

X → Y is consistent if for every value x of X there is some allowed y
- If X loses a value, neighbors of X need to be rechecked
- Arc consistency detects failure earlier than forward checking 
- Can be run as a preprocessor or after each assignment

**Arc consistency algorithm**

psudocode
```
function AC-3( csp) returns the CSP, possibly with reduced domains
  inputs: csp, a binary CSP with variables {X1, X2, . . . , Xn}
  local variables: queue, a queue of arcs, initially all the arcs in csp
  while queue is not empty do
    (Xi, Xj)← Remove-First(queue)
    if Remove-Inconsistent-Values(X i, Xj) then 
      for each Xk in Neighbors[Xi] do
        add (Xk, Xi) to queue
function Remove-Inconsistent-Values( Xi, Xj) returns true iff succeeds
  removed←false
  for each x in Domain[Xi] do
    if no value y in Domain[Xj] allows (x,y) to satisfy the constraint Xi Xj
      then delete x from Domain[X i]; removed←true
  return removed
```

## Local Search for CSPs

- Local search algorithms can be very effective in solving many CSPs.
- Local search algorithms use a complete-state formulation where each state assigns a value to every variable, and the search changes the value of one variable at a time.
- Min-conflicts heuristic: value that results in the minimum number of conflicts with other variables that brings us closer to a solution. 
  * Usually has a series of plateaus

- Plateau search: allowing sideways moves to another state with the same score. 
  * can help local search find its way off the plateau.

- Constraint weighting aims to concentrate the search on the important constraints
  * Each constraint is given a numeric weight, initially all 1. 
  * weights adjusted by incrementing when it is violated by the current assignment

## Tree-structured CSPs

**Theorem**: if the constraint graph has no loops, the CSP can be solved in O(nd2) time

Compare to general CSPs, where worst-case time is $O(d^n)$

This property also applies to logical and probabilistic reasoning: an important example of the relation between syntactic restrictions and the complexity of reasoning.


### Algorithm for tree-structured CSPs
1. Choose a variable as root, order variables from root to leaves such that every node’s parent precedes it in the ordering
2. Forj from n down to 2, apply RemoveInconsistent(Parent(Xj), Xj)
3. For j from 1 to n, assign Xj consistently with Parent(Xj)


## Nearly tree-structured CSPs

**Conditioning**: instantiate a variable, prune its neighbors’ domains
**Cutset conditioning**: instantiate (in all ways) a set of variables such that the remaining constraint graph is a tree
Cutset size c ⇒ runtime $O(d^c ·(n − c)d^2)$, very fast for small c

## Iterative algorithms for CSPs
Hill-climbing, simulated annealing typically work with “complete” states, i.e., all variables assigned

To apply to CSPs: allow states with unsatisfied constraints operators reassign variable values
Variable selection: randomly select any conflicted variable 
Value selection by min-conflicts heuristic:
- choose value that violates the fewest constraints
- i.e., hillclimb with h(n) = total number of violated constraints






















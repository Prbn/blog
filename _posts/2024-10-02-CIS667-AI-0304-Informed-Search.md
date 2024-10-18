# Informed (Heuristic) Search Strategies

The informed search strategy uses domain-specific hints about the location of goals—can find solutions more efficiently than an uninformed strategy.
The hints come in the form of a heuristic function, denoted $h(n)$


Informed (Heuristic) 
- Informed search methods have access to a heuristic function $h(n)$ that estimates the cost of a solution from $n$.
  
$$
h(n) = \text{ estimated cost of the cheapest path from the state at node }n \text{ to a goal state}
$$


# Search Strategies in Special cases:
- Greedy best-first search
- A* Search

## Greedy best-first search
- Greedy best-first search is a form of best-first search that expands first the node with the lowest h(n) value—the node that appears to be closest to the goal—on the grounds that this is likely to lead to a solution quickly. So the evaluation function f(n) = h(n)
- Greedy search expands the node that appears to be closest to goal
- It uses an Evaluation function h(n) (heuristic)
  * It gives the estimate of cost from n to the closest goal

- Greedy best-first graph search is complete in finite state spaces, but not in infinite ones.
- The worst-case time and space complexity is $O(|V|)$
- Complexity can be substantially reduced with a good heuristic function.

### Properties of greedy search
Complete: No–can get stuck in loops, 
  e.g., Iasi → Neamt → Iasi → Neamt →
Complete in finite space with repeated-state checking
Time: $O(b^m)$, but a good heuristic can give dramatic improvement 
Space: $O(b^m)$—keeps all nodes in memory
Optimal: No

## A* Search
Idea: avoid expanding paths that are already expensive

Evaluation function: 
$$
f (n) = g(n) + h(n)
$$ 
Where:
- $g(n)$ = cost so far to reach n
- $h(n)$ = estimated cost to goal from n
- $f(n)$ = estimated total cost of path through n to goal

- A* search is **complete**.
- Whether A* is cost-optimal depends on certain properties of the heuristic.

### Admissibility
It is a key property of a heuristic
- an admissible heuristic is one that never overestimates the cost to reach a goal.
- An admissible heuristic is therefore optimistic.
- A cost-optimal A∗ search uses an admissible heuristic
i.e., $h(n) ≤ h∗(n)$ where $h∗(n)$ is the *true cost* from n. (Also require $h(n) ≥ 0$, so $h(G) = 0$ for any goal G.)

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


# Heuristic Function:

A heuristic is consistent if 
$$
h(n) ≤ c(n, a, n ) + h(n )
$$

If $h$ is consistent, we have

$$
f (n ) = g(n ) + h(n )
= g(n) + c(n, a, n ) + h(n )
≥ g(n) + h(n)
= f (n)
$$

I.e., f (n) is nondecreasing along any path.

### Domiance
If $h_2(n) ≥ h_1(n)$ for all $n$ (both admissible), then $h_2$ dominates $h_1$ and is better for search

Given any admissible heuristics $h_a$, $h_b$, 
$$
h(n) = max(h_a(n), h_b(n))
$$
is also admissible and dominates $h_a$, $h_b$

### Relaxed problems

Admissible heuristics can be derived from the exact solution cost of a relaxed version of the problem

For Example:\
If the rules of the 8-puzzle are relaxed so that a tile can move *anywhere*, then $h_1(n)$ gives the shortest solution
If the rules are relaxed so that a tile can move to any adjacent *square*, then $h_2(n)$ gives the shortest solution

Key point: the optimal solution cost of a relaxed problem is no greater than the optimal solution cost of the real problem

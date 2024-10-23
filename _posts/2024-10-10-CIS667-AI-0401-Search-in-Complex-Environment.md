# Search in Complex Environments

## Local Search and Optimization Problems
In many optimization problems, path is irrelevant; the goal state itself is the solution
In problems where the requirement is to find the optimal configuration (example: TSP):
- The state space is the set of “complete” configurations
- The goal is the find the configuration satisfying constraints (example: timetable)

In such cases, we can use iterative improvement algorithms;
  Where we keep a single “current” state and try to improve it

**Local search algorithms** operate by searching from a start state to neighboring states, without keeping track of the paths, nor the set of states that have been reached.
- They are not systematic
  * They might never explore a portion of the search space where a solution actually resides
- They start with any complete tour, then  perform pairwise exchanges
- Variants of this approach get within 1% of optimal very quickly with thousands of cities

*Properties:*
-  they use very little memory
-  they can often find reasonable solutions in large or infinite state spaces for which systematic algorithms are unsuitable.

Local search algorithms can also solve optimization problems, in which the aim is to find the best state according to an objective function.


### Example: Travelig Salesperson Problem (**TSP**)


### Example: n-queens
- Put n queens on an n × n board with no two queens on the same row, column, or diagonal
- Move a queen to reduce number of conflicts
- Almost always solves n-queens problems almost instantaneously for very large n, e.g., n= 1 million

## Hill-climbing

The hill-climbing search algorithm keeps track of one current state and on each iteration moves to the neighboring state with highest value—that is, it heads in the direction that provides the steepest ascent. 
It terminates when it reaches a “peak” where no neighbor has a higher value.
Hill climbing does not look ahead beyond the immediate neighbors of the current state.

This resembles trying to find the top of Mount Everest in a thick fog while suffering from amnesia.
Note that one way to use hill-climbing search is to use the negative of a heuristic cost function as the objective function; that will climb locally to the state with smallest heuristic distance to the goal.

```
function Hill-Climbing( problem) returns a state that is a local maximum
  inputs: problem, a problem
  local variables:  current, a node
                    neighbor, a node
  current← Make-Node(Initial-State [problem])
  loop do
    neighbor← a highest-valued successor of current
    if Value[neighbor] ≤ Value[current] then return State[current]
    current← neighbor
  end
```
Hill climbing is sometimes called greedy local search because it grabs a good neighbor state without thinking ahead about where to go next.
Hill climbing can make rapid progress toward a solution because it is usually quite easy to improve a bad state.

**Challenges**:
Hill climbing can get stuck for any of the following reasons:
- Local maxima:
  A local maximum is a peak that is higher than each of its neighboring states but lower than the global maximum.
  * Hill-climbing algorithms that reach the vicinity of a local maximum will be drawn upward toward the peak but will then be stuck with nowhere else to go
- Ridges:
  * Ridges result in a sequence of local maxima that is very difficult for greedy algorithms to navigate
- Plateaus:
  * A plateau is a flat area of the state-space landscape.
  * It can be a flat local maximum, from which no uphill exit exists, or a shoulder, from which progress is possible.
  * A hill-climbing search can get lost wandering on the plateau

**Solution:**
- Allow a sideways move
  * Random sideways moves escape from shoulders loop on flat maxima
- First-choice hill climbing
  * implement Stochastic hill climbing by generating successors randomly until one is generated that is better than the current state.
- Random-restart hill climbing
  *  It conducts a series of hill-climbing searches from randomly generated initial states, until a goal is found
  *  overcomes local maxima—trivially complete


### Simulated annealing
A hill-climbing algorithm that never makes “downhill” moves toward states with lower value (or higher cost) is always vulnerable to getting stuck in a local maximum. 
In contrast, a purely random walk that moves to a successor state without concern for the value will eventually stumble upon the global maximum, but will be extremely inefficient. 
Therefore, it seems reasonable to try to combine hill climbing with a random walk in a way that yields both efficiency and completeness.

**Idea:* escape local maxima by allowing some “bad” moves, but gradually decrease their size and frequency

```
function Simulated-Annealing( problem,schedule) returns a solution state
  inputs: problem, a problem
          schedule,a mapping from time to “temperature”
  local variables:  current, a node
                    next, a node
                    T, a “temperature” controlling prob. of downward steps
current← Make-Node(Initial-State [problem])
for t← 1 to ∞ do
  T ← schedule[t]
  if T = 0 then return current
  next← a randomly selected successor of current
  ∆E← Value[next] – Value[current]
  if ∆E > 0 then current← next
  else current← next only with probability e∆ E/T
```

The overall structure of the simulated-annealing algorithm is similar to hill climbing. 
Instead of picking the best move, however, it picks a random move. 
If the move improves the situation, it is always accepted. 
Otherwise, the algorithm accepts the move with some probability less than 1. 
The probability decreases exponentially with the “badness” of the move—the amount ∆E by which the evaluation is worsened. 
The probability also decreases as the “temperature” $T$ goes down: “bad” moves are more likely to be allowed at the start when $T$ is high, and they become more unlikely as $T$ decreases.
If the schedule lowers $T$ to 0 slowly enough, then a property of the Boltzmann distribution, $e^{∆E/T}$, is that all the probability is concentrated on the global maxima, which the algorithm will find with probability approaching 1.

**Properties of simulated annealin**

At fixed “temperature” T, state occupation probability reaches Boltzman distribution

$$
p(x)=ae^{\frac{E(x)}{kT}}
$$

T decreased slowly enough =⇒ always reach best state x* because $\frac{e^{\frac{E(x*)}{kT}}}{e^{\frac{E(x)}{kT}}} = e^{\frac{E(x*)-E(x)}{kT}} = 1 \text{ for small }T$

- based on [Metropolis et al., 1953](https://www.aliquote.org/pub/metropolis-et-al-1953.pdf), for physical process modelling
- Simulated annealing was used to solve VLSI layout problems beginning in the 1980s
- this is widely used in VLSI layout, airline scheduling, etc


## Local beam search
The local beam search algorithm keeps track of k states rather than just one. 
It begins with k randomly generated states. 
At each step, all the successors of all k states are generated. 
If any one is a goal, the algorithm halts. 
Otherwise, it selects the k best successors from the complete list and repeats.

The two algorithms are quite different.
- In a random-restart search, each search process runs independently of the others.
- In a local beam search, useful information is passed among parallel search threads.
- The algorithm quickly abandons unfruitful searches and moves its resources to where the most progress is being mad

**Idea:** 
- keep k states instead of 1;
- choose top k of all their successors

- Not the same as k searches run in parallel
- Searches that find good states recruit other searches to join them

**Problem:** 
- Local beam search can suffer from a lack of diversity among the k states — they can become clustered in a small region of the state space, making the search little more than a k-times-slower version of hill climbing.
- quite often, all k states end up on same local hill 


**Stochastic Beam search**
This variant analogous to stochastic hill climbing, helps alleviate this problem. 
Instead of choosing the top k successors, stochastic beam search chooses successors with probability proportional to the successor’s value, thus increasing diversity.

**Idea:** 
- choose ksuccessors randomly, biased towards good ones 
- Observe the close analogy to natural selection!

### Evolutionary algorithms
- Evolutionary algorithms can be seen as variants of stochastic beam search that are explicitly motivated by the metaphor of natural selection in biology
  *  there is a population of individuals (states), in which the fittest (highest value) individuals produce offspring (successor states) that populate the next generation, a process called recombination.

There are endless forms of evolutionary algorithms, varying in the following ways:
- size of the population
- representation of each individual
- selection process for selectin
- The recombination procedure
- The mutation rate
- The makeup of the next generation

#### Genetic algorithms
stochastic local beam search + generate successors from pairs of states

- GAs require states encoded as strings
- Crossover helps iff substrings are meaningful components
- GAs /= evolution: e.g., real genes encode replication machinery!


## Local search in continuous spaces
A continuous action space has an infinite branching factor, and thus can not be handled by most of the algorithms covered.

One way to deal with a continuous state space is to discretize it.
For example, instead of allowing the $(x_i ,y_i)$ locations to be any point in continuous two-dimensional space, we could limit them to fixed points on a rectangular grid with spacing of size δ (delta).


## Search with Nondeterministic Actions

The Agent does not know the state its transitioned to after action, the environment is nondeterministic. 
Rather, it will know the possible states it will be in, which is called “belief state”

### Examples:
- **The erratic vacuum world**
  * (if-then-else) steps. If statement tests to know the current state.
- **AND-OR** search trees
  * Two possible actions (OR nodes)
  * Branching that happens from a choice (AND nodes)
- **Try, try again**
  * A cyclic plan where minimum condition
  * (every leaf = goal state & reachable from other points in the plan)

## Search in Partially Observable Environments

**Problem of partial observability**:\
where the agent’s percepts are not enough to pin down the exact state.

**Searching with no observation**:\
Agent’s percepts provide no information at all, sensorless problem (or a conformant problem).
- Solution: sequence of actions, not a conditional plan

**Searching in partially observable environments** requires a function that monitors or estimatesthe environment to maintain the belief state


Link: 
[Metropolis et al., 1953:](https://www.aliquote.org/pub/metropolis-et-al-1953.pdf) https://www.aliquote.org/pub/metropolis-et-al-1953.pdf
[Understanding the Metropolis-Hastings Algorithm:](https://github.com/user-attachments/files/17469951/Understanding_the_Metropolis-H.pdf) https://github.com/user-attachments/files/17469951/Understanding_the_Metropolis-H.pdf
[Effiient Metropolis Jumping Rules:](https://stat.columbia.edu/~gelman/research/published/baystat5.pdf) https://stat.columbia.edu/~gelman/research/published/baystat5.pdf
[The Metropolis algorithm:](https://stat.columbia.edu/~gelman/research/published/baystat5.pdf) https://stat.columbia.edu/~gelman/research/published/baystat5.pdf


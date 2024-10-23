# Logical Agents

# Knowledge bases
They are set of sentences in a formal language

It is a declarative approach to building an agent (or other system)
* Tell it what it needs to know
* Then it can Ask itself what to do—answers should follow from the KB

Agents can be viewed at the knowledge level
* i.e., what they know, regardless of how implemented

at the implementation level
i.e., data structures in KB and algorithms that manipulate them

## A simple knowledge-based agent

The agent must be able to: 
- Represent states, actions, etc.
- Incorporate new percepts
- Update internal representations of the world
- Deduce hidden properties ofthe world
- Deduce appropriate actions

pseudocode
```
function KB-Agent(percept) returns an action
  static: KB, a knowledge base
          t, a counter, initially 0, indicating time
  Tel l(KB,Make-Percept-Sentence(percept,t)) 
  action ← Ask(KB,Make-Action-Query(t)) 
  Tell(KB, Make-Action-Sentence(action, t))
  t ← t + 1
  return action
```

## Example: Wumpus World

### PEAS description

**Performance measure**:
- gold +1000, death -1000
- -1 per step, -10 for using the arrow 

**Environment**:
- Squares adjacent to wumpus are smelly
- Squares adjacent to pit are breezy
- Glitter iff gold is in the same square
- Shooting kills wumpus if you are facing it
- Shooting uses up the only arrow
- Grabbing picks up gold if in same square
- Releasing drops the gold in same square

**Actuators**:
  Left turn, Right turn, Forward, Grab, Release, Shoot

**Sensors**:
  Breeze, Glitter, Smell

### Wumpus world characterization

**Observable**: No—only local perception
**Deterministic**: Yes—outcomes exactly specified 
**Episodic**: No—sequential at the level of actions 
**Static**: Yes—Wumpus and Pits donotmove 
**Discrete**: Yes
**Single-agent**: Yes—Wumpus is essentially a natural feature

## Logic in general

- **Logics** are formal languages for representing information such that conclusions can be drawn
- **Syntax** definesthe sentencesin the language
- **Semantics** define the “meaning” of sentences;
  * i.e., define truth of a sentence in a world

## Entailment

Entailment means that one thing follows from another:

$$
KB |= α
$$

Knowledge base $KB$ entails sentence $α$, if and only if $α$ is true in all worlds where $KB$ is true

Example:
- $x + y= 4$ entails $4= x + y$
- The KB containing "the Giants won" and "the Reds won" *entails* "Either the Giants won or the Reds won"

**Entailment is a relationship between sentences (i.e., syntax) that is based on semantics**

## Models

They are formally structured worlds with respect to which truth can be evaluated

We say $m$ is a model of a sentence $α$ if $α$ is true in $m$

$M (α)$ is the set of all models of $α$

Then $KB|=α$ if and only if $M(KB) ⊆ M (α)$
Example: 
  $KB$ = Giants won and Reds won
  $α$ = Giants won

## Inference

$KB f--i α = \text{ sentence } α$ can be derived from $KB$ by procedure $i$

Consequences of $KB$ area haystack; $α$ is a needle. \
Entailment = needle in haystack; inference = finding it

**Soundness**: i is sound if
  whenever KB f--iα, it is also true that KB |= α

**Completeness**: i is complete if
  whenever $KB |= α$, it is also true that $KB f--iα$

- We will define a logic (first-order logic) which is expressive enough to say almost anything of interest, and for which there exists a sound and complete inference procedure
- The procedure will answer any question whose answer follows from what is known by the KB.

## Propositional logic

### Syntax

Propositional logic is the simplest logic—illustrates basic ideas

The proposition symbols P1, P2 etc are sentences
- If $S$ is a sentence, $¬S$ is a sentence (negation)
- If $S_1$ and $S_2$ are sentences, $S_1 ∧ S_2$ is a sentence (conjunction) 
- If $S_1$ and $S_2$ are sentences, $S_1 ∨ S_2$ is a sentence (disjunction)
- If $S_1$ and $S_2$ are sentences, $S_1 ⇒ S_2$ is a sentence (implication)
- If $S_1$ and $S_2$ are sentences, $S_1 ⇔ S_2$ is a sentence (biconditional)

### Semantics

Each model specifies true/false for each proposition symbol

Rules for evaluating truth with respect to a model m:

- $¬S$ is *true* if $S$ is *false*
- $S_1 ∧ S_2$ is *true* if $S_1$ is *true* **and** $S_2$ is *true*
- $S_1 ∨ S_2$ is *true* if $S_1$ is *true* **or** $S_2$ is *true*
- $S_1 ⇒ S_2$ is *true* if $S_1$ is *false* **or** $S_2$ is *true*
- $S_1 ⇒ S_2$ is *false* if $S_1$ is *true* **and** $S_2$ is *false*
- $S_1 ⇔ S_2$ is *true* if $S_1 ⇒ S_2$ is *true* **and** $S_2 ⇒ S_1$ is *true*

Simple recursive process evaluates an arbitrary sentence
Example:
$¬P_{1,2} ∧ (P_{2,2} ∨ P_{3,1}) = true ∧ (false ∨ true) = true ∧ true = true$

**Truth tables for connectives**
| $P$ | $Q$ | $¬P$ | $P ∧ Q$ | $P ∨ Q$ | $P⇒Q$ | $P⇔Q$ |
|-----|-----|------|---------|---------|-------|-------|
| *false* | *false* | *true* | *false* | *false* | *true* | *true* |
| *false* | *true* | *true* | *false* | *true* | *true* | *false* |
| *true* | *false* | *false* | *false* | *true* | *false* | *false* |
| *true* | *true* | *false* | *true* | *true* | *true* | *true* |

## Wumpus world sentences

Let P_{i,j} be true if there is a pit in $[i, j]$.
Let B_{i,j} be true if there is a breeze in $[i, j]$.

**Pits cause breezes in adjacent squares**
$B_{1,1} ⇔ (P_{1,2} ∨ P_{2,1})$
$B_{2,1} ⇔ (P_{1,1} ∨ P_{2,2} ∨ P_{3,1})$

**A square is breezy if and only if there is an adjacent pit**

### Inference by enumeration
Depth-first enumeration of all models is sound and complete

```
function TT-Entails?(KB,α) returns true or false
  inputs: KB, the knowledge base, a sentence in propositional logic
    α, the query, a sentence in propositional logic
  symbols← a list of the proposition symbols in KB and α
  return TT-Check-A ll(KB,α,symbols,[])
function TT-Check-All(KB, α, symbols,model) returns true or false
  if Empty?(symbols) then
    if PL-True?(KB, model) then return PL-True?(α, model)
    else return true
  else do
    P ← First(symbols); rest← Rest(symbols)
    return TT-Check-All(KB, α, rest,Extend(P ,true,model)) and
      TT-Check-All(KB, α, rest,Extend(P ,false,model))
```

$O(2^n)$ for $n$ symbols; problem is *co-NP-complete*

### Logical equivalence

Two sentences are logically equivalent if true in same models:
$α ≡ β$ if and only if $α |= β$ and $β |= α$

- $(α ∧ β) ≡ (β ∧ α)$ commutativity of $∧$
- $(α ∨ β) ≡ (β ∨ α)$ commutativity of $∨$
- $((α ∧ β) ∧ γ) ≡ (α ∧ (β ∧ γ))$ associativity of $∧$ 
- $((α ∨ β) ∨ γ) ≡ (α ∨ (β ∨ γ))$ associativity of $∨$
- $¬(¬α) ≡ α$ double-negation elimination
- $(α ⇒ β) ≡ (¬β ⇒ ¬α)$ contraposition
- $(α ⇒ β) ≡ (¬α ∨ β)$ implication elimination
- $(α ⇔ β) ≡ ((α ⇒ β) ∧(β ⇒ α))$ biconditional elimination
- $¬(α ∧ β) ≡ (¬α ∨ ¬β)$ De Morgan
- $¬(α ∨ β) ≡ (¬α ∧ ¬β)$ De Morgan
- $(α ∧ (β ∨ γ)) ≡ ((α ∧ β) ∨(α ∧ γ))$ distributivity of $∧$ over $∨$
- $(α ∨ (β ∧ γ)) ≡ ((α ∨ β) ∧(α ∨ γ))$ distributivity of $∨$ over $∧$

## Validity and satisfiability

A sentence is valid if it is true in all models,
  * Example: $True, A ∨ ¬A, A ⇒ A, (A ∧ (A ⇒ B)) ⇒ B$

Validity is connected to inference via the Deduction Theorem:
  KB |= α if and only if (KB ⇒ α) is valid

A sentence is satisfiable if it is true in some model 
  * Example: $A ∨ B, C$

A sentence is unsatisfiable if it is true in no models 
  * Example: $A ∧ ¬A$

Satisfiability is connected to inference via the following:
  $KB |= α$ if and only if $(KB ∧ ¬α)$ is unsatisfiable 
i.e., prove $α$ by reductio adabsurdum

## Proof methods

Proof methods divide into (roughly) two kinds:
1. Application of inference rules
  - Legitimate (sound) generation of new sentences from old
  - Proof = a sequence of inference rule applications
      Can use inference rules as operators in a standard search alg.
  - Typically require translation of sentences into a normal form


2. Model checking
  - truth table enumeration (always exponential in n)
  - improved backtracking, e.g., Davis–Putnam–Logemann–Loveland
  - heuristic search in model space (sound but incomplete)
    e.g., min-conflicts-like hill-climbing algorithms


## Resolution
**CNF—universal**:
- Conjunctive Normal Form
- conjunction of disjunctions of literals

Resolution inference rule (for CNF): complete for propositional logic

$$
\frac{J_1 ∨ ... ∨ J_k \ \  m_1 ∨ ... ∨ m_n}{J_1 ∨ ... ∨ J_{i-1} ∨ J_{i+1} ∨ ... ∨ J_n ∨ m_1 ∨ ... ∨ m_{j-1} ∨ m_{j+1} ∨ ... ∨ m_n}
$$

where $J_i$ and $m_j$ are complementary literals.

Resolution is sound and complete for propositional logic

## Conversion to CNF


$B_{1,1} ⇔(P_{1,2} ∨ P_{2,1})

1. Eliminate ⇔, replacing $α ⇔ β$ with $(α ⇒ β) ∧ (β ⇒ α)$.\
  $(B_{1,1} ⇒ (P_{1,2} ∨ P_{2,1})) ∧ ((P_{1,2} ∨ P_{2,1}) ⇒ B_{1,1})$
2. Eliminate ⇒, replacing α ⇒ β with ¬α ∨β.\
  $(¬B_{1,1} ∨ P_{1,2} ∨ P_{2,1}) ∧ (¬(P_{1,2} ∨ P_{2,1}) ∨ B_{1,1})$
3. Move $¬$ inwards using de Morgan’s rules and double-negation:\
  $(¬B_{1,1} ∨ P_{1,2} ∨ P_{2,1}) ∧ ((¬P_{1,2} ∧ ¬P_{2,1}) ∨ B_{1,1})$
4. Apply distributivity law (∨ over ∧) and flatten:\
  $(¬B_{1,1} ∨ P_{1,2} ∨ P_{2,1}) ∧ (¬P_{1,2} ∨ B_{1,1}) ∧ (¬P_{2,1} ∨ B_{1,1})$


**Resolution algorithm**
```
function PL-Resolution(KB, α) returns true or false
  inputs: KB, the knowledge base, a sentence in propositional logic
        α, the query, a sentence in propositional logic
  clauses ← the set of clauses in the CNF representation of KB ∧ ¬α
  new ← { }
  loop do
    for each Ci, Cj in clauses do
      resolvents ← PL-Resol ve(Ci,Cj)
      if resolvents contains the empty clause then return true 
      new ← new∪ resolvents
    if new ⊆ clauses then return false 
    clauses ← clauses ∪ new
```

## Forward and backward chaining


These algorithms are very natural and run in linear time

### Forward chaining

**Idea**: fire any rule whose premises are satisfied in the KB, add its conclusion to the KB, until query is found


**Forward chaining algorithm**
```
function PL-FC-Entails?(KB, q) returns true or false
  inputs: KB, the knowledge base, a set of propositional Horn clauses
    q, the query, a proposition symbol
  local variables: count, a table, indexed by clause, initially the number of premises
    inferred, a table, indexed by symbol, each entry initially false
    agenda, a list of symbols, initially the symbols known in KB

while agenda is not empty do 
  p← Pop(agenda) 
  unless inferred[p] do
    Inferred[p]← true
    for each Horn clause c in whose premise p appears do
      decrement count[c]
      if count[c] = 0 then do
        if Head[c] = q then return true
        Push(Head[c],agenda)
  return false
```


**Proof of completeness**
FC derives every atomic sentence that is entailed by KB
1. FC reaches a fixed point where no new atomic sentences are derived
2. Consider the final state as a model m, assigning true/false to symbols
3. Every clause in the original KB is true in m
    Proof: Suppose a clause $a_1 ∧ ... ∧ a_k ⇒ b$ is false in $m$ 
    Then $a_1 ∧ ... ∧ a_k$ is true in $m$ and $b$ is false in $m$
    Therefore the algorithm has not reached a fixed point!
4. Hence $m$ is a model of $KB$
5. If $KB |= q, q$ is true in every model of $KB$, including $m$

General idea: construct any model of $KB$ by sound inference, check $α$


### Backward chaining

Idea: work backwards from the query q: 
    to prove q by BC,
      check if q is known already, or
      prove by BC all premises of some rule concluding q

Avoid loops: check if new subgoal is already on the goal stack 

Avoid repeated work: check if new subgoal
1) has already been proved true, or
2) has already failed



### Forward vs. backward chaining

Forward Chaining is data-driven, cf. automatic, unconscious processing, 
  * example: object recognition, routine decisions

May dolots of work that is irrelevant to the goal

BC is goal-driven, appropriate for problem-solving,
  * example: Where are my keys? How do I get into a PhD program?

Complexity of BC can be much less than linear in size of $KB$

### Effective Propositional Model Checking

Davis–Putnam algorithm with three improvements over TT-ENTAILS
• Early termination: detect T/F 
• Pure symbol heuristic: same sign in all clauses
• Unit Clause heuristic: clause with one literal

Local search algorithms such as hill-climbing & simulated annealing.

In recent years, there has been a great deal of experimentation to find a good balance between greediness and randomness.

WALKSAT: On every iteration, the algorithm picks an unsatisfied clause and picks a symbol in the clause to flip.

# Summary

Logical agents apply inference to a knowledge base to derive new information and make decisions

Basic concepts of logic:
– syntax: formal structure of sentences
– semantics: truth of sentences wrt models
– entailment: necessary truth of one sentence given another
– inference: deriving sentences from other sentences
– soundess: derivations produce only entailed sentences
– completeness: derivations can produce all entailed sentences

Wumpus world requires the ability to represent partial and negated information, reason by cases, etc

Forward, backward chaining are linear-time, complete for Horn clauses 

Resolution is complete for propositional logic. 

Propositional logic lacks expressive power

Local search methods (WALKSAT) find solutions (sound but not complete).










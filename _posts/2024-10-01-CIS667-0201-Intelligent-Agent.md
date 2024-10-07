# Intelligent Agent:

## Agent and Environment

An **agent** is any entity that can be understood as **perceiving its environment** through sensors and **acting on that environment** through actuators. This broad definition includes various types of agents such as humans, robots, software agents (softbots), and even simple devices like thermostats.

The agent’s behavior is described by an **agent function**, which maps a sequence of percepts (i.e., the history of what the agent has perceived) to an action:

$$
f: P^* \to A
$$

Where:
- $ P^* $ represents the set of all possible percept histories.
- $ A $ represents the set of actions the agent can take.

In practice, the **agent program** is the software that runs on the agent's **physical architecture**, producing the function \( f \), which determines the agent’s actions based on its percepts.

## The Concept of Rationality

A **rational agent** is one that **does the right thing**. But what does "doing the right thing" actually mean?

In AI, the concept of "right" often follows the philosophical notion of **consequentialism**. According to consequentialism, the correctness of an agent’s actions is determined by the **consequences** of those actions. When an agent interacts with an environment, it generates a sequence of actions based on the percepts it receives, which in turn causes the environment to go through a series of states. If this sequence of states is desirable, the agent has performed well.

This idea of **desirability** is quantified by a **performance measure** that evaluates the sequence of states produced by the agent’s actions in the environment.

### Rationality
An agent's rationality at any given time is influenced by four factors:
- The **performance measure** that defines success.
- The agent’s **prior knowledge** about the environment.
- The **actions** that the agent is capable of performing.
- The agent’s **percept sequence** to date.

**Definition of a rational agent:**\
A rational agent is one that, for each possible percept sequence, selects the action that is expected to **maximize** its performance measure, given the evidence from the percept sequence and the built-in knowledge the agent possesses.

Thus, a rational agent always chooses the action that maximizes the expected value of the performance measure, based on the percept sequence up to that point.

### Omniscience, Learning, and Autonomy

**Omniscience:**\
An **omniscient** agent would know the actual outcomes of all its actions and act accordingly. However, omniscience is impossible in reality. Rationality is different from omniscience: rationality focuses on **maximizing expected performance**, while omniscience would require **perfect** knowledge. Since rational decisions are based on the percept sequence to date, omniscience is not required for rationality.

**Learning:**\
A rational agent must engage in **information gathering** before acting. This involves performing actions to modify future percepts, and it is crucial for rational behavior. A rational agent should not only gather information but also **learn** from what it perceives. While the agent may start with some prior knowledge, its learning should allow it to modify and improve its understanding of the environment over time.

In cases where the environment is entirely known and predictable, the agent may not need to perceive or learn—it can act optimally based on prior knowledge alone. However, this is rarely the case.

**Autonomy:**\
An agent that relies heavily on its designer's prior knowledge, rather than on its own perceptions and learning processes, is said to lack **autonomy**. A truly rational agent should be **autonomous**, learning from its environment to compensate for incomplete or inaccurate prior knowledge. This allows the agent to adapt and make better decisions over time.

## The Nature of Environments

In AI, **task environments** represent the "problems" that rational agents are designed to solve. The task environment directly influences the appropriate design of an agent program. By specifying the environment, performance measures, actuators, and sensors, we can better understand how to structure an agent for a particular task.

### Specifying the Task Environment

When designing an agent, the first step is to specify the task environment in detail, which involves defining the **performance measure**, the **environment**, the agent's **actuators**, and **sensors**. This specification is often referred to using the acronym **PEAS** (Performance, Environment, Actuators, Sensors).

#### Performance Measure
The **performance measure** defines the criteria for success. For instance, when designing an automated taxi, performance could be evaluated by factors like safety, reaching the destination, minimizing fuel consumption, adhering to traffic laws, maximizing passenger comfort, and generating profits. Often, multiple objectives may conflict, requiring tradeoffs between different goals.

#### Environment
The **environment** refers to the external context in which the agent operates. For example, an automated taxi's environment could include roads, traffic conditions, pedestrians, weather, and other unpredictable elements.

#### Actuators
**Actuators** are the mechanisms through which the agent interacts with its environment. For a robot or automated taxi, actuators might include components like the steering, accelerator, brakes, or horn, which allow the agent to control its movement and actions.

#### Sensors
**Sensors** allow the agent to perceive its environment. These could be video cameras, accelerometers, GPS, or any other input devices that collect data from the surroundings.

*Case Examples:*
1. **Automated Taxi Design:**
   - **Performance measure:** Safety, reaching the destination, profitability, compliance with laws, comfort, etc.
   - **Environment:** US streets, highways, traffic, pedestrians, weather conditions.
   - **Actuators:** Steering, accelerator, brake, horn, display, speakers.
   - **Sensors:** Video cameras, accelerometers, engine sensors, GPS, gauges.

2. **Internet Shopping Agent:**
   - **Performance measure:** Price, quality, appropriateness, efficiency, user satisfaction.
   - **Environment:** Current and future web pages, online vendors, shipping options.
   - **Actuators:** Displaying information to users, following URLs, filling out forms.
   - **Sensors:** HTML pages (including text, images, scripts, etc.). 

## Properties of Task Environments

The variety of task environments in AI is vast, but they can be categorized along several key dimensions that help determine the appropriate design for an agent and the best techniques for agent implementation. Below are the key properties of task environments:

1. Fully observable vs. partially observable
2. Single-agent vs. multiagent
3. Deterministic vs. nondeterministic.
4. Episodic vs. sequential
5. Static vs. dynamic
6. Discrete vs. continuous
7. Known vs. unknown

### 1. Fully Observable vs. Partially Observable
- **Fully Observable:** An environment is fully observable if the agent's sensors can detect the complete state of the environment at any given time. This is advantageous because the agent does not need to maintain any internal state.
- **Partially Observable:** An environment is partially observable if the agent's sensors provide incomplete or noisy data. This could occur due to limitations in the sensors or because parts of the environment are hidden. For example, a vacuum cleaner might not know if another room is dirty without moving to it. An environment may also be **unobservable** if the agent has no sensors at all.

### 2. Single-Agent vs. Multiagent
- **Single-Agent:** A task environment involves only one agent acting independently, such as a puzzle-solving system.
- **Multiagent:** Multiple agents interact, each influencing the environment. For example, in a chess game, one agent’s success depends on the actions of the other. In such environments, agents might cooperate or compete, leading to different behaviors like communication or randomized actions to avoid predictability.

### 3. Deterministic vs. Nondeterministic (Stochastic)
- **Deterministic:** If the next state of the environment is entirely determined by the current state and the agent’s actions, the environment is deterministic. An agent in a deterministic environment can predict outcomes with certainty.
- **Nondeterministic:** If the environment's next state is uncertain, it is nondeterministic. In some cases, this involves randomness or probabilities, which is referred to as **stochastic** (i.e., explicitly dealing with probabilities). Nondeterminism requires the agent to handle uncertainty in its decision-making process.

### 4. Episodic vs. Sequential
- **Episodic:** In an episodic environment, an agent’s experiences are divided into separate, independent episodes. Each episode involves perceiving and acting, but actions in one episode do not affect future episodes. Many classification tasks fall into this category (e.g., identifying defective items on an assembly line).
- **Sequential:** In sequential environments, an agent's current decisions affect future outcomes. For example, chess and driving are sequential because short-term actions have long-term consequences. Sequential environments require the agent to consider future actions.

### 5. Static vs. Dynamic
- **Static:** In a static environment, the world remains unchanged while the agent deliberates. The agent does not need to keep track of time or the changing state of the environment while deciding on an action.
- **Dynamic:** A dynamic environment changes over time, and the agent must account for these changes while making decisions. For example, in driving, traffic and road conditions can change continuously. If the environment does not change, but the agent's performance score does (e.g., waiting too long reduces success), it is considered **semidynamic**.

### 6. Discrete vs. Continuous
- **Discrete:** An environment is discrete if there are a finite number of distinct states, percepts, and actions. Chess is an example of a discrete environment where the number of possible moves is countable.
- **Continuous:** A continuous environment has infinite states, actions, or percepts. For example, driving involves continuous control of steering angles, speed, and positioning, and the environment evolves over continuous time.

### 7. Known vs. Unknown
- **Known:** In a known environment, the outcomes of all possible actions are understood by the agent or its designer, even if the environment is not fully observable.
- **Unknown:** In an unknown environment, the agent must learn the consequences of its actions over time. Unknown environments require exploration and learning from experience.

### Example Scenarios

1. **Automated Taxi:**
   - **Fully observable or partially observable:** A taxi may not have full knowledge of other drivers' intentions.
   - **Single-agent or multiagent:** Multiple taxis or vehicles compete for road space, making this a multiagent environment.
   - **Deterministic or nondeterministic:** The environment is largely nondeterministic due to unpredictable elements like traffic and pedestrians.
   - **Sequential:** Each driving action (e.g., turning or braking) impacts future actions.
   - **Dynamic:** Traffic and road conditions change in real-time.
   - **Continuous:** The taxi’s movement and environment are continuous.
   - **Unknown:** The taxi may not know the effects of all actions in all situations.

2. **Internet Shopping Agent:**
   - **Partially observable:** It can only see the information available on websites, which might be incomplete.
   - **Single-agent:** The agent is operating in isolation, interacting only with websites.
   - **Nondeterministic:** Prices, availability, and shipping times may change unpredictably.
   - **Episodic:** The agent may complete one purchase without affecting future ones.
   - **Static:** The environment does not change while the agent is selecting items.
   - **Discrete:** The environment (websites, prices) is discrete in nature.
   - **Known:** The agent knows the rules of navigating websites and making purchases.
  
*Examples of task environments and their characteristics:*

| Task Environment      | Observable     | Agents   | Deterministic  | Episodic    | Static     | Discrete     |
|-----------------------|----------------|----------|----------------|-------------|------------|--------------|
| Crossword puzzle       | Fully          | Single   | Deterministic  | Sequential  | Static     | Discrete     |
| Chess with a clock     | Fully          | Multi    | Deterministic  | Sequential  | Semi       | Discrete     |
| Poker                  | Partially      | Multi    | Stochastic     | Sequential  | Static     | Discrete     |
| Backgammon             | Fully          | Multi    | Stochastic     | Sequential  | Static     | Discrete     |
| Taxi driving           | Partially      | Multi    | Stochastic     | Sequential  | Dynamic    | Continuous   |
| Medical diagnosis      | Partially      | Single   | Stochastic     | Sequential  | Dynamic    | Continuous   |
| Image analysis         | Fully          | Single   | Deterministic  | Episodic    | Semi       | Continuous   |
| Part-picking robot     | Partially      | Single   | Stochastic     | Episodic    | Dynamic    | Continuous   |
| Refinery controller    | Partially      | Single   | Stochastic     | Sequential  | Dynamic    | Continuous   |
| English tutor          | Partially      | Multi    | Stochastic     | Sequential  | Dynamic    | Discrete     |


### Hardest Task Environment
The most challenging environment is **partially observable, multiagent, nondeterministic, sequential, dynamic, continuous, and unknown**. Such environments require sophisticated strategies, learning, and real-time decision-making to handle uncertainty and interaction with other agents.

## Agent Types

In AI, **agent programs** take percepts from sensors as input and return actions to actuators. The key difference between the **agent program** and the **agent function** is that the agent program operates based on the current percept alone, while the agent function may depend on the entire percept history. If an agent’s actions need to consider the entire percept sequence, the agent must store and process previous percepts.

### Table-Driven Agents

Here’s an example of a simple agent program in pseudocode:

``` 
function TABLE-DRIVEN-AGENT(percept) returns an action
persistent: percepts, a sequence, initially empty
table, a table of actions, indexed by percept sequences, initially fully specified
append percept to the end of percepts
action←LOOKUP(percepts, table)
return action
```

The **TABLE-DRIVEN-AGENT** stores every percept it receives, indexing these percept sequences into a pre-specified table of actions. Each time it receives a new percept, it looks up the corresponding action in the table and executes it. 

While this approach works in principle, it is impractical for most real-world applications. The size of the lookup table becomes prohibitively large as the number of possible percepts and percept sequences grows. For example:
- An automated taxi would require a lookup table with over \(10^{600,000,000,000}\) entries for just an hour of driving based on its visual input.
- Even a relatively simple game like chess would require a lookup table with at least \(10^{150}\) entries—far more than the number of atoms in the observable universe (less than \(10^{80}\)).

Thus, this method fails because:
1. **Storage**: No physical system could store such a large table.
2. **Creation**: It is impossible for a designer to construct the table for every possible scenario.
3. **Learning**: The agent cannot reasonably learn all the required table entries from experience.

Despite this, the table-driven agent represents the desired agent function in theory. The challenge of AI is to create programs that achieve **rational behavior** efficiently, without relying on enormous tables of percept-action pairs.

### Types of Agent Programs

There are four basic kinds of agent programs, which are more practical and embody the principles of almost all intelligent systems:
- Simple reflex agents
- Model-based reflex agents
- Goal-based agents
- Utility-based agents

#### 1. Simple Reflex Agents

- **Definition**: Simple reflex agents select actions based solely on the current percept, ignoring any past percepts or history. These agents operate using a set of predefined **condition-action rules** (e.g., if a certain condition is perceived, then a specific action is taken). They do not store information about previous experiences and rely entirely on the immediate environment to make decisions.

- **Example**: A classic example is a **thermostat**, which adjusts the temperature based on the current room temperature without considering how long the room has been at that temperature.

- **Limitation**: Simple reflex agents are effective in **fully observable** environments where the agent has access to all relevant information needed to act. However, they perform poorly in environments that are **partially observable**, where the current percept alone is insufficient to make the best decision, as they lack memory of past states or knowledge of future consequences.

Despite their simplicity, these agents are useful in certain applications where the environment is relatively straightforward.

Here is the pseudocode for a **simple reflex agent**:

``` 
function SIMPLE-REFLEX-AGENT(percept) returns an action
    persistent: rules, a set of condition–action rules
    state ← INTERPRET-INPUT(percept)
    rule ← RULE-MATCH(state, rules)
    action ← rule.ACTION
    return action
```

In this psudocode:
- The agent uses the current **percept** to determine the **state** of the environment.
- It then matches the **state** with a predefined **rule** from a set of **condition-action** rules.
- The agent selects the **action** corresponding to the rule that matches the current state.
- Finally, the agent returns and performs the action.

This approach works well in scenarios where the environment is static and easily interpreted based on the current percept, but it becomes limited when more sophisticated reasoning or memory is required.

#### 2. Model-Based Reflex Agents

- **Definition**: Model-based reflex agents maintain an **internal state** that reflects the current state of the world, updated based on the agent’s percept history. This internal state allows the agent to infer the next state of the world by combining information about its actions and how the world changes over time. These agents use a **model of the world** to manage partial observability, maintaining a dynamic understanding of their environment.

- **Example**: A **robot vacuum cleaner** that keeps track of which areas of the room it has already cleaned. By maintaining an internal state, it avoids repeatedly cleaning the same spot.

- **Limitation**: While more effective than simple reflex agents in partially observable environments, model-based agents depend on the accuracy of their internal models. If the model of the world is incomplete or inaccurate, the agent may make suboptimal or incorrect decisions.

**Managing Partial Observability**

In a **partially observable** environment, the agent can’t always perceive the entire state of the world. To compensate for this, the agent keeps track of what it cannot currently observe by maintaining an **internal state**. This internal state represents an estimate of the current world state based on the agent's percept history and the model of how the world evolves over time.

To update the internal state, the agent needs two key components:
1. **Transition model**: Information about how the world changes in response to actions and external factors. For instance, when the agent turns the steering wheel of a car, the car turns accordingly, or when it rains, the camera might become obscured by raindrops.
2. **Sensor model**: Information about how the state of the world is reflected in the agent's percepts. For example, illuminated red lights in the car’s forward camera signal that the vehicle in front is braking.

Together, the **transition model** and **sensor model** help the agent maintain an accurate understanding of the world’s state, even when certain aspects are unobservable. Agents that use these models are known as **model-based agents**.

**Pseudocode for Model-Based Reflex Agent**

Here’s the pseudocode for a **model-based reflex agent**:

``` 
function MODEL-BASED-REFLEX-AGENT(percept) returns an action
    persistent: 
        state, the agent’s current conception of the world state
        transition model, a description of how the next state depends on the current state and action
        sensor model, a description of how the current world state is reflected in the agent’s percepts
        rules, a set of condition–action rules
        action, the most recent action, initially none
        
    state ← UPDATE-STATE(state, action, percept, transition model, sensor model)
    rule ← RULE-MATCH(state, rules)
    action ← rule.ACTION
    return action
```

### How It Works:
- **Internal state**: The agent’s conception of the world’s current state is updated with each new percept. The update process uses the agent’s **transition model** (how actions and the environment affect the world) and **sensor model** (how the world is reflected in the agent’s percepts).
- **Rule matching**: Once the internal state is updated, the agent applies its **condition-action rules** to determine which action to take next.
- **Action selection**: The agent selects the action based on the rule that matches the current state and executes it.

This structure allows the agent to handle environments that are only **partially observable**, enabling more sophisticated behavior than simple reflex agents. However, the agent’s effectiveness depends heavily on the accuracy of its models.

#### 3. Goal-Based Agents

- **Definition**: **Goal-based agents** make decisions not only by analyzing the current state of the environment but also by considering the **goals** they aim to achieve. These agents reason about which actions will best lead to their goals and select actions accordingly.
  
- **Example**: A **self-driving car** that selects routes to minimize travel time, ensuring safety and passenger comfort while navigating to a specific destination.
  
- **Limitation**: Goal-based agents require more **computational resources** since they need to evaluate future outcomes and plan actions to achieve their goals, making them less efficient than reflex agents in simple environments.

### How Goal-Based Agents Work

Merely understanding the **current state** of the environment isn’t always enough to determine the best action. For instance, at a road junction, a taxi can turn left, right, or go straight. The appropriate decision depends on the **goal**—where the taxi is trying to go. Thus, beyond just a description of the current state, a goal-based agent needs **goal information** that defines desirable situations (e.g., reaching a specific destination).

The agent can use this **goal information**, combined with a model of the world (similar to the model-based reflex agent), to evaluate different sequences of actions and select the ones that will achieve the goal. In some cases, achieving the goal may be simple, resulting from a single action. In other cases, the agent must plan more complex, multi-step sequences of actions, such as navigating through a series of roads to reach a destination.

**Advantages of Goal-Based Agents**
Although goal-based agents may seem less efficient in the short term because they require planning and reasoning, they offer significant advantages:
- **Flexibility**: The agent’s knowledge is represented explicitly, so its behavior can be easily modified by updating its goals. For example, if the taxi needs to go to a different destination, the goal-based agent can simply update the goal to reflect the new destination, and the agent will adjust its behavior accordingly. 
- In contrast, a reflex agent would need entirely new condition-action rules to handle a new destination.

**Pseudocode for a Goal-Based Agent**

``` 
function GOAL-BASED-AGENT(percept) returns an action
    persistent: 
        state, the agent’s current conception of the world state
        goal, a description of the desired goal
        transition model, a description of how actions affect the state
        sensor model, a description of how the state is reflected in percepts
        
    state ← UPDATE-STATE(state, percept, transition model, sensor model)
    
    if GOAL-ACHIEVED(state, goal) then
        return no-op
    else
        action ← PLAN-ACTION(state, goal, transition model)
        return action
```

**How It Works:**
- **State update**: The agent updates its understanding of the world based on new percepts and its internal models (transition and sensor models).
- **Goal check**: It checks whether the current state satisfies the goal.
- **Action planning**: If the goal hasn’t been achieved, the agent plans an action (or sequence of actions) that will help achieve the goal.
- **Action execution**: The chosen action is then executed, and the cycle repeats.

Goal-based agents offer greater flexibility and adaptability than reflex-based agents because they explicitly represent goals and can reason about future actions. This allows them to handle more complex environments where achieving a goal requires multi-step reasoning and planning. However, the tradeoff is the need for more computational resources to reason about potential future states and actions.

#### 4. Utility-Based Agents

- **Definition**: **Utility-based agents** aim to maximize a **utility function**, which quantifies the desirability of different states. This allows them to evaluate tradeoffs between different goals and select actions that maximize overall utility.
  
- **Example**: A **financial trading system** that seeks to maximize profit while minimizing risk by evaluating and selecting the best investment strategies.

- **Limitation**: Defining an appropriate **utility function** can be complex, and balancing competing goals (e.g., safety vs. speed) often requires sophisticated computations.

**Utility-Based Decision Making**\
While **goals** provide a binary distinction between "achieved" and "not achieved," they often fall short when it comes to making high-quality decisions in real-world environments. For instance, several different action sequences may get a taxi to its destination (achieving the goal), but some routes may be quicker, safer, or more cost-effective than others. In such situations, goals alone are insufficient to distinguish between better or worse outcomes.

To address this, **utility functions** are used to provide a more fine-grained comparison of different states. Utility functions measure how desirable a state is to the agent, allowing it to choose actions that maximize **happiness** or **satisfaction**—commonly referred to as **utility** in scientific terms.

**Utility Function and Performance:**\
An agent’s **utility function** is an internal representation of the performance measure. As long as the utility function aligns with the external performance measure, the agent will behave **rationally** by selecting actions that maximize utility, thus performing well by external standards.

**Utility in Decision-Making Under Uncertainty:**

Utility-based agents are particularly useful when:
1. **Conflicting goals** need to be balanced, such as optimizing for speed and safety at the same time.
2. There are multiple goals, but none can be achieved with certainty. In such cases, the utility function helps the agent weigh the **likelihood of success** against the **importance of each goal**.

In real-world environments where **partial observability** and **nondeterminism** are common, decision-making often involves uncertainty. A **rational utility-based agent** selects the action that maximizes the **expected utility** of the possible outcomes. This expected utility is the average utility value of the outcomes, weighted by their probabilities. 

**Pseudocode for a Utility-Based Agent:**
``` 
function UTILITY-BASED-AGENT(percept) returns an action
    persistent:
        state, the agent’s current conception of the world state
        utility function, a measure of how desirable each state is
        transition model, a description of how actions affect the state
        sensor model, a description of how the state is reflected in percepts

    state ← UPDATE-STATE(state, percept, transition model, sensor model)
    
    action ← CHOOSE-ACTION(state, utility function, transition model)
    
    return action
```

**How It Works:**
- **State update**: The agent updates its internal model of the world based on the current percept.
- **Action selection**: The agent chooses the action that maximizes the **expected utility** of the outcome, given the transition model and utility function.
- **Utility optimization**: The agent evaluates different actions by calculating their potential impact on the utility function, considering tradeoffs between conflicting goals or uncertain outcomes.

**Example: Self-Driving Car**
Consider a self-driving car that must choose a route to reach its destination. Simply getting to the destination (the goal) may not be enough; the car must balance speed, safety, passenger comfort, and fuel efficiency. A **utility function** could assign a score to each possible state (i.e., each route), allowing the car to choose the route that maximizes its overall utility, taking into account tradeoffs like faster but riskier routes versus slower but safer ones.

**Advantages of Utility-Based Agents**
- **Flexible decision-making**: By using utility functions, these agents can handle multiple and conflicting goals, such as maximizing profits while minimizing risk in financial trading systems.
- **Rational behavior under uncertainty**: These agents can make rational decisions even when the outcome of actions is uncertain, thanks to expected utility calculations.
- **General-purpose algorithms**: Utility-based agents can use a general-purpose decision-making algorithm, as the utility function abstracts away the specifics of the problem.

**Limitations**
- **Complex utility functions**: Defining and designing an appropriate utility function that correctly represents the agent’s performance objectives can be difficult.
- **High computational cost**: Weighing tradeoffs between different goals and evaluating all potential outcomes can require complex calculations, especially in dynamic, uncertain environments.

**utility-based agents** are highly versatile and can handle complex decision-making scenarios by optimizing actions based on a utility function. This capability makes them well-suited for environments where tradeoffs and uncertainty are prevalent, but the challenge lies in defining the utility function and managing the computational complexity involved.


## Summarized key points:

### **Agent and Environment**
- An **agent** perceives its environment through **sensors** and acts upon it using **actuators**.
- The agent's actions are determined by an **agent function**, which maps its percept sequence to an action, often implemented via an **agent program**.

### **Rationality**
- A **rational agent** is one that chooses actions expected to maximize its **performance measure**, given its percept sequence and built-in knowledge.
- Rational agents differ from omniscient agents, as they make decisions based on expected outcomes, not perfect foresight.
- **Learning** and **autonomy** allow agents to improve performance by gathering information from their environment and adjusting actions accordingly.

### **Task Environment**
The design of an agent depends on its **task environment**, often characterized using the PEAS framework:
- **Performance Measure**: The criteria for success.
- **Environment**: The external world in which the agent operates.
- **Actuators**: Mechanisms that allow the agent to act.
- **Sensors**: Tools for perceiving the environment.

Task environments can vary across several dimensions:
1. **Fully Observable vs. Partially Observable**: Whether the agent can fully observe the environment at any moment.
2. **Single-Agent vs. Multiagent**: Whether other agents influence the task environment.
3. **Deterministic vs. Nondeterministic**: Whether actions lead to predictable outcomes.
4. **Episodic vs. Sequential**: Whether each task episode is independent or dependent on previous actions.
5. **Static vs. Dynamic**: Whether the environment changes while the agent deliberates.
6. **Discrete vs. Continuous**: Whether the states, actions, and percepts are countable or not.
7. **Known vs. Unknown**: Whether the agent knows the outcomes of all actions in advance.

### **Agent Types**
Different types of agent programs are used to implement intelligent agents:

1. **Simple Reflex Agents**:
   - Act based on the current percept using condition-action rules.
   - Effective in fully observable environments but limited in partially observable ones.

2. **Model-Based Reflex Agents**:
   - Maintain an internal state to handle partial observability.
   - Use a **transition model** (how actions affect the state) and a **sensor model** (how percepts reflect the state).

3. **Goal-Based Agents**:
   - Make decisions by considering future goals, planning sequences of actions to achieve desired outcomes.
   - More flexible and adaptive, suitable for complex tasks requiring multi-step reasoning.

4. **Utility-Based Agents**:
   - Aim to maximize a **utility function**, which quantifies the desirability of different states.
   - Handle tradeoffs and uncertainty, making rational decisions even when outcomes are uncertain.

## **Conclusion**
Intelligent agents must interact effectively with their environments to achieve rationality. Depending on the complexity and nature of the environment, different agent types are suited to different tasks. For highly dynamic and uncertain environments, utility-based agents are most versatile but computationally expensive. For simpler tasks, reflex-based agents can suffice.

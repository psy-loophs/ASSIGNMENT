============================================================
                    ARTIFICIAL INTELLIGENCE
                       ASSIGNMENT
============================================================


PART A - SHORT QUESTIONS
========================


1. WHAT IS ARTIFICIAL INTELLIGENCE?

Artificial Intelligence (AI) is the field of computer science that makes
machines capable of performing tasks that normally require human
intelligence.

It includes:
- Reasoning
- Learning from experience
- Understanding language
- Perceiving the environment
- Decision making

Definition:
AI is the study and design of intelligent agents that perceive their
environment and take actions to maximize their chances of achieving
their goals.


2. LIST ANY TWO UNINFORMED SEARCH STRATEGIES.

Uninformed search, also called blind search, searches without using
additional information about the distance to the goal.

Examples:
1. Breadth First Search (BFS)
2. Depth First Search (DFS)
3. Uniform Cost Search (UCS)
4. Depth Limited Search (DLS)
5. Iterative Deepening DFS (IDDFS)


3. DESCRIBE THE STRUCTURE OF AN INTELLIGENT AGENT.

An intelligent agent consists of:

Agent = Architecture + Agent Program

Components:

- Sensors:
  Perceive the environment.
  Examples: Camera, keyboard, microphone.

- Actuators:
  Act on the environment.
  Examples: Motors, screen, speaker.

- Agent Function:
  Maps a percept sequence to an action.

- Agent Program:
  Implements the agent function on the agent's architecture.

- Percept History / Knowledge Base:
  Stores information about previous percepts and knowledge.

Basic flow:

Environment
     |
     v
  Sensors
     |
     v
  Percepts
     |
     v
Agent Program
     |
     v
  Decision
     |
     v
 Actuators
     |
     v
Environment


4. EXPLAIN BRIEFLY SEARCH IN AI.

Search in AI is the process of finding a sequence of actions that
transforms an initial state into a goal state through a state space.

Main components of a search problem:

1. Initial State
2. Actions
3. Transition Model
4. Goal Test
5. Path Cost

A search algorithm explores the state-space tree or graph to find a
solution.


5. BRIEFLY EXPLAIN PROPOSITIONAL LOGIC WITH AN EXAMPLE.

Propositional logic is a type of logic that deals with propositions
which can have only two possible values:

- True
- False

Propositions can be connected using logical connectives such as:

- AND (^)
- OR (v)
- NOT (¬)
- Implication (->)
- Biconditional (<->)

Example:

P: It is raining.
Q: The road is wet.

Sentence:

P -> Q

Meaning:

If it is raining, then the road is wet.

If P is True, then Q must be True according to this rule.

Propositional logic can be used to represent knowledge and perform
logical inference.


6. DISCUSS THE USE OF HEURISTIC IN INFORMED SEARCH.

A heuristic is a function h(n) that estimates the cost from a node
n to the goal.

It is used in informed search to guide the search towards promising
nodes.

Uses of heuristic:

- Makes the search more efficient.
- Helps prioritize promising nodes.
- Reduces unnecessary exploration.
- Helps find the goal faster.

In algorithms such as Greedy Best First Search and A*, the heuristic
helps decide which node should be explored next.

For A*:

    f(n) = g(n) + h(n)

Where:

g(n) = Actual cost from the start node to n.
h(n) = Estimated cost from n to the goal.
f(n) = Total estimated cost.

A* is optimal when the heuristic is admissible, meaning it never
overestimates the actual cost to the goal.



============================================================
PART B
============================================================


7. ROLE OF INTELLIGENT AGENTS IN AI.

An intelligent agent is a central concept in AI. It perceives its
environment and takes actions to achieve its objectives.

Roles of intelligent agents:

- Provides a framework to model intelligent behaviour.
- Acts autonomously.
- Perceives and interacts with the environment.
- Forms the basis for problem solving.
- Used in robotics and software assistants.
- Supports different levels of intelligence, from simple reflex
  agents to learning agents.


8. DIFFERENTIATE BETWEEN INFORMED AND UNINFORMED SEARCH.

+----------------+----------------------------+----------------------------+
| Feature        | Uninformed Search         | Informed Search            |
+----------------+----------------------------+----------------------------+
| Knowledge      | No goal-distance          | Uses heuristic h(n)        |
|                | information               |                            |
| Efficiency     | May expand many nodes     | More directed and          |
|                |                            | generally efficient       |
| Examples       | BFS, DFS, UCS             | Best First, A*,            |
|                |                            | Hill Climbing              |
| Guidance       | No heuristic guidance     | Uses heuristic information |
+----------------+----------------------------+----------------------------+


9. BEST FIRST SEARCH ALGORITHM.

Best First Search selects the most promising node according to a
heuristic function.

Algorithm:

    function BEST-FIRST-SEARCH(problem):

        open = priority queue ordered by h(n)
        open.add(initial state)
        closed = empty set

        while open is not empty:

            n = open.pop()       // lowest h(n)

            if GoalTest(n):
                return n

            add n to closed

            for each successor of n:

                if successor is not in closed
                   and successor is not in open:

                    open.add(successor)
                    using h(successor)

        return failure


10. DEPTH FIRST SEARCH ALGORITHM.

Depth First Search (DFS) explores one branch as deeply as possible
before backtracking.

Algorithm:

    function DFS(problem):

        stack.push(initial state)
        visited = {initial}

        while stack is not empty:

            node = stack.pop()

            if GoalTest(node):
                return node

            for child in reverse(Expand(node)):

                if child is not in visited:

                    visited.add(child)
                    stack.push(child)

        return failure

DFS uses a LIFO (Last In, First Out) stack.

Advantages:
- Uses less memory.
- Can reach a deep solution quickly.

Disadvantage:
- Can get stuck exploring a deep path.


11. HILL CLIMBING SEARCH ALGORITHM.

Hill Climbing is a local search algorithm that continuously moves
towards a better neighbouring state.

Algorithm:

    function HILL-CLIMBING(problem):

        current = initial state

        loop:

            neighbor = highest valued successor of current

            if neighbor.value <= current.value:
                return current

            current = neighbor

Hill Climbing keeps moving to a better neighbouring state until no
better neighbour is available.



============================================================
PART C - DETAILED QUESTIONS
============================================================


12(A). BFS TO REACH GOAL STATE.

Breadth First Search (BFS) explores nodes level by level.

It uses a FIFO (First In, First Out) queue.

Example:

            S
           / \
          A   B
         / \   \
        C   D   G

Start State: S
Goal State: G

Traversal order:

    S -> A -> B -> C -> D -> G

Steps:

1. Start with S.
2. Visit S and add A and B to the queue.
3. Visit A and add C and D.
4. Visit B and add G.
5. Visit C.
6. Visit D.
7. Visit G and reach the goal.

BFS guarantees the shortest path in an unweighted graph.

Completeness: Yes.


12(B). A* INFORMED SEARCH.

A* is an informed search algorithm that uses both the actual cost
and estimated cost.

Formula:

    f(n) = g(n) + h(n)

Where:

g(n) = Actual cost from the start to node n.
h(n) = Estimated cost from node n to the goal.
f(n) = Total estimated cost through node n.

A* expands the node with the lowest f(n) value.

Example:

A* can be used for path finding where there are obstacles.

It evaluates possible paths, calculates f(n) for the nodes, and
selects the node with the lowest estimated total cost.

A* is optimal if the heuristic is admissible, meaning the heuristic
never overestimates the actual cost to reach the goal.


13(A). PREDICATE LOGIC - "ALL HUMANS ARE MORTAL".

The statement "All humans are mortal" can be represented using
First Order Logic as:

    ∀x (Human(x) -> Mortal(x))

If we know:

    Human(Socrates)

Then we can infer:

    Mortal(Socrates)

This inference is based on Modus Ponens.


13(B). PROPOSITIONAL LOGIC FOR KNOWLEDGE REPRESENTATION.

A Knowledge Base (KB) contains facts represented as propositions.

Example:

    P = Battery Charged
    Q = Car Starts

Rule:

    P -> Q

Fact:

    P is True

Inference:

    Q is True

Therefore, the car starts.

Propositional logic is useful in expert systems and knowledge
representation.

Limitation:

It cannot easily represent objects and relationships between
objects like First Order Logic can.


14(A). ROLE OF AI IN IMPROVING EDUCATION.

AI can improve education in several ways:

- Personalized learning:
  Adaptive learning platforms adjust the difficulty according to
  the student's performance.

- Intelligent Tutoring Systems:
  Provide personalized guidance and explanations.

- Automated grading:
  Helps evaluate answers and provide feedback.

- Chatbots:
  Help students solve doubts and answer questions.

- Content creation:
  AI can assist in creating learning materials.

- Identifying weak students:
  AI can analyze student performance and identify areas where
  students need improvement.


14(B). IMPACT OF AI ACROSS DIFFERENT FIELDS.

Healthcare:
- Disease diagnosis
- Medical imaging
- Drug discovery

Education:
- Personalized learning
- Automated administration
- Intelligent tutoring

Entertainment:
- Recommendation systems
- Game AI
- Generative AI for music and video


15(A). UTILITY-BASED AGENT IN PATH FINDING.

A utility-based agent chooses an action that maximizes the expected
utility instead of simply achieving a goal.

In path finding, the utility may consider:

- Distance
- Safety
- Fuel consumption
- Time
- Cost

The agent uses a utility function:

    U(state)

Example:

Suppose there are two paths to the destination.

Path 1:
- Short
- Risky

Path 2:
- Long
- Safe

A utility-based agent compares the overall utility of both paths
and selects the path with the highest utility.


15(B). GOAL-BASED AGENT VS MODEL-BASED AGENT.

Model-Based Agent:
- Maintains an internal model of the environment.
- Understands how the environment changes.
- Can work in partially observable environments.
- Example: An agent that remembers that a door is closed.

Goal-Based Agent:
- Uses information about a desired goal.
- Selects actions that help achieve the goal.
- Can search for a sequence of actions leading to the goal.
- More flexible than a simple reflex agent.

Main difference:

A model-based agent maintains an internal model of the world,
whereas a goal-based agent uses goals to decide which actions
should be taken.


16(A). UNIFORM COST SEARCH.

Uniform Cost Search (UCS) is an uninformed search algorithm.

It expands the node with the lowest path cost g(n).

It uses a priority queue ordered by:

    g(n)

Features:

- Uninformed search.
- Expands the lowest-cost node first.
- Complete.
- Optimal when step costs are appropriate.
- Useful for finding the cheapest route.

Example:

UCS can be used to find the cheapest route between two cities.

If all step costs are equal, UCS behaves like BFS.


16(B). SIMPLE REFLEX AGENT.

A Simple Reflex Agent acts only according to the current percept.

It uses condition-action rules.

Example: Vacuum Cleaner Agent

    If percept = Dirty
        Action = Suck

    If percept = Clean
        Action = Move

Features:

- Uses current percept.
- Does not maintain memory.
- Uses condition-action rules.
- Works best in fully observable environments.


17(A). HILL CLIMBING - LOCAL AND GLOBAL OPTIMA.

Hill Climbing moves towards a better neighbouring state until it
reaches a peak.

Problems faced by Hill Climbing:

1. Local Maximum:
   A peak that is better than its neighbours but is not the global
   best solution.

   Solution:
   Random Restart.

2. Plateau:
   A flat area where neighbouring states have similar values.

   Solution:
   Random Walk.

3. Ridge:
   A narrow uphill path that can be difficult for the algorithm
   to follow.

Hill Climbing is used in optimization problems such as the
Travelling Salesman Problem (TSP).

Techniques such as Simulated Annealing can be used to escape local
optima and improve the chance of reaching a global optimum.


17(B). BEST FIRST SEARCH TO REACH GOAL.

Best First Search uses a heuristic to guide the search towards
the goal.

Example:

In navigation, the heuristic can be:

    h(n) = Straight-line distance to the destination

The algorithm expands the city that appears closest to the goal.

Advantages:
- Can reach the goal quickly.
- Uses heuristic information.

Disadvantage:
- Not always optimal.
- Can be misled by an inaccurate heuristic.


18(A). STRUCTURE OF AN INTELLIGENT AGENT.

The structure of an intelligent agent includes:

- Sensors
- Percepts
- Agent Program
- Agent Function
- Actuators
- Knowledge
- Learning Element

Basic structure:

        +-------------------+
        |  Intelligent      |
        |      Agent        |
        +-------------------+
          ^               |
          |               v
       Percepts        Actions
          |               |
       Sensors         Actuators
          ^               |
          |               v
        +-------------------+
        |    Environment   |
        +-------------------+

An intelligent agent perceives the environment through sensors,
processes the information, and performs actions using actuators.


18(B). LEARNING AGENT VS SIMPLE REFLEX AGENT.

+----------------------+----------------------------+
| Simple Reflex Agent | Learning Agent             |
+----------------------+----------------------------+
| Rule-based           | Learns from experience    |
| No memory            | Has learning capabilities |
| Uses current percept | Improves over time        |
| Cannot improve by    | Can improve performance   |
| itself               | through learning          |
| Example: Thermostat  | Example: Self-driving car |
+----------------------+----------------------------+

A learning agent generally contains:

- Performance element
- Learning element
- Critic
- Problem generator


19(A). DESIGN A SIMPLE INTELLIGENT AGENT FOR HOME AUTOMATION.

Goal:

Control lights, temperature, and home security.

Sensors:

- Temperature sensor
- Motion sensor
- Light sensor
- Smartphone input

Actuators:

- Lights
- Air conditioner
- Door locks
- Alarm

Working:

1. If motion is detected at night:
       Turn ON the light.

2. If temperature is greater than 25°C:
       Turn ON the AC.

3. If nobody is at home:
       Lock the doors.
       Activate the security system.

The system can initially work as a simple reflex agent using
condition-action rules.

It can later be extended into a learning agent that learns the
user's daily routines.


19(B). DESIGN A SIMPLE GOAL-BASED AGENT.

Example: Delivery Robot

Goal:

Reach location B.

Components:

- Model of the map
- Sensors such as GPS and camera
- Actuators such as wheels
- Goal state: Location B

Working:

1. The robot perceives its current position.
2. It identifies the goal location B.
3. It searches possible paths using algorithms such as BFS or A*.
4. It selects an appropriate path.
5. It executes the required actions.
6. If an obstacle is detected, it updates the path and replans.

The goal-based agent selects actions based on whether they help
achieve the desired goal.


============================================================
                         END
============================================================

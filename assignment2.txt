# ============================================================
# S3 AI ASSIGNMENT 1
# ============================================================


# 1. What is Artificial Intelligence?

Artificial Intelligence (AI) is the branch of computer science focused on building intelligent agents capable of perceiving their environment, reasoning, making rational decisions, and taking actions to achieve specific goals.


# 2. List any two uninformed search strategies.

* Breadth-First Search (BFS)
* Depth-First Search (DFS)

(Other uninformed search methods include Depth-Limited Search and Uniform Cost Search).


# 3. Describe the structure of an intelligent agent.

An intelligent agent perceives its environment through sensors and acts upon it using actuators.

* **Architecture:** The physical machinery or hardware (e.g., sensors, motors, processing unit).
* **Agent Program:** The software implementation or algorithm that maps percept inputs to appropriate actions.
* **Sensors & Actuators:** Sensors (e.g., cameras, motion detectors) gather environment data, while actuators (e.g., wheels, switches) execute physical actions.


# 4. Explain briefly search in Artificial Intelligence.

Search is a fundamental problem-solving process in AI where an agent evaluates sequences of actions to transition from an initial state to a desired goal state.

## Problem-Solving Cycle:

* **Goal Formulation:** Defining the target goal.
* **Problem Formulation:** Identifying states, actions, and step costs.
* **Search:** Finding a path of actions leading to the goal.
* **Execution:** Carrying out the selected action sequence.


# 5. Briefly explain propositional logic with an example.

Propositional logic (Boolean logic) is a formal logic system where statements (propositions) evaluate strictly to either True (T) or False (F).

* **Connectives:** Atomic propositions are combined using \neg (NOT), \wedge (AND), \vee (OR), \rightarrow (IMPLIES), and \leftrightarrow (BICONDITIONAL).

* **Example:**
  * Let P = "It is raining"
  * Let Q = "The ground is wet"
  * Compound Proposition (P \rightarrow Q): "If it is raining, then the ground is wet."


# 6. Discuss the use of heuristic in informed search.

In informed search, a heuristic function h(n) provides an estimated cost from the current node n to the goal node. Heuristics inject domain-specific knowledge to prioritize nodes that appear closer to the goal, drastically reducing search time and memory overhead compared to uninformed search.


# 7. Explain the role of intelligent agents in Artificial Intelligence.

Intelligent agents represent the central operational framework of AI. They autonomously observe environmental conditions, process information, make rational choices, and execute actions to achieve defined targets across real-world systems such as robotics, automated diagnosis, and smart environments.


# 8. Differentiate between informed and uninformed search.

| Feature | Uninformed (Blind) Search | Informed (Heuristic) Search |
|---|---|---|
| Domain Knowledge | Uses no extra information about goal proximity. | Uses heuristic estimates h(n) to guide search. |
| Efficiency | Can be slow and memory-intensive. | Generally faster and explores fewer nodes. |
| Algorithms | BFS, DFS, UCS | Best-First Search, Hill Climbing, A^* Search |


# 9. Write Best-First Search algorithm.

* Create an empty priority queue (Open list).
* Insert the start node into the priority queue.
* Remove the node with the lowest heuristic value h(n).
* Check if it is the goal node; if yes, stop and return the path.
* Otherwise, expand the node, evaluate h(n) for all child nodes, and insert them into the priority queue.
* Repeat steps 3–5 until the goal is found or the queue is empty.


# 10. Write Depth-First Search algorithm.

* Initialize a stack and push the start node.
* Create a visited set to track expanded nodes.
* Pop the top node from the stack.
* If it has not been visited, mark it as visited.
* Check if it is the goal node; if yes, terminate search.
* Generate unvisited child nodes and push them onto the stack.
* Backtrack when reaching a dead end.
* Repeat until the goal is found or the stack is empty.


# 11. Write Hill Climbing search algorithm.

* Evaluate the initial state.
* Set current state = initial state.
* Generate neighboring states.
* Compare neighboring states with the current state.
* If a neighbor provides a better heuristic score, update current state to that neighbor.
* Repeat step 3 from the new state.
* Stop when no neighbor is better than the current state.


# 12. (A) Breadth-First Search vs (B) A^* Search

* **BFS:** Explores search spaces level-by-level using a FIFO Queue. It guarantees the shortest path in unweighted graphs but has high space complexity O(b^d).

* **A^* Search:** Combines actual path cost g(n) and estimated heuristic cost h(n) using the evaluation function:
   
   
   It selects nodes with the lowest f(n) value, guaranteeing an optimal solution when h(n) is admissible.


# 13. Logic Representation

## (A) Predicate Logic for "All Humans are Mortal":

   

## (B) Knowledge Representation using Propositional Logic:

Encodes facts and rules as propositions.

* **Fact:** P ("Smoke detected")
* **Rule:** P \rightarrow Q ("If smoke detected, then trigger alarm")
* **Inference (Modus Ponens):** From P and P \rightarrow Q, deduce Q ("Trigger alarm").


# 14. Applications of AI

* **Education:** Adaptive learning software, automated essay grading, intelligent tutoring systems.
* **Healthcare:** Disease diagnosis, medical image processing, robotic surgery support.
* **Entertainment:** Content recommendations (e.g., Netflix, YouTube), AI non-player characters (NPCs) in gaming.


# 15. Goal-Based Agent vs Model-Based Reflex Agent

* **Model-Based Reflex Agent:** Maintains internal memory/state to track unobserved aspects of the world and acts via condition-action rules.
* **Goal-Based Agent:** Combines state tracking with explicit goal descriptions and search/planning algorithms to find action sequences that achieve the target goal.


# 16. Uniform Cost Search (UCS) vs Simple Reflex Agent

* **Uniform Cost Search (UCS):** Uninformed graph search strategy that expands the node with the lowest path cost g(n) using a priority queue, guaranteeing optimal paths in weighted graphs.
* **Simple Reflex Agent:** The simplest agent type; operates strictly on current percepts using IF-THEN rules without maintaining past history. (Example: Automatic room light controller).


# 17. Hill Climbing (Local Optima vs Global Optima)

* **Local Optima (Local Maximum):** A state better than all immediate neighbors but inferior to the overall best state. Hill Climbing can get trapped here because no local move improves the score.
* **Global Optima (Global Maximum):** The single best solution in the entire state space.


# 18. Compare Learning Agent with Simple Reflex Agent

| Property | Simple Reflex Agent | Learning Agent |
|---|---|---|
| Adaptability | Fixed condition-action rules. | Learns and adapts from feedback. |
| Memory | No memory of past states. | Stores knowledge to improve over time. |
| Components | Sensors, Rules, Actuators. | Performance element, Critic, Learning element, Problem generator. |


# 19. Design a Simple Intelligent Agent for Home Automation

## PEAS Description:

* **Performance Measure:** Energy efficiency, temperature/light comfort, safety.
* **Environment:** House rooms, ambient light level, temperature.
* **Actuators:** Smart relay switches, HVAC controllers, alarm buzzers.
* **Sensors:** Motion sensors, photodetectors, temperature sensors.

## Working Mechanism:

Motion sensors detect human presence, light sensors measure ambient light, and the agent program triggers smart switches to turn lights on/off automatically.


# ============================================================
# END OF ASSIGNMENT
# ============================================================

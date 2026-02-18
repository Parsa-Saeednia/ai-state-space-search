# AI State-Space Search

Implementation of classical uninformed and informed search algorithms applied to a constrained grid-based planning problem.  
This project was developed as part of the Artificial Intelligence course (Computer Engineering) at the University of Tehran.

## Overview

This project investigates **state-space search techniques** for solving a Sokoban-like planning problem with additional constraints such as **multiple movable boxes**, **walls**, and **portals**.

The environment is modeled as a deterministic search problem, and different search strategies are evaluated with respect to **solution optimality**, **runtime**, and **state-space efficiency**.

The primary goal of the project is to demonstrate correct **problem formulation**, **search algorithm implementation**, and **heuristic design**, rather than game development or graphical rendering.

## Project Orientation (For Reviewers)

This repository contains **algorithmic implementations and analysis of classical AI search methods**.
The graphical interface and environment logic were **provided as course skeleton code** and are not the focus.

If you are reviewing this project for technical evaluation, the most relevant files are:

- `notebook.ipynb` — **Search algorithm implementations and experiments**
- `report.ipynb` — **Theoretical analysis, heuristic design, and empirical discussion**

The GUI (`gui.py`) and environment (`game.py`) are included for completeness and visualization.


## Implemented Algorithms

### Uninformed Search
- **Breadth-First Search (BFS)**  
  Complete and optimal, but memory intensive.
- **Depth-First Search (DFS)**  
  Memory efficient but neither complete nor optimal for this problem.
- **Iterative Deepening Search (IDS)**  
  Combines DFS space efficiency with BFS optimality at the cost of additional runtime.

### Informed Search
- **A\***  
  Uses admissible and consistent heuristics to guarantee optimal solutions.
- **Weighted A\***  
  Accelerates search by scaling the heuristic function, trading optimality for speed.

  All informed search implementations follow the standard evaluation function  
f(n) = g(n) + w · h(n), where w = 1 corresponds to A* and w > 1 to Weighted A*.

## State-Space Formulation

- **State Representation**  
  Each state is defined by:
  - The player’s position
  - The positions of all boxes  
  This abstraction avoids storing the full grid map in every state and significantly reduces memory usage.

- **Actions**  
  Four deterministic actions are available: `U`, `D`, `L`, `R`, corresponding to player movement.

- **Transition Model**  
  State transitions respect:
  - Wall constraints
  - Box-pushing rules
  - Portal mechanics defined by the environment

- **Goal Test**  
  A state is considered terminal if all boxes are placed on their designated goal positions.

- **Cost Function**  
  All valid actions have uniform cost.

## Heuristic Design

Several heuristic strategies were designed and evaluated:

- **Naive heuristic**  
  Manhattan distances between the player, boxes, and goal positions.
- **Improved heuristics**
  - Distance to the nearest box
  - Aggregated distances from boxes to goals
  - Portal-aware distance estimation

The heuristic used for A\* is **admissible and consistent**, ensuring optimality.  
Alternative heuristics were intentionally tested to analyze performance trade-offs in **Weighted A\***.

Formal arguments for heuristic admissibility and consistency, as well as failure cases for naive heuristics, are discussed in detail in `report.ipynb`.


## Repository Structure


├── assets/              # Maps, music, and static game resources  
├── game.py              # Game environment and rules (provided skeleton)  
├── gui.py               # Visualization and rendering utilities (provided skeleton)  
├── notebook.ipynb       # Search algorithms and experimental evaluations  
├── report.ipynb         # Theoretical analysis and discussion  
└── README.md

## How to Run

1. Install Python 3.x  
2. Install required dependencies (if not already installed):

   pip install numpy

3. Open and run `notebook.ipynb` to:
   - Load problem instances
   - Execute different search algorithms
   - Compare performance and solution quality

Visualization utilities in `gui.py` may be used to observe solution paths.

## Experimental Analysis

Experimental results align with classical theoretical expectations:

- BFS produces optimal solutions but suffers from high memory usage.
- DFS performs well on small maps but is unreliable in complex environments.
- IDS guarantees optimality with better space efficiency than BFS at the cost of increased runtime.
- A\* finds optimal solutions efficiently when using admissible heuristics.
- Weighted A\* significantly improves speed while sacrificing optimality.

Detailed experimental analysis and comparisons are provided in `report.ipynb`.

## Authorship and Attribution

### Provided Skeleton Code
The following components were provided by the course instructors and teaching assistants:
- Game environment and rules (`game.py`)
- Visualization and GUI (`gui.py`)
- Map files and graphical/audio assets (`assets/`)

These components define the environment but do **not** implement any search logic.

### My Contributions
I implemented all algorithmic and analytical components of this project, including:
- State representation and abstraction
- Uninformed search algorithms (BFS, DFS, IDS)
- Informed search algorithms (A*, Weighted A*)
- Heuristic design (including portal-aware heuristics)
- Experimental evaluation and performance analysis
- Theoretical analysis of admissibility, consistency, and trade-offs

## License

This repository is released under the MIT License.

The license applies **only to my original code and documentation**.
Instructor-provided skeleton files and assets remain the intellectual property of their original authors and are included here solely for educational completeness.


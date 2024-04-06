# Maze Navigation Project

## CS 520 - GHOST IN THE MAZE

Following steps need to be performed to replicate the environment I am using on Miniconda:

1. Run the following on CLI (with miniconda installed) in the repo folder: conda env create -f environment.yml

2. Activate the created environment using: conda activate /Path/To/Your/env

## Summary

### Design and Algorithms
- **Object Oriented Approach:** Implemented in Python (v3.7) for flexibility in code maintenance and extension.
- **Maze Generation:** Random mazes generated using constraints, with solvability checked using Bi-directional Breadth-First Search for improved space complexity.
- **Ghosts:** Spawned based on rules, with movements triggered by specific conditions.
- **Agents:** Developed with varying strategies using search algorithms and additional intelligence.

### Agent Strategies
- **Agent 1:** Utilized BFS for path planning without considering ghost locations during execution.
- **Agent 2:** Similar to Agent 1 but replanned paths if blocked by ghosts.
- **Agent 3:** (**Pac-Man**) Employed a Monte Carlo approach, simulating agent movements to determine optimal paths.
- **Agent 4:** Improved upon Agent 3 by considering ghost regions and path weights.
- **Agent 5:** Modified to operate without information on ghosts within walls.

### Challenges Faced and Solutions
- **Computational Bottleneck:** Attempted multiprocessing and set limitations to mitigate endless simulations.
- **Agent Performance Analysis:** Evaluated agents' performance considering computational constraints and information availability.

### Code Breakdown
- **Maze Generation:** Automated pipeline for generating and storing mazes as CSV files.
    - **maze.py**: Generates random mazes with a 0.28 blocking rule, verifies maze correctness, and saves them as CSV files.
    - **bdbfs.py**: Utilizes Bi-Directional BFS to check if an optimal path exists between start and goal.
    - **csvops.py**: Facilitates CSV file creation based on matrices.

### Ghosts

- **ghost.py**: Defines the Ghost class, manages its position, and ensures reachable spawning.
    This code has the ghost class (for the ghost objects in the maze) which has necessary attributes
    like row and col indicating its position on the maze and methods like spawnGhost and
    moveGhost that spawn the ghost and move it respectively. The spawnGhost method makes
    use of the BD-BFS algorithm in **bdbfs.py** to check if the ghost is spawned in a location
    reachable from the agent.

- **Main:** Orchestrated agent runs on mazes, including ghost spawning and data storage.
    - **main.py**: Orchestrates maze and agent interactions, conducts simulations, and generates survivability statistics CSVs.
    - **csvops.py**: Supports CSV file loading for maze runs.


- **Agents:** Implemented classes and methods for various agent strategies, considering maze structure and ghost locations.
1. **Attributes**:
   - `row` and `col`: Indicate the position of an agent.
   - `name`: Indicates the type of the agent (e.g., agent1, agent2, etc.).
   - `heuristics`: A map storing the number of steps required for the agent to traverse from any node on a specific maze to the goal node. This attribute is calculated at the beginning of each run by invoking the `getBaseHeuristics` method. It utilizes the `calcHeuristics` method to determine optimal path lengths from each node to the goal node using a BD-BFS algorithm. The values in the `heuristics` map are used to plan paths effectively.

2. **Methods**:
   - `planPath`: Applies an A* algorithm to decide a path using the `heuristics` map available in the agent object. It returns a list of possible steps that can be taken to reach from the start to the goal node.
   - `isValidMove` and `createPath`: Helper methods used to assist in checking for only valid neighbors and creating a list for the planned path, respectively, within the `planPath` method.

- **Data Visualization:** Utilized pandas and matplotlib to plot survivability data for different agent strategies.
    - **main.py**: Utilizes colorama module for terminal printing of agent and ghost positions.
    - **data.py**: Employs pandas and matplotlib to plot survivability graphs for different numbers of ghost spawns.
    - **comparingAgents.py**: Uses pandas and matplotlib to create bar graphs comparing survivability of different agents.
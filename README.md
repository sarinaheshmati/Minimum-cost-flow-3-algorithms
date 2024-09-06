# Minimum Cost Flow - 3 Algorithms

This project implements three algorithms (Cycle Canceling, Successive Shortest Path, Capacity Scaling) to solve the **Minimum Cost Flow** problem.

## Problem Definition
The Minimum Cost Flow problem extends the maximum flow problem by associating a cost with each edge in addition to a capacity. The goal is to determine the flow through the network such that it satisfies flow constraints (capacity) while minimizing the total cost. This problem combines elements of both the **maximum flow** and **shortest path** problems.

Given a directed graph, each edge has:
- **Capacity**: the maximum flow that can pass through the edge.
- **Cost**: the cost incurred for each unit of flow.

The objective is to find the flow with minimum total cost, subject to the capacity limits.

## Algorithm 1: Cycle Canceling
This is the simplest approach to solving the problem. The algorithm works by:
1. Finding a **feasible flow** by solving a maximum flow problem.
2. Iteratively locating **negative cost cycles** in the residual network.
3. Augmenting flow along these cycles to reduce the overall cost.
4. The algorithm terminates when no negative cost cycles remain in the residual graph, which guarantees optimality due to the **Negative Cycle Optimality Condition**.

### Steps:
- Establish a feasible flow by solving a max-flow problem.
- Search for negative cost cycles in the residual network.
- Cancel negative cycles by augmenting flow along them.
- Repeat until no more negative cycles exist.

## Algorithm 2: Successive Shortest Path
This algorithm focuses on maintaining **optimality** at each step while striving for feasibility. It works by:
1. Keeping a **pseudoflow** that satisfies the capacity constraints but may violate the flow conservation constraints.
2. At each step, it sends flow from a node with **excess supply** to a node with **unfulfilled demand** along the shortest path in the residual network.
3. The algorithm terminates when the solution satisfies all flow conservation constraints.

### Key Concepts:
- **Pseudoflow**: A function that satisfies capacity constraints but not necessarily flow conservation.
- **Node imbalance**: A measure of excess or deficit at a node.
- **Shortest Path**: Used to transfer flow from nodes with excess to those with deficits efficiently.

## Algorithm 3: Capacity Scaling
An improvement over the successive shortest path algorithm, **Capacity Scaling** ensures that each flow augmentation is significant, reducing the total number of iterations:
1. The algorithm works in phases, each associated with a parameter ∆.
2. In each phase, it augments flows of size **∆** along shortest paths in the residual network.
3. After each phase, the value of ∆ is halved, and the process repeats.
4. When ∆ reaches 1, the solution is optimal.

### Improvements:
- Reduces the number of augmentations by ensuring each augmentation is sufficiently large.
- Enhances worst-case time complexity from **O(nU)** to **O(m log U)**, where **U** is the maximum edge capacity.

### Scaling Phases:
- The algorithm begins with a large ∆, gradually reducing it.
- Augmentation is performed along paths where all edges have residual capacity of at least ∆.
- The process continues until ∆ = 1, at which point the flow is optimal.

## Conclusion
This project showcases how different algorithms solve the Minimum Cost Flow problem, each improving on the others in terms of efficiency and complexity. While **Cycle Canceling** is intuitive, **Successive Shortest Path** ensures optimality at each step, and **Capacity Scaling** significantly improves performance by handling larger flow augmentations.

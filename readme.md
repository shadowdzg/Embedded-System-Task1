# Introduction

NetworkX is a Python library designed for the creation, manipulation, and study of the structure, dynamics, and functions of complex networks and graphs. In this task, you are required to implement a set of functions using the NetworkX library.

# Instructions

- Fork this project on GitHub and make sure your repository is public. Then, import the project into your IDE (e.g., PyCharm).
- You cannot change the signature or rename the functions provided in `task.py`.
- You cannot interact with your peers: work individually and do your best.
- The features to implement are organized into a series of sub-tasks.
- Implement the functions one at a time, strictly following the order of the sub-tasks. Do not read upcoming sub-tasks in advance.
- A sub-task is considered completed when you are confident that the required functionality has been correctly implemented.
- Each time you complete a sub-task, commit and push your code to your repository.
- At the end of the assignment, ensure that the entire project has been pushed to your GitHub repository.

# Graph Theory Fundamentals

A **graph** is a discrete mathematical structure used to model pairwise relations between objects.
- **Node (or Vertex)**: An individual object or entity in the network (e.g., a city, a person, a computer, a web page).
- **Edge (or Link)**: A connection between two nodes indicating an association or relationship between them (e.g., a road connecting two cities, a friendship between two people, a network cable).
- **Undirected Graph**: A graph where edges have no direction. If there is an edge between node A and node B, the connection is symmetric and bidirectional: traversing from A to B is equivalent to traversing from B to A.
- **Directed Graph**: A graph where edges have a defined direction (often represented as an arrow u -> v). The edge (u, v) means a one-way connection from source node u to target node v.

---

# Sub-tasks

Remember to read and implement the sub-tasks one at a time, strictly following the provided order. Do not proceed to the next sub-task until the current one is completed. Implement the required functions inside `task.py`.

---

## Sub-task 1 – Node Degrees

In an undirected graph, the **degree** of a node is the total number of edges connected (incident) to that node. It serves as a metric of local connectivity: nodes with higher degrees have more immediate connections within the network.

### Requirement

Implement the function:

```python
calculate_node_degrees(edges: list) -> dict
```

This function receives a list of undirected edges, where each edge is represented as a 2-element tuple or list `(u, v)` denoting a connection between node `u` and node `v`.

The function must construct an undirected graph using NetworkX and return a dictionary where each key is a node and its corresponding value is an integer representing the degree of that node. If the graph is empty (no edges), return an empty dictionary.

### Examples

```python id="nx_deg_1"
Input: edges = [("A", "B"), ("B", "C"), ("B", "D")]
Output: {"A": 1, "B": 3, "C": 1, "D": 1}
```

```python id="nx_deg_2"
Input: edges = [(1, 2), (2, 3), (3, 1)]
Output: {1: 2, 2: 2, 3: 2}
```

```python id="nx_deg_3"
Input: edges = [("X", "Y")]
Output: {"X": 1, "Y": 1}
```

---

## Sub-task 2 – Shortest Path

A **path** in a graph is a sequence of alternating nodes and edges that connects a sequence of vertices without repeating any nodes. The **shortest path** between two nodes is the path that traverses the minimum number of edges.

### Requirement

Implement the function:

```python
find_shortest_path(edges: list, source: str, target: str) -> list
```

This function receives:
- `edges`: a list of tuples `(u, v)` representing the undirected edges of the graph;
- `source`: the starting node (string);
- `target`: the destination node (string).

The function must build the graph and return the shortest path between `source` and `target` as an ordered list of nodes, starting with `source` and ending with `target`.

### Examples

```python id="nx_sp_1"
Input: edges = [("A", "B"), ("B", "C"), ("A", "C"), ("C", "D")], source = "A", target = "D"
Output: ["A", "C", "D"]
```

```python id="nx_sp_2"
Input: edges = [("X", "Y"), ("Y", "Z")], source = "X", target = "Z"
Output: ["X", "Y", "Z"]
```

```python id="nx_sp_3"
Input: edges = [("A", "B"), ("B", "C"), ("C", "D"), ("B", "D")], source = "A", target = "D"
Output: ["A", "B", "D"]
```

---

## Sub-task 3 – Number of Connected Components

A **connected component** of an undirected graph is a maximal subgraph in which every pair of nodes is connected to each other by at least one path, and no node in the component is connected to any node outside of it. A graph is considered *connected* if it consists of exactly one connected component. If a graph contains isolated islands of nodes with no links between the islands, each isolated island forms its own connected component.

### Requirement

Implement the function:

```python
count_connected_components(edges: list) -> int
```

This function receives a list of undirected edges `(u, v)` and returns an integer representing the total number of connected components present in the graph. If `edges` is empty, the function must return `0`.

### Examples

```python id="nx_cc_1"
Input: edges = [("A", "B"), ("B", "C"), ("D", "E")]
Output: 2
```

```python id="nx_cc_2"
Input: edges = [("A", "B"), ("B", "C"), ("C", "A")]
Output: 1
```

```python id="nx_cc_3"
Input: edges = [("A", "B"), ("C", "D"), ("E", "F")]
Output: 3
```

---

## Sub-task 4 – Topological Sort in a Directed Acyclic Graph (DAG)

A **Directed Acyclic Graph (DAG)** is a directed graph with no directed cycles. That is, it is impossible to start at any node v and follow a sequence of directed edges that eventually loops back to v.

A **topological sort** (or topological ordering) of a DAG is a linear ordering of its vertices such that for every directed edge from node u to node v (u -> v), node u comes before node v in the ordering. This operation is widely used in task scheduling, dependency resolution (such as package managers), and workflow execution.

### Requirement

Implement the function:

```python
compute_topological_sort(directed_edges: list) -> list
```

This function receives a list of directed edges `(u, v)`, where each edge represents a one-way dependency pointing from `u` to `v`.

The function must build a directed graph from the provided edges and return a valid topological ordering of the nodes as a Python list. If the list of edges is empty, return an empty list.

### Examples

```python id="nx_ts_1"
Input: directed_edges = [("A", "B"), ("B", "C")]
Output: ["A", "B", "C"]
```

```python id="nx_ts_2"
Input: directed_edges = [("Task1", "Task3"), ("Task2", "Task3"), ("Task3", "Task4")]
Output: ["Task1", "Task2", "Task3", "Task4"]
```

```python id="nx_ts_3"
Input: directed_edges = [("compile", "test"), ("test", "deploy")]
Output: ["compile", "test", "deploy"]
```

---

## Sub-task 5 – Average Clustering Coefficient

In network science, the **clustering coefficient** measures the degree to which nodes in a graph tend to cluster together. Evidence suggests that in most real-world networks (especially social networks), nodes tend to create tightly knit groups characterized by a relatively high density of ties (triangles).

For a single node, the clustering coefficient is the ratio of edges between its neighbors to the maximum possible number of edges between those neighbors. The **average clustering coefficient** of a graph is the mean of the clustering coefficients of all its nodes.

**C = (1 / |V|) Σᵥ∈V cᵥ**

where *cᵥ* is the local clustering coefficient of node *v*, and *|V|* is the number of vertices.

### Requirement

Implement the function:

```python
compute_average_clustering(edges: list) -> float
```

This function receives a list of undirected edges `(u, v)` and returns the average clustering coefficient of the graph as a `float`. If the graph has no nodes or edges, return `0.0`.

### Examples

```python id="nx_acc_1"
Input: edges = [("A", "B"), ("B", "C"), ("C", "A")]
Output: 1.0
```

```python id="nx_acc_2"
Input: edges = [("A", "B"), ("B", "C"), ("C", "D")]
Output: 0.0
```

```python id="nx_acc_3"
Input: edges = [("A", "B"), ("B", "C"), ("A", "C"), ("C", "D")]
Output: 0.5833333333333334
```

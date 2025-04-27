# Problem 1


## **Equivalent Resistance Using Graph Theory**


## **Motivation**

Calculating equivalent resistance through graph theory simplifies the analysis of complex electrical circuits. Instead of manually applying series and parallel rules repeatedly, we represent circuits as graphs where:
- **Nodes** represent junctions.
- **Edges** represent resistors, weighted by their resistance.

Graph theory provides an algorithmic framework that can automate the calculation, offering efficiency for large-scale and nested networks.

By understanding this relationship, engineers and scientists can design better electronic systems, predict network behavior, optimize electrical grids, and model biological and social networks where similar principles apply.

---

## **Theoretical Foundations**

### **Graph Representation of Circuits**

An electrical circuit can be viewed as an undirected graph $G(V, E)$ where:
- $V$ is a set of vertices (nodes or junctions).
- $E$ is a set of edges (resistors) with weights corresponding to resistance values.

### **Series Connection Rule**
If two resistors $R_1$ and $R_2$ are in series:

$$
R_{eq} = R_1 + R_2
$$

### **Parallel Connection Rule**
If two resistors $R_1$ and $R_2$ are in parallel:

$$
\frac{1}{R_{eq}} = \frac{1}{R_1} + \frac{1}{R_2}
$$

For $n$ resistors in parallel:

$$
\frac{1}{R_{eq}} = \sum_{i=1}^n \frac{1}{R_i}
$$

---

## **Option 1: Algorithm Description with Pseudocode**

### **Algorithm Overview**

The idea is to iteratively simplify the graph:
- Identify nodes with exactly two neighbors to apply series reduction.
- Detect parallel edges between the same pair of nodes and reduce them.
- Repeat the process until only two nodes remain (start and end nodes).

### **Detailed Pseudocode**

```pseudo
Algorithm EquivalentResistance(G, start_node, end_node):
    While number of nodes > 2:
        For each node v in G:
            If v has exactly two neighbors (u, w):
                Combine resistors in series:
                    New resistance = R(u-v) + R(v-w)
                Remove node v
                Connect u and w with the new resistance

        For each pair of nodes (u, w) with multiple edges:
            Combine resistors in parallel:
                New resistance = 1 / (sum of reciprocals of each resistance)
            Remove all multiple edges between u and w
            Add a single edge with the new resistance

    Return resistance between start_node and end_node
```

### **Handling Nested and Complex Combinations**
- Apply series and parallel detection in a loop.
- After each modification, check the updated graph.
- For graphs containing cycles (loops), careful detection and proper handling of cycles are necessary.

### **Special Cases**
- Dead-end nodes (nodes connected by only one edge) can often be ignored unless they are start or end nodes.
- Nodes part of multiple cycles might require more complex cycle reduction techniques.

---

## **Option 2: Full Python Implementation**

### **Python Code Using NetworkX**

```python
import networkx as nx

def equivalent_resistance(G, start_node, end_node):
    G = G.copy()
    while len(G.nodes) > 2:
        merged = False

        # Handle series connections
        for node in list(G.nodes):
            neighbors = list(G.neighbors(node))
            if len(neighbors) == 2 and node not in [start_node, end_node]:
                u, w = neighbors
                R1 = G.edges[node, u]['resistance']
                R2 = G.edges[node, w]['resistance']
                R_new = R1 + R2
                G.add_edge(u, w, resistance=R_new)
                G.remove_node(node)
                merged = True
                break

        if not merged:
            # Handle parallel edges
            to_merge = []
            for u, v in G.edges:
                if G.number_of_edges(u, v) > 1:
                    to_merge.append((u, v))
            for u, v in set(to_merge):
                parallel_edges = G.get_edge_data(u, v)
                resistances = [data['resistance'] for key, data in parallel_edges.items()]
                R_parallel = 1 / sum(1/R for R in resistances)
                G.remove_edges_from(list(G.edges(u, v)))
                G.add_edge(u, v, resistance=R_parallel)

    return G.edges[start_node, end_node]['resistance']

# Example Circuit
G = nx.MultiGraph()
G.add_edge('A', 'B', resistance=5)
G.add_edge('B', 'C', resistance=10)
G.add_edge('A', 'C', resistance=20)

result = equivalent_resistance(G, 'A', 'C')
print(f"Equivalent Resistance: {result:.2f} ohms")
```

---

## **Testing the Algorithm on Examples**

### **Example 1: Simple Series**
- Two resistors 5 Ω and 10 Ω in series.
- Expected:

$$
R_{eq} = 5 + 10 = 15\,\Omega
$$

### **Example 2: Simple Parallel**
- Two resistors 10 Ω and 20 Ω in parallel.
- Expected:

$$
\frac{1}{R_{eq}} = \frac{1}{10} + \frac{1}{20} \Rightarrow R_{eq} \approx 6.67\,\Omega
$$

### **Example 3: Nested Series and Parallel**
- Two resistors 3 Ω and 6 Ω in series combined with a 9 Ω resistor in parallel.
- Expected:

Series first:

$$
R_s = 3 + 6 = 9\,\Omega
$$

Then parallel:

$$
\frac{1}{R_{eq}} = \frac{1}{9} + \frac{1}{9} \Rightarrow R_{eq} = 4.5\,\Omega
$$

---

## **Efficiency Analysis**

- **Time Complexity:**
    - Series detection: $O(N)$ per pass.
    - Parallel detection: $O(M)$ per pass.
    - Where $N$ is the number of nodes and $M$ is the number of edges.

- **Space Complexity:**
    - Storing a full graph: $O(N+M)$.

### **Optimization Strategies**
- Prioritize series simplifications before parallel simplifications.
- Use a union-find data structure to efficiently manage sets of connected nodes.
- Apply Kirchhoff's laws for advanced mesh analysis when needed.

---

## **Conclusion**

Graph theory provides a powerful, structured, and flexible framework for analyzing and simplifying electrical circuits. By representing circuits as weighted graphs, we can systematically identify series and parallel structures and iteratively reduce them to find the equivalent resistance.

This method is essential for:
- Manual analysis of moderately complex networks.
- Automating calculations in simulation software.
- Designing optimized electronic circuits.

Understanding graph-based circuit analysis bridges physics, computer science, and engineering, showcasing the interdisciplinary nature of modern scientific problems.

---

## **Future Extensions**
- Implement support for voltage and current sources (graph with labeled sources).
- Extend to AC circuits by handling impedance instead of pure resistance.
- Incorporate machine learning to predict optimal reduction paths for faster computation.

---
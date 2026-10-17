---
hide:
  - navigation
---

# Interactive lab

Here you can get your hands on network optimization: each app runs an algorithm step by step on the reference instances of the course,
which you can also change. Pick an app: it opens full page. Everything runs in the browser; the numbers are computed by the algorithm, not typed by hand.

## Graphs

<div class="grid cards" markdown>

-   :material-graph-outline: **Graph search: BFS and DFS**

    ---

    The generic search one iteration at a time, with LIST as a queue (BFS) or as a stack (DFS): labelling order, predecessor tree and levels d(j).

    [Open the app →](graph-search-bfs-dfs.md)

</div>

## Trees and paths

<div class="grid cards" markdown>

-   :material-pine-tree: **Minimum spanning trees: Kruskal and Prim**

    ---

    Kruskal on the edges sorted by weight, with the components and the rejected edges; Prim with the labels d(v), pred(v) and the cut; the weight of the tree.

    [Open the app →](minimum-spanning-tree-kruskal-prim.md)

-   :material-map-marker-path: **Shortest paths: Dijkstra, Bellman–Ford, acyclic graphs**

    ---

    The labels d(i) and pred(i) step by step: Dijkstra's permanent nodes, Bellman–Ford's passes with negative cycles, the topological order; at the end the tree and the potentials certificate.

    [Open the app →](shortest-paths-dijkstra-bellman-ford.md)

</div>

## Flows

<div class="grid cards" markdown>

-   :material-pipe: **Maximum flow: Ford–Fulkerson and Edmonds–Karp**

    ---

    The residual network, the augmenting path (depth-first or breadth-first search), the bottleneck and the flow update; at the end the minimum cut, whose capacity equals the flow value.

    [Open the app →](maximum-flow-ford-fulkerson-edmonds-karp.md)

-   :material-cash: **Minimum cost flow: cycle canceling and successive shortest paths**

    ---

    The residual network with costs, the negative cycle and its augmentation, or the shortest paths on the reduced costs; at the end the potentials certificate.

    [Open the app →](minimum-cost-flow.md)

-   :material-truck-delivery: **Transportation: initial solution and potentials method**

    ---

    The transportation tableau: north-west corner or minimum cost, then the potentials, the reduced costs, the cycle of the entering cell and the step.

    [Open the app →](transportation-potentials-method.md)

-   :material-grid: **Assignment: the Hungarian algorithm**

    ---

    Row and column reduction, covering the zeros with the minimum number of lines, adjusting the matrix and the optimal assignment.

    [Open the app →](assignment-hungarian-algorithm.md)

</div>

## The network simplex

<div class="grid cards" markdown>

-   :material-swap-horizontal: **The network simplex, pivot by pivot**

    ---

    The basis tree, the arcs at their bounds, the potentials and the reduced costs; the entering arc, the cycle, the step and the leaving arc; at the end the certificate.

    [Open the app →](network-simplex.md)

</div>

## Project management

<div class="grid cards" markdown>

-   :material-chart-gantt: **The critical path method (CPM)**

    ---

    The forward and backward pass on the project network, the slacks, the critical activities and the Gantt chart.

    [Open the app →](critical-path-method.md)

</div>

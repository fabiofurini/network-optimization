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

</div>

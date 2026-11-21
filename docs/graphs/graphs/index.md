---
title: "Graphs"
---

# Graphs

<div class="info-capitolo" markdown>

**Part 1 · Graphs · Chapter 1** · [:material-file-pdf-box: Lecture notes, volume 1 (PDF)](../../pdf/lecture-notes-1-graphs.pdf) · [:material-presentation: Slides](../../pdf/slides-graphs.pdf) · [:material-pencil: Exercises: Graphs](../../exercises/graphs.md) · [:material-gesture-tap: App: Graph search: BFS and DFS](../../lab/graph-search-bfs-dfs.md)

</div>

<div class="grid cards sottopagine" markdown>

-   **1.1 Undirected and directed graphs**

    Simple graphs and multigraphs

    [:octicons-arrow-right-24: Open](undirected-and-directed-graphs.md)

-   **1.2 Representations of a graph**

    The incidence matrix and flow conservation

    [:octicons-arrow-right-24: Open](representations-of-a-graph.md)

-   **1.3 Connectivity**

    [:octicons-arrow-right-24: Open](connectivity.md)

-   **1.4 Trees and forests**

    [:octicons-arrow-right-24: Open](trees-and-forests.md)

-   **1.5 The rank of the incidence matrix**

    [:octicons-arrow-right-24: Open](the-rank-of-the-incidence-matrix.md)

-   **1.6 Graph search**

    The predecessor tree · The breadth-first search on the reference graph · The depth-first search on the reference graph · Using the search

    [:octicons-arrow-right-24: Open](graph-search.md)

</div>

!!! nota "Prerequisites"

    - From the module <em>Linear Algebra</em>, the chapters [«Vectors»](https://fabiofurini.github.io/linear-algebra/vectors-matrices/01-vectors/) and [«Matrices»](https://fabiofurini.github.io/linear-algebra/vectors-matrices/02-matrices/): matrices, linear combinations, linearly independent vectors and the rank of a matrix.

    - From the module <em>Mathematical Analysis 1</em>, the chapters [«Sets»](https://fabiofurini.github.io/mathematical-analysis-1/numbers/01-sets/) and [«Binary relations»](https://fabiofurini.github.io/mathematical-analysis-1/relations/01-binary-relations/): sets, relations and equivalence classes.

    - From the module <em>Algorithms</em>, the chapter [«Asymptotic notation»](https://fabiofurini.github.io/algorithms/asymptotics/09-asymptotic-notation/): the $O(\cdot)$ notation for the running time of an algorithm.

    - No knowledge of graph theory is needed: every notion is defined in this chapter.

!!! chiave "Objectives"

    At the end of this chapter you will be able to:

    - use the basic notions on undirected and directed graphs: adjacency, degree, walks, paths and cycles;

    - store a graph as an adjacency matrix, as adjacency lists, as an arc list and as a node–arc incidence matrix, and compare the space they need;

    - find the connected components and the strongly connected components of a graph;

    - recognize a tree with the equivalent characterizations, and compute the rank of the incidence matrix;

    - run the breadth-first search and the depth-first search, draw the predecessor tree and prove that the search finds the reachable nodes in $O(|N|+|A|)$ time.

---

**Next:** [1.1 Undirected and directed graphs](undirected-and-directed-graphs.md)

---

**Exercises on this chapter:** [:material-pencil: Graphs](../../exercises/graphs.md)

<!-- laboratorio-interattivo: sezione generata da interattivi.py -->

:material-flask-outline: **In the interactive lab:** [Graph search: BFS and DFS](../../lab/graph-search-bfs-dfs.md).
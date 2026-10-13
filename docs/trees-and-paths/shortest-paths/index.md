---
title: "Shortest paths"
---

# Shortest paths

<div class="info-capitolo" markdown>

**Part 2 · Trees and paths · Chapter 3** · [:material-file-pdf-box: Lecture notes, volume 2 (PDF)](../../pdf/lecture-notes-2-trees-and-paths.pdf) · [:material-pencil: Exercises: Shortest paths](../../exercises/shortest-paths.md) · [:material-gesture-tap: App: Shortest paths: Dijkstra, Bellman–Ford, acyclic graphs](../../lab/shortest-paths-dijkstra-bellman-ford.md)

</div>

<div class="grid cards sottopagine" markdown>

-   **3.1 Shortest path problems**

    Optimality of subpaths

    [:octicons-arrow-right-24: Open](shortest-path-problems.md)

-   **3.2 Optimality conditions and potentials**

    [:octicons-arrow-right-24: Open](optimality-conditions-and-potentials.md)

-   **3.3 The linear programming formulation**

    The single-source model

    [:octicons-arrow-right-24: Open](the-linear-programming-formulation.md)

-   **3.4 Shortest paths in acyclic graphs**

    [:octicons-arrow-right-24: Open](shortest-paths-in-acyclic-graphs.md)

-   **3.5 The Bellman–Ford algorithm**

    [:octicons-arrow-right-24: Open](the-bellman-ford-algorithm.md)

-   **3.6 Dijkstra's algorithm**

    Dijkstra's algorithm on the reference graph · Negative lengths

    [:octicons-arrow-right-24: Open](dijkstra-s-algorithm.md)

</div>

!!! nota "Prerequisites"

    - From [Chapter 1 «Graphs»](https://fabiofurini.github.io/network-optimization/graphs/graphs/): directed walks, paths and cycles, the node–arc incidence matrix, trees and the reference graph.

    - From the module Linear Programming, [Chapter 9 «Duality theory»](https://fabiofurini.github.io/linear-programming/duality/09-duality/): the dual of an LP model and the weak duality theorem.

!!! chiave "Objectives"

    At the end of this chapter you will be able to:

    - state the $s$–$t$ and the single-source shortest path problems, and recognize when a negative cycle makes them ill-posed;

    - use the optimality of subpaths, Bellman's equations and the shortest path tree;

    - write the LP model of a shortest path as a unit flow, write its dual with the potentials $\pi_i$, and use feasible potentials as a certificate of optimality;

    - run the algorithm for acyclic graphs, the Bellman–Ford algorithm (with the detection of a negative cycle) and Dijkstra's algorithm, prove their correctness and give their running time.

---

**Next:** [3.1 Shortest path problems](shortest-path-problems.md)

---

**Exercises on this chapter:** [:material-pencil: Shortest paths](../../exercises/shortest-paths.md)

<!-- laboratorio-interattivo: sezione generata da interattivi.py -->

:material-flask-outline: **In the interactive lab:** [Shortest paths: Dijkstra, Bellman–Ford, acyclic graphs](../../lab/shortest-paths-dijkstra-bellman-ford.md).
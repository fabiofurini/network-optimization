---
title: "Transportation and assignment"
---

# Transportation and assignment

<div class="info-capitolo" markdown>

**Part 3 · Flows · Chapter 7** · [:material-file-pdf-box: Lecture notes, volume 3 (PDF)](../../pdf/lecture-notes-3-flows.pdf) · [:material-presentation: Slides](../../pdf/slides-transportation-and-assignment.pdf) · [:material-pencil: Exercises: Transportation and assignment](../../exercises/transportation-and-assignment.md) · [:material-gesture-tap: App: Transportation: initial solution and potentials method](../../lab/transportation-potentials-method.md) · [:material-gesture-tap: App: Assignment: the Hungarian algorithm](../../lab/assignment-hungarian-algorithm.md)

</div>

<div class="grid cards sottopagine" markdown>

-   **7.1 The transportation problem**

    Unbalanced instances · Transshipment as transportation

    [:octicons-arrow-right-24: Open](the-transportation-problem.md)

-   **7.2 Basic solutions**

    [:octicons-arrow-right-24: Open](basic-solutions.md)

-   **7.3 Initial basic feasible solutions**

    The minimum cost rule

    [:octicons-arrow-right-24: Open](initial-basic-feasible-solutions.md)

-   **7.4 The potential method**

    The potential method on the transportation instance · Degeneracy

    [:octicons-arrow-right-24: Open](the-potential-method.md)

-   **7.5 The assignment problem**

    Degeneracy of the potential method · Reductions and potentials · Independent zeros and lines · The Hungarian algorithm · The Hungarian algorithm on the example

    [:octicons-arrow-right-24: Open](the-assignment-problem.md)

</div>

!!! nota "Prerequisites"

    - From this module, [Chapter 1 «Graphs»](https://fabiofurini.github.io/network-optimization/graphs/graphs/): trees, leaves, fundamental cycles and the rank of the node–arc incidence matrix.

    - From this module, [Chapter 3 «Shortest paths»](https://fabiofurini.github.io/network-optimization/trees-and-paths/shortest-paths/): distances, and [Chapter 4 «Network flow models»](https://fabiofurini.github.io/network-optimization/flows/network-flow-models/): the minimum cost flow model, the dummy node, integer vertices, potentials and reduced costs.

    - From the module Linear Programming, [Chapter 9 «Duality theory»](https://fabiofurini.github.io/linear-programming/duality/09-duality/): the dual of an LP model and the weak and strong duality theorems.

!!! chiave "Objectives"

    At the end of this chapter you will be able to:

    - write the transportation model and its tableau, balance an instance with a dummy origin or destination, and reduce an uncapacitated transshipment instance to a transportation instance;

    - recognize the bases of the transportation model as the spanning trees of a bipartite network, compute a basic solution and recognize a degenerate one;

    - build an initial basic feasible solution with the north-west corner rule and the minimum cost rule;

    - run the potential method, with potentials, reduced costs, cycles and pivots, and certify the optimality of a solution with the dual model;

    - write the assignment model, prove the theorem of König and Egerváry, and run the Hungarian algorithm, reading its potentials as an optimal dual solution.

---

**Next:** [7.1 The transportation problem](the-transportation-problem.md)

---

**Exercises on this chapter:** [:material-pencil: Transportation and assignment](../../exercises/transportation-and-assignment.md)

<!-- laboratorio-interattivo: sezione generata da interattivi.py -->

:material-flask-outline: **In the interactive lab:** [Transportation: initial solution and potentials method](../../lab/transportation-potentials-method.md), [Assignment: the Hungarian algorithm](../../lab/assignment-hungarian-algorithm.md).
---
title: "The network simplex"
---

# The network simplex

<div class="info-capitolo" markdown>

**Part 4 · The network simplex · Chapter 8** · [:material-file-pdf-box: Lecture notes, volume 4 (PDF)](../../pdf/lecture-notes-4-network-simplex.pdf) · [:material-pencil: Exercises: Network simplex](../../exercises/network-simplex.md)

</div>

<div class="grid cards sottopagine" markdown>

-   **8.1 The simplex algorithm on the minimum cost flow model**

    [:octicons-arrow-right-24: Open](the-simplex-algorithm-on-the-minimum-cost-flow-model.md)

-   **8.2 Bases and spanning trees**

    [:octicons-arrow-right-24: Open](bases-and-spanning-trees.md)

-   **8.3 Potentials and optimality**

    [:octicons-arrow-right-24: Open](potentials-and-optimality.md)

-   **8.4 The pivot**

    [:octicons-arrow-right-24: Open](the-pivot.md)

-   **8.5 The network simplex algorithm**

    [:octicons-arrow-right-24: Open](the-network-simplex-algorithm.md)

-   **8.6 An uncapacitated example**

    [:octicons-arrow-right-24: Open](an-uncapacitated-example.md)

-   **8.7 Degeneracy and strongly feasible trees**

    [:octicons-arrow-right-24: Open](degeneracy-and-strongly-feasible-trees.md)

-   **8.8 A capacitated example with a degenerate pivot**

    [:octicons-arrow-right-24: Open](a-capacitated-example-with-a-degenerate-pivot.md)

-   **8.9 The initial tree: Phase 0**

    Typical mistakes · In summary

    [:octicons-arrow-right-24: Open](the-initial-tree-phase-0.md)

</div>

!!! nota "Prerequisites"

    - From this module, [Chapter 1 «Graphs»](https://fabiofurini.github.io/network-optimization/graphs/graphs/): spanning trees, leaves, fundamental cycles and the rank of the node–arc incidence matrix.

    - From this module, [Chapter 4 «Network flow models»](https://fabiofurini.github.io/network-optimization/flows/network-flow-models/): the minimum cost flow model, the removal of the lower bounds, the potentials, the reduced costs and the transshipment instance on the reference network.

    - From the module Linear Programming, [Chapter 6 «Simplex algorithm»](https://fabiofurini.github.io/linear-programming/simplex/06-simplex/), [Chapter 7 «Optimality conditions and pivot rules»](https://fabiofurini.github.io/linear-programming/simplex/07-optimality-pivot/), [Chapter 8 «Phase 0 of the simplex algorithm»](https://fabiofurini.github.io/linear-programming/simplex/08-phase-zero/) and [Chapter 11 «Revised simplex algorithm»](https://fabiofurini.github.io/linear-programming/advanced-methods/11-revised-simplex/): bases, basic solutions, reduced costs, pivoting operations, degeneracy and Phase 0.

!!! chiave "Objectives"

    At the end of this chapter you will be able to:

    - prove that the bases of the minimum cost flow model are the spanning trees, and compute a tree solution from the leaves;

    - compute the potentials of a spanning tree and the reduced costs, and test the optimality of a tree solution with arcs at the lower and at the upper bound;

    - perform a pivot: entering arc, oriented cycle, step, leaving arc, and the update of the flows, of the tree and of the potentials;

    - recognize a degenerate pivot, check whether a tree structure is strongly feasible, and apply the leaving arc rule that keeps it strongly feasible and prevents cycling;

    - find an initial tree structure with Phase 0 on the auxiliary network, or prove that no feasible flow exists.

---

**Next:** [8.1 The simplex algorithm on the minimum cost flow model](the-simplex-algorithm-on-the-minimum-cost-flow-model.md)

---

**Exercises on this chapter:** [:material-pencil: Network simplex](../../exercises/network-simplex.md)

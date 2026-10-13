---
title: "Network flow models"
---

# Network flow models

<div class="info-capitolo" markdown>

**Part 3 · Flows · Chapter 4** · [:material-file-pdf-box: Lecture notes, volume 3 (PDF)](../../pdf/lecture-notes-3-flows.pdf) · [:material-pencil: Exercises: Flow models](../../exercises/network-flow-models.md)

</div>

<div class="grid cards sottopagine" markdown>

-   **4.1 Networks and flows**

    [:octicons-arrow-right-24: Open](networks-and-flows.md)

-   **4.2 The minimum cost flow model**

    [:octicons-arrow-right-24: Open](the-minimum-cost-flow-model.md)

-   **4.3 Feasibility conditions**

    [:octicons-arrow-right-24: Open](feasibility-conditions.md)

-   **4.4 Removing the lower bounds**

    [:octicons-arrow-right-24: Open](removing-the-lower-bounds.md)

-   **4.5 Unbalanced instances**

    [:octicons-arrow-right-24: Open](unbalanced-instances.md)

-   **4.6 Total unimodularity and integrality**

    [:octicons-arrow-right-24: Open](total-unimodularity-and-integrality.md)

-   **4.7 The dual model and the reduced costs**

    [:octicons-arrow-right-24: Open](the-dual-model-and-the-reduced-costs.md)

-   **4.8 Special cases**

    [:octicons-arrow-right-24: Open](special-cases.md)

-   **4.9 A transshipment instance**

    The certificate of optimality

    [:octicons-arrow-right-24: Open](a-transshipment-instance.md)

</div>

!!! nota "Prerequisites"

    - From this module, [Chapter 1 «Graphs»](https://fabiofurini.github.io/network-optimization/graphs/graphs/): directed graphs, the node–arc incidence matrix, spanning trees and the rank of the incidence matrix.

    - From the module Linear Programming, [Chapter 9 «Duality theory»](https://fabiofurini.github.io/linear-programming/duality/09-duality/) and [Chapter 15 «The geometry of Linear Programming»](https://fabiofurini.github.io/linear-programming/advanced-methods/15-geometry/): the dual of an LP, weak and strong duality, vertices of a polyhedron.

    - Determinants: the Laplace expansion along a column and Cramer's rule.

!!! chiave "Objectives"

    At the end of this chapter you will be able to:

    - describe a network with balances, lower bounds, capacities and costs, and write the minimum cost flow model, also in matrix form with the incidence matrix;

    - check the necessary conditions for the existence of a feasible flow, and build counterexamples;

    - remove the lower bounds by a substitution, and balance an instance with a dummy node;

    - prove that the incidence matrix is totally unimodular, and deduce that the model has integer optimal solutions when the data are integer;

    - write the dual with the potentials $\pi_i$, compute the reduced costs and certify the optimality of a flow;

    - recognize the shortest path, the maximum flow, the transportation and the assignment problems as minimum cost flow models.

---

**Next:** [4.1 Networks and flows](networks-and-flows.md)

---

**Exercises on this chapter:** [:material-pencil: Flow models](../../exercises/network-flow-models.md)

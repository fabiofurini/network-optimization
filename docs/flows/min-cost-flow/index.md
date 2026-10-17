---
title: "Minimum cost flow"
---

# Minimum cost flow

<div class="info-capitolo" markdown>

**Part 3 · Flows · Chapter 6** · [:material-file-pdf-box: Lecture notes, volume 3 (PDF)](../../pdf/lecture-notes-3-flows.pdf) · [:material-presentation: Slides](../../pdf/slides-min-cost-flow.pdf) · [:material-pencil: Exercises: Minimum cost flow](../../exercises/min-cost-flow.md) · [:material-gesture-tap: App: Minimum cost flow: cycle canceling and successive shortest paths](../../lab/minimum-cost-flow.md)

</div>

<div class="grid cards sottopagine" markdown>

-   **6.1 The residual network with costs**

    [:octicons-arrow-right-24: Open](the-residual-network-with-costs.md)

-   **6.2 Circulations and their decomposition**

    [:octicons-arrow-right-24: Open](circulations-and-their-decomposition.md)

-   **6.3 Negative cycle optimality conditions**

    [:octicons-arrow-right-24: Open](negative-cycle-optimality-conditions.md)

-   **6.4 Optimality conditions with potentials**

    [:octicons-arrow-right-24: Open](optimality-conditions-with-potentials.md)

-   **6.5 A first feasible flow**

    [:octicons-arrow-right-24: Open](a-first-feasible-flow.md)

-   **6.6 The cycle-canceling algorithm**

    The algorithm · Cycle canceling on the reference network

    [:octicons-arrow-right-24: Open](the-cycle-canceling-algorithm.md)

-   **6.7 The successive shortest path algorithm**

    Successive shortest paths on the reference network

    [:octicons-arrow-right-24: Open](the-successive-shortest-path-algorithm.md)

</div>

!!! nota "Prerequisites"

    - From this module, [Chapter 3 «Shortest paths»](https://fabiofurini.github.io/network-optimization/trees-and-paths/shortest-paths/): the Bellman–Ford algorithm with the detection of a negative cycle, Dijkstra's algorithm, and the potentials $\pi_i=-\tilde{d}(i)$ as a certificate.

    - [Chapter 4 «Network flow models»](https://fabiofurini.github.io/network-optimization/flows/network-flow-models/): the minimum cost flow model, the flow across a cut, the substitution of the lower bounds, the potentials and the reduced costs.

    - [Chapter 5 «Maximum flow»](https://fabiofurini.github.io/network-optimization/flows/maximum-flow/): the residual network $G(\vet{x})$, augmenting paths and the Edmonds–Karp algorithm.

!!! chiave "Objectives"

    At the end of this chapter you will be able to:

    - build the residual network of a flow with residual capacities and costs, compute the cost of one of its cycles, and augment the flow along it;

    - decompose a circulation, and the difference of two feasible flows, into cycles;

    - prove that a feasible flow is optimal if and only if its residual network has no negative cycle, and if and only if potentials with non-negative reduced costs exist, and recognize an unbounded instance;

    - find a first feasible flow with a maximum flow;

    - run the cycle-canceling algorithm and the successive shortest path algorithm, and prove their correctness.

!!! nota "Where we were"

    - In [Chapter 4 «Network flow models»](https://fabiofurini.github.io/network-optimization/flows/network-flow-models/) the minimum cost flow problem is the LP $\min\{\vet{c}'\vet{x} : \mat{B}\vet{x}=\vet{b},~\vet{l} \le \vet{x} \le \vet{u}\}$. Potentials $\pi_i$ whose reduced costs $\bar{c}_{ij}=c_{ij}-\pi_i+\pi_j$ are positive only on empty arcs and negative only on saturated arcs certify that a flow is optimal.

    - On the reference network the optimal flow $\tilde{\vet{x}}$ costs $60$, and $\vet{\pi}=(15,13,13,5,10,0)$ certifies it.

    - In [Chapter 5 «Maximum flow»](https://fabiofurini.github.io/network-optimization/flows/maximum-flow/) a flow grows along augmenting paths of the residual network $G(\vet{x})$.

    - In this chapter the certificate becomes an algorithm: we lower the cost of a feasible flow along cycles of $G(\vet{x})$, or we build the flow along shortest paths of $G(\vet{x})$ keeping the certificate true.

---

**Next:** [6.1 The residual network with costs](the-residual-network-with-costs.md)

---

**Exercises on this chapter:** [:material-pencil: Minimum cost flow](../../exercises/min-cost-flow.md)

<!-- laboratorio-interattivo: sezione generata da interattivi.py -->

:material-flask-outline: **In the interactive lab:** [Minimum cost flow: cycle canceling and successive shortest paths](../../lab/minimum-cost-flow.md).
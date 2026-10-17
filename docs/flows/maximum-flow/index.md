---
title: "Maximum flow"
---

# Maximum flow

<div class="info-capitolo" markdown>

**Part 3 · Flows · Chapter 5** · [:material-file-pdf-box: Lecture notes, volume 3 (PDF)](../../pdf/lecture-notes-3-flows.pdf) · [:material-presentation: Slides](../../pdf/slides-maximum-flow.pdf) · [:material-pencil: Exercises: Maximum flow](../../exercises/maximum-flow.md) · [:material-gesture-tap: App: Maximum flow: Ford–Fulkerson and Edmonds–Karp](../../lab/maximum-flow-ford-fulkerson-edmonds-karp.md)

</div>

<div class="grid cards sottopagine" markdown>

-   **5.1 The maximum flow problem**

    [:octicons-arrow-right-24: Open](the-maximum-flow-problem.md)

-   **5.2 Cuts**

    [:octicons-arrow-right-24: Open](cuts.md)

-   **5.3 The residual network**

    [:octicons-arrow-right-24: Open](the-residual-network.md)

-   **5.4 The max-flow min-cut theorem**

    [:octicons-arrow-right-24: Open](the-max-flow-min-cut-theorem.md)

-   **5.5 The Ford–Fulkerson algorithm**

    The number of augmentations

    [:octicons-arrow-right-24: Open](the-ford-fulkerson-algorithm.md)

-   **5.6 The Edmonds–Karp algorithm**

    [:octicons-arrow-right-24: Open](the-edmonds-karp-algorithm.md)

-   **5.7 Applications**

    Maximum matching in a bipartite graph · Arc-disjoint paths

    [:octicons-arrow-right-24: Open](applications.md)

</div>

!!! nota "Prerequisites"

    - From this module, [Chapter 1 «Graphs»](https://fabiofurini.github.io/network-optimization/graphs/graphs/): directed paths, the breadth-first search and the depth-first search.

    - From this module, [Chapter 4 «Network flow models»](https://fabiofurini.github.io/network-optimization/flows/network-flow-models/): flow conservation, the flow across a cut, the minimum cost flow model and its integer vertices.

    - From the module Linear Programming, [Chapter 15 «The geometry of Linear Programming»](https://fabiofurini.github.io/linear-programming/advanced-methods/15-geometry/): a linear function attains its maximum over a nonempty bounded polyhedron.

!!! chiave "Objectives"

    At the end of this chapter you will be able to:

    - state the maximum flow problem and write its LP model;

    - compute the capacity of an $s$–$t$ cut, and use cuts as upper bounds on the value of every flow;

    - build the residual network of a flow, find an augmenting path and its bottleneck, and augment the flow;

    - prove the max-flow min-cut theorem and the integrality theorem;

    - run the Ford–Fulkerson and the Edmonds–Karp algorithms, read a minimum cut at the stop, and give their running times;

    - compute a maximum matching in a bipartite graph and a maximum set of arc-disjoint paths as maximum flows.

---

**Next:** [5.1 The maximum flow problem](the-maximum-flow-problem.md)

---

**Exercises on this chapter:** [:material-pencil: Maximum flow](../../exercises/maximum-flow.md)

<!-- laboratorio-interattivo: sezione generata da interattivi.py -->

:material-flask-outline: **In the interactive lab:** [Maximum flow: Ford–Fulkerson and Edmonds–Karp](../../lab/maximum-flow-ford-fulkerson-edmonds-karp.md).
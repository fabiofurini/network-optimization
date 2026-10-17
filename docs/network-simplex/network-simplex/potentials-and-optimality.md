---
title: "Potentials and optimality"
---

# 8.3 Potentials and optimality { #sez-sec-ns-optimality }

<div class="info-capitolo" markdown>

**Part 4 · The network simplex · Chapter 8** · [:material-book-open-variant: Chapter 8: Network simplex](index.md) · [:material-file-pdf-box: Lecture notes, volume 4 (PDF)](../../pdf/lecture-notes-4-network-simplex.pdf) · [:material-presentation: Slides](../../pdf/slides-network-simplex.pdf) · [:material-pencil: Exercises: Network simplex](../../exercises/network-simplex.md) · [:material-gesture-tap: App: The network simplex, pivot by pivot](../../lab/network-simplex.md)

</div>

<a id="box-9-ns-def-potentials"></a>

!!! definizione "Definition 8.7: potentials of a tree"

    Let $T$ be a spanning tree of $G$. Node $n$ is the <strong>root</strong> of $T$. The <strong>potentials</strong> of $T$ are the values $\pi_i$, $i \in N$, such that

    $$
    \bar{c}_{ij}=c_{ij}-\pi_i+\pi_j=0, \quad \forall (i,j) \in T, \qquad\qquad \pi_n=0 .
    $$

- The potentials are computed from the root, as in the certificate of [Chapter 4](https://fabiofurini.github.io/network-optimization/flows/network-flow-models/a-transshipment-instance/): $\pi_n=0$, and for a tree arc $(i,j)$ with one known endpoint, $\pi_j=\pi_i-c_{ij}$ or $\pi_i=\pi_j+c_{ij}$.

- The normalization $\pi_n=0$ corresponds to the deleted row of node $n$ in $\mat{M}$.

<a id="box-10-ns-lem-multipliers"></a>

!!! teorema "Lemma 8.8: potentials and simplex multipliers"

    The potentials of a spanning tree $T$ exist and are unique. The vector $(\pi_1,\pi_2,\dots,\pi_{n-1})$ is the vector of the simplex multipliers of the basis $T$, and $\bar{c}_{ij}$ is the reduced cost of $x_{ij}$. Moreover, $\pi_i$ is the cost of the tree path from $i$ to $n$, where an arc traversed from tail to head counts $+c_{ij}$ and an arc traversed from head to tail counts $-c_{ij}$.

??? dimostrazione "Proof"

    We write $\vet{\pi}=(\pi_1,\pi_2,\dots,\pi_{n-1})$ for the first $n-1$ potentials, and $\pi_n=0$.

    1. The column of $(i,j)$ in $\mat{M}$ has $+1$ in row $i$ and $-1$ in row $j$, the row of $n$ being deleted. Hence $\vet{\pi}'\mat{M}_{(i,j)}=\pi_i-\pi_j$, also when $i=n$ or $j=n$.

    2. The system $\vet{\pi}'\mat{M}_T=\vet{c}_T'$ reads $\pi_i-\pi_j=c_{ij}$ on the tree arcs, that is $\bar{c}_{ij}=0$. Its matrix is nonsingular by <span style="color:#1971c2">[Theorem 8.3](bases-and-spanning-trees.md#box-4-ns-th-bases)</span>, so the potentials exist and are unique, and $c_{ij}-\vet{\pi}'\mat{M}_{(i,j)}=c_{ij}-\pi_i+\pi_j=\bar{c}_{ij}$.

    3. Let $i=v_0,v_1,\dots,v_r=n$ be the tree path. An arc traversed from tail to head gives $\pi_{v_{t-1}}-\pi_{v_t}= c_{v_{t-1}v_t}$; an arc traversed from head to tail gives $\pi_{v_{t-1}}-\pi_{v_t}=-c_{v_tv_{t-1}}$. Adding up, the sum telescopes to $\pi_i-\pi_n=\pi_i$. <span class="qed">□</span>

- A <strong>cycle</strong> $C$ of $G$ is traversed in one of its two directions. Its arcs traversed from tail to head are <strong>forward</strong>, the others <strong>backward</strong>, and its cost is

    $$
    c(C)=\sum_{(i,j) \text{ forward}} c_{ij}-\sum_{(i,j) \text{ backward}} c_{ij} .
    $$

<a id="box-11-ns-lem-cycle"></a>

!!! teorema "Lemma 8.9: the cost of a cycle"

    For every vector of potentials $\vet{\pi}$ and every cycle $C$ traversed in one direction,

    $$
    c(C)=\sum_{(i,j) \text{ forward}} \bar{c}_{ij}-\sum_{(i,j) \text{ backward}} \bar{c}_{ij} .
    $$

    In particular, if $\vet{\pi}$ are the potentials of a spanning tree $T$ and $C$ is the fundamental cycle of an arc $(k,l) \notin T$, traversed in the direction of $(k,l)$, then $c(C)=\bar{c}_{kl}$.

??? dimostrazione "Proof"

    Let $C$ visit $v_0,v_1,\dots,v_r=v_0$, and let the arc $a_t$ join $v_{t-1}$ and $v_t$.

    1. If $a_t=(v_{t-1},v_t)$ is forward, $\bar{c}_{a_t}=c_{a_t}-(\pi_{v_{t-1}}-\pi_{v_t})$. If $a_t=(v_t,v_{t-1})$ is backward, $-\bar{c}_{a_t}=-c_{a_t}-(\pi_{v_{t-1}}-\pi_{v_t})$.

    2. Adding up over the cycle, the terms $\pi_{v_{t-1}}-\pi_{v_t}$ telescope to $\pi_{v_0}-\pi_{v_r}=0$, which gives the formula.

    3. For the fundamental cycle of $(k,l)$, every tree arc has $\bar{c}_{ij}=0$, and $(k,l)$ is forward: the sum is $\bar{c}_{kl}$. <span class="qed">□</span>

<a id="box-12-ns-th-optimality"></a>

!!! teorema "Theorem 8.10: optimality of a tree solution"

    Let $(T,L,U)$ be a feasible tree structure, with tree solution $\vet{x}$ and potentials $\vet{\pi}$. If

    $$
    \bar{c}_{ij} \ge 0, \quad \forall (i,j) \in L, \qquad\qquad \bar{c}_{ij} \le 0, \quad \forall (i,j) \in U,
    $$

    then $\vet{x}$ is an optimal solution of the $\mathrm{MCF}$ model. If the inequalities are strict, $\vet{x}$ is the unique optimal solution.

??? dimostrazione "Proof"

    Let $\vet{y}$ be a feasible flow. By [Chapter 4, Lemma «cost and reduced cost»](https://fabiofurini.github.io/network-optimization/flows/network-flow-models/the-dual-model-and-the-reduced-costs/), $\vet{c}'\vet{y}=\bar{\vet{c}}'\vet{y}+\vet{b}'\vet{\pi}$ and $\vet{c}'\vet{x}=\bar{\vet{c}}'\vet{x}+ \vet{b}'\vet{\pi}$, hence

    $$
    \vet{c}'\vet{y}-\vet{c}'\vet{x}=\sum_{(i,j) \in A}\bar{c}_{ij}\,(y_{ij}-x_{ij}) .
    $$

    - On the arcs of $T$ the term is zero, since $\bar{c}_{ij}=0$.

    - On the arcs of $L$, $x_{ij}=0 \le y_{ij}$ and $\bar{c}_{ij} \ge 0$: the term is $\bar{c}_{ij}y_{ij} \ge 0$.

    - On the arcs of $U$, $x_{ij}=u_{ij} \ge y_{ij}$ and $\bar{c}_{ij} \le 0$: the term is $\bar{c}_{ij}(y_{ij}-u_{ij}) \ge 0$.

    Hence $\vet{c}'\vet{y} \ge \vet{c}'\vet{x}$. With strict inequalities, $\vet{c}'\vet{y}=\vet{c}'\vet{x}$ forces $y_{ij}=0$ on $L$ and $y_{ij}=u_{ij}$ on $U$; the flows on $T$ are then those of the tree solution, which is unique (<span style="color:#1971c2">[Theorem 8.3](bases-and-spanning-trees.md#box-4-ns-th-bases)</span>), and $\vet{y}=\vet{x}$. <span class="qed">□</span>

- These are the conditions of [Chapter 4, Corollary «reduced cost certificate»](https://fabiofurini.github.io/network-optimization/flows/network-flow-models/the-dual-model-and-the-reduced-costs/): an arc with positive reduced cost is empty, an arc with negative reduced cost is saturated, and every tree arc has reduced cost zero.

- An arc of $L$ with $\bar{c}_{ij}<0$, or of $U$ with $\bar{c}_{ij}>0$, violates the conditions: by <span style="color:#1971c2">[Lemma 8.9](#box-11-ns-lem-cycle)</span>, sending flow around its fundamental cycle in the right direction lowers the cost by $|\bar{c}_{ij}|$ per unit.

<a id="box-13-ns-ex-potentials"></a>

!!! esempio "Example 8.3: potentials and reduced costs of the tree of $\bar{\vet{x}}$"

    For the tree structure of <span style="color:#1971c2">[Example 8.2](bases-and-spanning-trees.md#box-8-ns-ex-tree)</span> we start from the root $6$:

    $$
    \begin{gathered}
    \pi_6=0, \qquad \pi_4=\pi_6+c_{46}=5, \qquad \pi_2=\pi_4+c_{24}=10,\\
    \pi_5=\pi_4+c_{54}=10, \qquad \pi_1=\pi_2+c_{12}=12, \qquad \pi_3=\pi_2+c_{32}=12 .
    \end{gathered}
    $$

    For example, $\pi_1=c_{12}+c_{24}+c_{46}=12$ is the cost of the tree path $1,2,4,6$. The reduced costs of the nonbasic arcs are

    $$
    \begin{gathered}
    \bar{c}_{13}=2-12+12=2, \qquad \bar{c}_{35}=3-12+10=1,\\
    \bar{c}_{43}=3-5+12=10, \qquad \bar{c}_{56}=3-10+0=-7 .
    \end{gathered}
    $$

    - The arc $(4,3) \in L$ has $\bar{c}_{43} \ge 0$, and the arc $(5,6) \in U$ has $\bar{c}_{56} \le 0$.

    - The arcs $(1,3)$ and $(3,5)$ are in $U$ with positive reduced cost: the conditions of <span style="color:#1971c2">[Theorem 8.10](#box-12-ns-th-optimality)</span> fail.

    - The fundamental cycle of $(1,3)$, in its direction, is $1,3,2,1$: it uses $(1,3)$ and $(3,2)$ forward and $(1,2)$ backward, and its cost is $c_{13}+c_{32}-c_{12}=2+2-2=2=\bar{c}_{13}$. Decreasing $x_{13}$ and sending the flow around the cycle in the opposite direction lowers the cost by $2$ per unit.

!!! chiave ""

    The potentials of a tree vanish at the root and give reduced cost zero on the tree arcs; they are the simplex multipliers. The reduced cost of a nonbasic arc is the cost of its fundamental cycle, and a tree solution with $\bar{c} \ge 0$ on $L$ and $\bar{c} \le 0$ on $U$ is optimal.

---

**Next:** [8.4 The pivot](the-pivot.md)

---
title: "The residual network"
---

# 5.3 The residual network { #sez-sec-mf-residual }

<div class="info-capitolo" markdown>

**Part 3 · Flows · Chapter 5** · [:material-book-open-variant: Chapter 5: Maximum flow](index.md) · [:material-file-pdf-box: Lecture notes, volume 3 (PDF)](../../pdf/lecture-notes-3-flows.pdf) · [:material-pencil: Exercises: Maximum flow](../../exercises/maximum-flow.md) · [:material-gesture-tap: App: Maximum flow: Ford–Fulkerson and Edmonds–Karp](../../lab/maximum-flow-ford-fulkerson-edmonds-karp.md)

</div>

- In the rest of the chapter $G$ has no pair of opposite arcs $(i,j)$ and $(j,i)$, as the reference graph. An arc $(j,i)$ opposite to $(i,j)$ can be replaced by the arcs $(j,k)$ and $(k,i)$ through a new node $k$, both with capacity $u_{ji}$: conservation at $k$ gives $x_{jk}=x_{ki}$, and the flows of the two networks correspond, with the same value.

<a id="box-7-mf-def-residual"></a>

!!! definizione "Definition 5.5: residual network"

    Let $\vet{x}$ be a feasible flow. The <strong>residual network</strong> $G(\vet{x})=(N,A(\vet{x}))$ has, for every arc $(i,j) \in A$:

    - the <strong>forward arc</strong> $(i,j)$, with <strong>residual capacity</strong> $r_{ij}=u_{ij}-x_{ij}$, if $x_{ij}<u_{ij}$;

    - the <strong>backward arc</strong> $(j,i)$, with residual capacity $r_{ji}=x_{ij}$, if $x_{ij}>0$.

- The residual capacity $r_{ij}$ is how much flow can still be sent from $i$ to $j$: by raising $x_{ij}$ on a forward arc, or by lowering $x_{ji}$ on a backward arc.

- An empty arc gives only its forward arc, a saturated arc only its backward arc, and an arc with $0<x_{ij}<u_{ij}$ both. Hence $G(\vet{x})$ has at most $2m$ arcs, all with positive residual capacity.

- Without opposite arcs in $G$, every ordered pair of nodes carries at most one residual arc.

<a id="box-8-mf-def-augmenting"></a>

!!! definizione "Definition 5.6: augmenting path"

    Let $\vet{x}$ be a feasible flow. An <strong>augmenting path</strong> is a directed path $P$ from $s$ to $t$ in $G(\vet{x})$. Its <strong>bottleneck</strong> is

    $$
    \delta=\min_{(i,j) \in P} r_{ij}>0 .
    $$

    <strong>Augmenting</strong> $\vet{x}$ along $P$ means sending $\delta$ units along $P$: for every arc of $P$,

    - if it is a forward arc $(i,j)$, then $x_{ij}:=x_{ij}+\delta$;

    - if it is a backward arc $(j,i)$, with $(i,j) \in A$, then $x_{ij}:=x_{ij}-\delta$.

<a id="box-9-mf-lem-aug"></a>

!!! teorema "Lemma 5.7: augmentation"

    Augmenting a feasible flow $\vet{x}$ of value $v$ along an augmenting path $P$ with bottleneck $\delta$ gives a feasible flow $\vet{x}'$ of value $v+\delta$.

??? dimostrazione "Proof"

    The nodes of $P$ are distinct and $G$ has no opposite arcs, so every arc of $A$ changes at most once.

    1. <em>Bounds.</em> On a forward arc, $x_{ij}+\delta \le x_{ij}+r_{ij}=u_{ij}$; on a backward arc, $x_{ij}-\delta \ge x_{ij}-r_{ji}=0$.

    2. <em>Conservation.</em> Let $k \notin \{s,t\}$ be a node of $P$. The arc of $P$ entering $k$ raises the net inflow of $k$ by $\delta$: a forward arc $(h,k)$ raises $x_{hk}$, a backward arc $(h,k)$ lowers $x_{kh}$. In the same way, the arc of $P$ leaving $k$ raises the net outflow of $k$ by $\delta$. The two changes cancel, and the nodes outside $P$ are not touched.

    3. <em>Value.</em> The path $P$ leaves $s$ once and never enters it again, so the net outflow of $s$ grows by $\delta$. <span class="qed">□</span>

<a id="box-10-mf-ex-residual"></a>

!!! esempio "Example 5.3: the residual network of $\bar{\vet{x}}$"

    For the flow $\bar{\vet{x}}$ of <span style="color:#1971c2">[Example 5.1](the-maximum-flow-problem.md#box-2-mf-ex-ref)</span>, of value $3$, the residual network $G(\bar{\vet{x}})$ has $13$ arcs. The six backward arcs, dashed in the figure, are $(2,1)$, $(3,4)$, $(4,2)$, $(5,3)$, $(6,4)$, $(6,5)$.

    - The arc $(2,4)$ is saturated, so it gives only the backward arc $(4,2)$, with $r_{42}=\bar{x}_{24}=3$.

    - The arc $(1,2)$ has $0<\bar{x}_{12}=3<5$, so it gives the forward arc $(1,2)$, with $r_{12}=2$, and the backward arc $(2,1)$, with $r_{21}=3$.

    ![Figure 3](../../img/maximum-flow/fig03.svg){ .fig loading=lazy  }

    The depth-first search of Chapter 1 from node $1$, with the residual arcs of each node by increasing index of the head, labels the nodes $1,2,3,4,6$: from $2$ the only residual arc goes back to $1$, from $3$ the search takes the backward arc $(3,4)$ ($2$ is labelled), and from $4$ the arc $(4,6)$. The augmenting path is $P=1,3,4,6$ (violet), with bottleneck

    $$
    \delta=\min\{r_{13},\,r_{34},\,r_{46}\}=\min\{4,\,2,\,3\}=2 .
    $$

    Augmenting gives $x_{13}=0+2=2$, $x_{43}=2-2=0$ (backward arc) and $x_{46}=1+2=3$, with value $3+2=5$. The two units that went from $4$ to $3$ now go from $4$ to $6$, and node $3$ receives two new units from $1$, which continue along $3,5,6$.

<a id="box-11-mf-ex-backward"></a>

!!! esempio "Example 5.4: why the backward arcs are needed"

    Suppose that from $\bar{\vet{x}}$ we use only the forward arcs of the residual network, so that flows can only grow.

    - The depth-first search on the forward arcs finds the path $1,3,5,4,6$, with $\delta=\min\{4,2,2,3\}=2$, and the value becomes $5$ with the flow $\vet{x}=(3,2,3,0,4,2,3,2,2)$.

    - Now the forward arcs $(2,4)$ and $(3,5)$ leaving $\{1,2,3\}$ are saturated: the search labels only $1,2,3$, and the method stops with value $5$.

    - The value is not maximum: for $S=\{1,2,3\}$, <span style="color:#1971c2">[Lemma 5.3](cuts.md#box-4-mf-lem-cut)</span> gives $v=x(\delta^+(S))-x(\delta^-(S))=7-2=5$. The two units on the backward arc $(4,3)$ of the cut, sent there by the first choices, come back into $S$.

    Only the backward arc $(3,4)$ of the residual network can cancel them: from this flow, the augmenting paths $1,3,4,5,6$ (with the backward arcs $(3,4)$ and $(4,5)$) and $1,3,4,6$, with $\delta=1$ each, reach the value $7$.

!!! chiave ""

    The residual network has a forward arc where the flow can grow and a backward arc where it can shrink. Sending the bottleneck $\delta$ along a path from $s$ to $t$ of the residual network keeps the flow feasible and raises its value by $\delta$; the backward arcs undo earlier choices.

---

**Next:** [5.4 The max-flow min-cut theorem](the-max-flow-min-cut-theorem.md)

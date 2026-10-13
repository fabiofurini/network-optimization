---
title: "Shortest path problems"
---

# 3.1 Shortest path problems { #sez-sec-sp-problems }

<div class="info-capitolo" markdown>

**Part 2 · Trees and paths · Chapter 3** · [:material-book-open-variant: Chapter 3: Shortest paths](index.md) · [:material-file-pdf-box: Lecture notes, volume 2 (PDF)](../../pdf/lecture-notes-2-trees-and-paths.pdf) · [:material-pencil: Exercises: Shortest paths](../../exercises/shortest-paths.md) · [:material-gesture-tap: App: Shortest paths: Dijkstra, Bellman–Ford, acyclic graphs](../../lab/shortest-paths-dijkstra-bellman-ford.md)

</div>

<a id="box-1-sp-def-problem"></a>

!!! definizione "Definition 3.1: shortest path problems"

    Let $G=(N,A)$ be a directed graph with a <strong>length</strong> $d_{ij} \in \R$ for every arc $(i,j) \in A$, of any sign.

    - The length of a directed walk $W=i_0,i_1,\dots,i_k$ is the sum of the lengths of its arcs, $d(W)=\sum_{t=1}^{k} d_{i_{t-1}i_t}$.

    - Given two nodes $s$ and $t$, the <strong>$s$–$t$ shortest path problem</strong> asks for a directed path from $s$ to $t$ of minimum length.

    - Given a node $s$, the <strong>source</strong>, the <strong>single-source shortest path problem</strong> asks for a shortest directed path from $s$ to every node $j \in N$.

    The minimum length of a directed path from $s$ to $j$ is the <strong>distance</strong> $\tilde{d}(j)$ of $j$; we set $\tilde{d}(j)=+\infty$ if $j$ is not reachable from $s$.

- In this chapter we write $n=|N|$, $m=|A|$, and “path” and “cycle” always mean directed path and directed cycle.

- An algorithm for the single-source problem also solves the $s$–$t$ problem, for every $t$ at once.

<a id="box-2-sp-ex-ref"></a>

!!! esempio "Example 3.1: the reference graph with lengths"

    We give the reference graph of [Chapter 1 «Graphs»](https://fabiofurini.github.io/network-optimization/graphs/graphs/) the lengths $d_{ij}$ written on the arcs, all non-negative; the source is $s=1$.

    ![Figure 1](../../img/shortest-paths/fig01.svg){ .fig loading=lazy  }

    Three of the paths from $1$ to $6$ and their lengths are:

    $$
    d(1,2,4,6)=7+3+5=15, \qquad d(1,3,2,4,6)=2+3+3+5=13, \qquad d(1,3,5,6)=2+8+7=17.
    $$

    The distances from node $1$, computed in <span style="color:#1971c2">Section [3.6](dijkstra-s-algorithm.md#sez-sec-sp-dijkstra)</span>, are

    $$
    \tilde{d}=(0,\,5,\,2,\,8,\,10,\,13),
    $$

    so $1,3,2,4,6$ is a shortest path from $1$ to $6$.

## 3.1.1 Negative cycles

<a id="box-3-sp-def-negcycle"></a>

!!! definizione "Definition 3.2: negative cycle"

    A <strong>negative cycle</strong> is a directed cycle $C$ with $d(C)<0$. In the rest of the chapter we refer to two assumptions:

    - **(A1)** every node of $G$ is reachable from $s$;

    - **(A2)** no negative cycle of $G$ is reachable from $s$.

<a id="box-4-sp-lem-walk"></a>

!!! teorema "Lemma 3.3: walks and paths"

    Under (A2), for every directed walk $W$ from $s$ to $j$ there is a directed path $P$ from $s$ to $j$, with arcs of $W$, such that $d(P) \le d(W)$.

??? dimostrazione "Proof"

    By induction on the number of arcs of $W$. If $W$ has distinct nodes, $P=W$.

    1. Otherwise $W$ repeats a node: $W=s,\dots,i_a,\dots,i_b,\dots,j$ with $i_a=i_b$, $a<b$, and $b-a$ minimum. The piece $C=i_a,\dots,i_b$ is a cycle, reachable from $s$ along $W$.

    2. By (A2), $d(C) \ge 0$. Deleting $C$ from $W$ gives a walk $W'$ from $s$ to $j$ with fewer arcs and $d(W')=d(W)-d(C) \le d(W)$.

    3. By induction $W'$ contains a path $P$ with $d(P) \le d(W') \le d(W)$. <span class="qed">□</span>

- Under (A2) the minimum length of a walk from $s$ to $j$ equals the distance $\tilde{d}(j)$: the algorithms of this chapter compute lengths of walks, and the lemma turns them into paths.

- With a negative cycle $C$ reachable from $s$ and from which $j$ is reachable, going around $C$ again and again gives walks from $s$ to $j$ of arbitrarily negative length. The algorithms of this chapter then detect $C$ instead of computing the distances.

<a id="box-5-sp-ex-negcycle"></a>

!!! esempio "Example 3.2: a negative cycle"

    The reference graph has two cycles, $2,4,3,2$ and $3,5,4,3$. With the lengths of <span style="color:#1971c2">[Example 3.1](#box-2-sp-ex-ref)</span> their lengths are $7$ and $11$. If the length of the arc $(5,4)$ drops from $2$ to $d''_{54}=-10$, the cycle $3,5,4,3$ has length

    $$
    8-10+1=-1 ,
    $$

    and the walks $1,3,5,6$, $1,3,5,4,3,5,6$, $1,3,5,4,3,5,4,3,5,6$, … from $1$ to $6$ have lengths $17,16,15,\dots$: no walk is shortest. We use these lengths $d''$ again in <span style="color:#1971c2">Section [3.5](the-bellman-ford-algorithm.md#sez-sec-sp-bf)</span>.

## 3.1.2 Optimality of subpaths

<a id="box-6-sp-lem-subpath"></a>

!!! teorema "Lemma 3.4: optimality of subpaths"

    Under (A2), let $P$ be a shortest path from $s$ to $j$, and let $i$ be a node of $P$. Then the subpath $P_{si}$ of $P$ from $s$ to $i$ is a shortest path from $s$ to $i$.

??? dimostrazione "Proof"

    Write $P$ as $P_{si}$ followed by the subpath $P_{ij}$ from $i$ to $j$, so $d(P)=d(P_{si})+d(P_{ij})$. Assume by contradiction that a path $Q$ from $s$ to $i$ has $d(Q)<d(P_{si})$.

    1. $Q$ followed by $P_{ij}$ is a walk from $s$ to $j$ of length $d(Q)+d(P_{ij})<d(P)$.

    2. By <span style="color:#1971c2">[Lemma 3.3](#box-4-sp-lem-walk)</span> it contains a path from $s$ to $j$ shorter than $P$: a contradiction. <span class="qed">□</span>

<a id="box-7-sp-th-bellman"></a>

!!! teorema "Theorem 3.5: Bellman's equations"

    Under (A1) and (A2), the distances satisfy

    $$
    \tilde{d}(s)=0, \qquad \tilde{d}(j)=\min_{(i,j) \in \delta^-(j)} \big\{\, \tilde{d}(i)+d_{ij} \,\big\}, \quad
    \forall j \in N \setminus \{s\},
    $$

    and $\tilde{d}(j) \le \tilde{d}(i)+d_{ij}$ for every arc $(i,j) \in A$.

??? dimostrazione "Proof"

    All distances are finite by (A1), and $\tilde{d}(s)=0$: the path $s$ has length $0$, and a path from $s$ to $s$ with arcs would be a cycle, of length $\ge 0$ by (A2).

    - <em>Inequality.</em> A shortest path from $s$ to $i$ followed by the arc $(i,j)$ is a walk of length $\tilde{d}(i)+d_{ij}$; by <span style="color:#1971c2">[Lemma 3.3](#box-4-sp-lem-walk)</span>, $\tilde{d}(j) \le \tilde{d}(i)+d_{ij}$.

    - <em>Equation.</em> For $j \neq s$, let $P$ be a shortest path from $s$ to $j$ and $(i,j)$ its last arc. By <span style="color:#1971c2">[Lemma 3.4](#box-6-sp-lem-subpath)</span>, $\tilde{d}(j)=d(P)=\tilde{d}(i)+d_{ij}$, so the minimum is attained.

    <p class="qed-riga"><span class="qed">□</span></p>

<a id="box-8-sp-prop-tree"></a>

!!! teorema "Proposition 3.6: shortest path tree"

    Under (A1) and (A2), there is a spanning tree $T$ of $G$, the <strong>shortest path tree</strong>, such that for every $j \in N$ the path from $s$ to $j$ in $T$ is directed and is a shortest path.

??? dimostrazione "Proof"

    For every $j$, let $k(j)$ be the minimum number of arcs of a shortest path from $s$ to $j$; $k(s)=0$.

    1. For $j \neq s$, choose a shortest path $P$ from $s$ to $j$ with $k(j)$ arcs, and let $\mathit{pred}(j)$ be the node before $j$ on $P$.

    2. The subpath of $P$ from $s$ to $\mathit{pred}(j)$ is shortest (<span style="color:#1971c2">[Lemma 3.4](#box-6-sp-lem-subpath)</span>) with $k(j)-1$ arcs, so $k(\mathit{pred}(j)) \le k(j)-1$, and $\tilde{d}(j)=\tilde{d}(\mathit{pred}(j))+d_{\mathit{pred}(j)\,j}$.

    3. Moving from $j$ to $\mathit{pred}(j)$, the number $k$ strictly decreases, so the sequence ends in $s$. The arcs $(\mathit{pred}(j),j)$ are $n-1$ and connect every node to $s$: they form a spanning tree ([Chapter 1, Theorem «characterizations of a tree»](https://fabiofurini.github.io/network-optimization/graphs/graphs/trees-and-forests/)).

    4. Along the tree path $s=i_0,i_1,\dots,i_r=j$ every arc satisfies $\tilde{d}(i_t)=\tilde{d}(i_{t-1})+d_{i_{t-1}i_t}$; adding up, its length is $\tilde{d}(j)$. <span class="qed">□</span>

<a id="box-9-sp-ex-bellman"></a>

!!! esempio "Example 3.3: Bellman's equations on the reference graph"

    With the distances $\tilde{d}=(0,5,2,8,10,13)$ of <span style="color:#1971c2">[Example 3.1](#box-2-sp-ex-ref)</span>:

    - node $4$ has the entering arcs $(2,4)$ and $(5,4)$, and $\tilde{d}(4)=\min\{5+3,\;10+2\}=8$;

    - node $6$ has the entering arcs $(4,6)$ and $(5,6)$, and $\tilde{d}(6)=\min\{8+5,\;10+7\}=13$.

    The arcs attaining the minimum form the shortest path tree $(1,3)$, $(3,2)$, $(2,4)$, $(3,5)$, $(4,6)$, in blue; next to each node its distance.

    ![Figure 2](../../img/shortest-paths/fig02.svg){ .fig loading=lazy  }

!!! chiave ""

    Without negative cycles reachable from the source, every subpath of a shortest path is shortest, the distances satisfy Bellman's equations, and one spanning tree contains a shortest path to every node.

---

**Next:** [3.2 Optimality conditions and potentials](optimality-conditions-and-potentials.md)

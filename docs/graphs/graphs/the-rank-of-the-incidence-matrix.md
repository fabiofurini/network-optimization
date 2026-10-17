---
title: "The rank of the incidence matrix"
---

# 1.5 The rank of the incidence matrix { #sez-sec-gr-rank }

<div class="info-capitolo" markdown>

**Part 1 · Graphs · Chapter 1** · [:material-book-open-variant: Chapter 1: Graphs](index.md) · [:material-file-pdf-box: Lecture notes, volume 1 (PDF)](../../pdf/lecture-notes-1-graphs.pdf) · [:material-presentation: Slides](../../pdf/slides-graphs.pdf) · [:material-pencil: Exercises: Graphs](../../exercises/graphs.md) · [:material-gesture-tap: App: Graph search: BFS and DFS](../../lab/graph-search-bfs-dfs.md)

</div>

- Let $G=(N,A)$ be a directed graph with node–arc incidence matrix $\mat{B}$. We denote by $\mat{B}_a$ the column of the arc $a$, and by $\vet{e}_i$ the $i$-th unit vector of $\R^n$, so that $\mat{B}_{(i,j)}=\vet{e}_i-\vet{e}_j$.

<a id="box-27-gr-lem-forest"></a>

!!! teorema "Lemma 1.20: columns of a forest"

    If the arcs $F \subseteq A$ form a forest, the columns $\mat{B}_a$, $a \in F$, are linearly independent.

??? dimostrazione "Proof"

    By induction on $|F|$; for $F=\emptyset$ there is nothing to prove. Let $|F| \ge 1$ and $\sum_{a \in F} \lambda_a \mat{B}_a=\vet{0}$.

    1. A component of the forest with at least one arc is a tree with at least $2$ nodes, so it has a leaf $\ell$ (<span style="color:#1971c2">[Lemma 1.14](trees-and-forests.md#box-20-gr-lem-leaves)</span>); let $a' \in F$ be the only arc of $F$ incident to $\ell$.

    2. Row $\ell$ of the combination contains only the term of $a'$, which is $\pm\lambda_{a'}$; hence $\lambda_{a'}=0$.

    3. The arcs $F \setminus \{a'\}$ still form a forest, and $\sum_{a \in F \setminus \{a'\}} \lambda_a \mat{B}_a=\vet{0}$: by induction all the $\lambda_a$ are zero. <span class="qed">□</span>

<a id="box-28-gr-lem-cycle"></a>

!!! teorema "Lemma 1.21: columns of a cycle"

    If the arcs $C \subseteq A$ form a cycle, the columns $\mat{B}_a$, $a \in C$, are linearly dependent.

??? dimostrazione "Proof"

    Let the cycle visit $v_0,v_1,\dots,v_k=v_0$ along the arcs $c_1,c_2,\dots,c_k$, and let $\varepsilon_t=+1$ if $c_t$ is forward and $\varepsilon_t=-1$ if it is backward. In both cases $\varepsilon_t \mat{B}_{c_t}=\vet{e}_{v_{t-1}}- \vet{e}_{v_t}$, and the sum telescopes:

    $$
    \sum_{t=1}^{k} \varepsilon_t \mat{B}_{c_t}=\vet{e}_{v_0}-\vet{e}_{v_k}=\vet{0}.
    $$

    The coefficients $\varepsilon_t$ are not zero, so the columns are linearly dependent. <span class="qed">□</span>

<a id="box-29-gr-th-rank"></a>

!!! teorema "Theorem 1.22: rank of the incidence matrix"

    Let $G=(N,A)$ be a directed graph whose underlying undirected graph has $k$ connected components. Then

    $$
    \rank(\mat{B})=|N|-k .
    $$

??? dimostrazione "Proof"

    Let $N_1,N_2,\dots,N_k$ be the node sets of the components, and $n=|N|$.

    - <em>$\rank(\mat{B}) \ge n-k$.</em> By <span style="color:#1971c2">[Corollary 1.18](trees-and-forests.md#box-24-gr-cor-spanning)</span> the graph has a spanning forest with $n-k$ arcs, whose columns are linearly independent by <span style="color:#1971c2">[Lemma 1.20](#box-27-gr-lem-forest)</span>.

    - <em>$\rank(\mat{B}) \le n-k$.</em> Every arc has both endpoints in the same component, so for each $h \in \{1,2,\dots,k\}$ the rows of the nodes of $N_h$ add up to the zero vector. The $k$ vectors $\vet{y}^h$ with $y^h_i=1$ for $i \in N_h$ and $0$ otherwise satisfy $(\vet{y}^h)' \mat{B}=\vet{0}'$.

    - These $k$ vectors have disjoint supports, so they are linearly independent: the left null space of $\mat{B}$ has dimension at least $k$, and $\rank(\mat{B}) \le n-k$.

    <p class="qed-riga"><span class="qed">□</span></p>

<a id="box-30-gr-cor-basis"></a>

!!! teorema "Corollary 1.23: bases of the incidence matrix"

    Let the underlying undirected graph of $G=(N,A)$ be connected. Then $\rank(\mat{B})=|N|-1$, the matrix obtained by deleting any one row of $\mat{B}$ has full row rank, and a set of $|N|-1$ columns of $\mat{B}$ is linearly independent if and only if its arcs form a spanning tree.

??? dimostrazione "Proof"

    The rank is $n-1$ by <span style="color:#1971c2">[Theorem 1.22](#box-29-gr-th-rank)</span> with $k=1$.

    - The rows add up to zero, so any row is minus the sum of the others: the remaining $n-1$ rows span the row space, which has dimension $n-1$, and they are linearly independent.

    - If $n-1$ arcs form a spanning tree, their columns are independent by <span style="color:#1971c2">[Lemma 1.20](#box-27-gr-lem-forest)</span>. If their columns are independent, the arcs contain no cycle by <span style="color:#1971c2">[Lemma 1.21](#box-28-gr-lem-cycle)</span>: they are acyclic with $n-1$ arcs, hence a spanning tree by <span style="color:#1971c2">[Theorem 1.17](trees-and-forests.md#box-23-gr-th-tree)</span>(c).

    <p class="qed-riga"><span class="qed">□</span></p>

<a id="box-31-gr-ex-rank"></a>

!!! esempio "Example 1.8: the rank on the reference graph"

    - The reference graph is weakly connected, so $\rank(\mat{B})=6-1=5$; Gaussian elimination on the matrix of <span style="color:#1971c2">[Example 1.4](representations-of-a-graph.md#box-12-gr-ex-matrices)</span> confirms it.

    - The five columns of the spanning tree of <span style="color:#1971c2">[Example 1.7](trees-and-forests.md#box-26-gr-ex-tree)</span>, $a_1,a_2,a_3,a_5,a_7$, are linearly independent.

    - The directed cycle $2,4,3,2$ uses $a_3=(2,4)$, $a_6=(4,3)$, $a_4=(3,2)$, all forward, and $\mat{B}_{a_3}+\mat{B}_{a_6}+\mat{B}_{a_4}=\vet{0}$.

    - Without the arcs $(4,6)$ and $(5,6)$ the graph has the two components $\{1,2,3,4,5\}$ and $\{6\}$, and the rank of its incidence matrix is $6-2=4$.

!!! chiave ""

    The rank of the node–arc incidence matrix is the number of nodes minus the number of connected components. In a connected graph one row is redundant, and the bases of $\mat{B}$ are exactly the spanning trees.

---

**Next:** [1.6 Graph search](graph-search.md)

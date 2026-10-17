---
title: "The simplex algorithm on the minimum cost flow model"
---

# 8.1 The simplex algorithm on the minimum cost flow model { #sez-sec-ns-lp }

<div class="info-capitolo" markdown>

**Part 4 · The network simplex · Chapter 8** · [:material-book-open-variant: Chapter 8: Network simplex](index.md) · [:material-file-pdf-box: Lecture notes, volume 4 (PDF)](../../pdf/lecture-notes-4-network-simplex.pdf) · [:material-presentation: Slides](../../pdf/slides-network-simplex.pdf) · [:material-pencil: Exercises: Network simplex](../../exercises/network-simplex.md) · [:material-gesture-tap: App: The network simplex, pivot by pivot](../../lab/network-simplex.md)

</div>

<a id="box-1-ns-def-basis"></a>

!!! definizione "Definition 8.1: basis and basic solution"

    Let $G=(N,A)$ be a network with $n$ nodes and $m$ arcs, whose underlying undirected graph is connected, with balances $b_i$ such that $\sum_{i \in N} b_i=0$, costs $c_{ij}$, zero lower bounds and capacities $0<u_{ij} \le +\infty$. Let $\mat{M}$ be its node–arc incidence matrix $\mat{B}$ without the row of node $n$, with the column $\mat{M}_a$ for the arc $a$, and let $\vet{h}=(b_1,b_2,\dots,b_{n-1})'$.

    - A <strong>basis</strong> is a set $T \subseteq A$ of $n-1$ arcs whose columns $\mat{M}_a$, $a \in T$, are linearly independent. The arcs of $T$ are <strong>basic</strong>, the other arcs are <strong>nonbasic</strong>.

    - A <strong>bound status</strong> of the nonbasic arcs is a partition of $A \setminus T$ into two sets $L$ and $U$, where every arc of $U$ has a finite capacity.

    - The <strong>basic solution</strong> of $(T,L,U)$ is the vector $\vet{x}$ with $x_{ij}=0$ on the arcs of $L$, $x_{ij}=u_{ij}$ on the arcs of $U$, and $\mat{M}\vet{x}=\vet{h}$. It is <strong>feasible</strong> if $0 \le x_{ij} \le u_{ij}$ on the arcs of $T$.

- In the whole chapter the network is as in the definition. The lower bounds are removed as in [Chapter 4 «Network flow models»](https://fabiofurini.github.io/network-optimization/flows/network-flow-models/), an arc with $u_{ij}=0$ is deleted, and the $\mathrm{MCF}$ model is

    $$
    \min\big\{\,\vet{c}'\vet{x} \;:\; \mat{B}\vet{x}=\vet{b},~\vet{0} \le \vet{x} \le \vet{u}\,\big\}.
    $$

- The basis is a set of columns; $L$ and $U$ say at which bound each nonbasic variable is fixed. The values of the basic variables solve the square system $\mat{M}_T\vet{x}_T=\vet{h}-\sum_{a \in U}\mat{M}_a u_a$, which has a unique solution because $\mat{M}_T$ is nonsingular.

<a id="box-2-ns-lem-redundant"></a>

!!! teorema "Lemma 8.2: the redundant equation"

    Let the underlying undirected graph of $G$ be connected and $\sum_{i \in N} b_i=0$. Then $\mat{M}$ has rank $n-1$, and a vector $\vet{x} \in \R^m$ satisfies $\mat{B}\vet{x}=\vet{b}$ if and only if it satisfies $\mat{M}\vet{x}=\vet{h}$.

??? dimostrazione "Proof"

    The rank is $n-1$ by [Chapter 1, Corollary «bases of the incidence matrix»](https://fabiofurini.github.io/network-optimization/graphs/graphs/the-rank-of-the-incidence-matrix/): deleting one row of $\mat{B}$ leaves $n-1$ linearly independent rows.

    - If $\mat{B}\vet{x}=\vet{b}$, then in particular $\mat{M}\vet{x}=\vet{h}$.

    - Conversely, every column of $\mat{B}$ has one $+1$ and one $-1$, so the rows of $\mat{B}$ add up to the zero vector. If $\mat{M}\vet{x}=\vet{h}$, row $n$ of $\mat{B}\vet{x}$ is $-\sum_{i=1}^{n-1}b_i=b_n$.

    <p class="qed-riga"><span class="qed">□</span></p>

- Hence a basic solution satisfies the conservation constraints of all the nodes, node $n$ included.

- The definition is the one of the simplex algorithm with one difference: in [Chapter 6 «Simplex algorithm»](https://fabiofurini.github.io/linear-programming/simplex/06-simplex/) of the module Linear Programming every nonbasic variable is zero, while here a nonbasic variable can also sit at its upper bound $u_{ij}$.

## 8.1.1 The simplex algorithm with bounds

- As in [Chapter 11 «Revised simplex algorithm»](https://fabiofurini.github.io/linear-programming/advanced-methods/11-revised-simplex/), at a basis $T$ the <strong>simplex multipliers</strong> $\vet{\pi} \in \R^{n-1}$ solve the first system $\vet{\pi}'\mat{M}_T=\vet{c}_T'$, and the reduced cost of the variable $x_a$ is $c_a-\vet{\pi}'\mat{M}_a$.

- The $\mathrm{MCF}$ model is a minimization. A nonbasic variable at its lower bound lowers the cost when it increases if its reduced cost is negative; a nonbasic variable at its upper bound lowers the cost when it decreases if its reduced cost is positive.

- If no nonbasic variable can lower the cost, the basic solution is optimal. Otherwise one of them enters the basis, the ratio test gives the largest step that keeps the basic variables within their bounds, and a basic variable that reaches a bound leaves the basis.

- The <strong>network simplex algorithm</strong> performs exactly these operations, without matrices: the bases are spanning trees, the multipliers are potentials computed along the tree, and the ratio test runs along a cycle.

<a id="box-3-ns-ex-bases"></a>

!!! esempio "Example 8.1: bases of the reference network"

    In the reference network of [Chapter 4 «Network flow models»](https://fabiofurini.github.io/network-optimization/flows/network-flow-models/) the matrix $\mat{M}$ is the incidence matrix without the row of node $6$; a basis has $n-1=5$ arcs.

    - The arcs $(1,2)$, $(2,4)$, $(3,2)$, $(4,6)$, $(5,4)$ give a $5 \times 5$ submatrix of $\mat{M}$ with determinant $1$: they form a basis.

    - The arcs $(1,2)$, $(2,4)$, $(3,2)$, $(4,3)$, $(5,6)$ touch every node, but they contain the cycle $2,4,3,2$: the columns of $(2,4)$, $(4,3)$, $(3,2)$ add up to zero, and the determinant is $0$.

    - Of the $126$ sets of $5$ arcs, exactly $55$ give a nonsingular submatrix, and they are the $55$ spanning trees of the reference graph. All these determinants are $1$ or $-1$.

!!! chiave ""

    In a connected network the equation of node $n$ is redundant. A basis is a set of $n-1$ arcs with linearly independent columns in $\mat{M}$; the nonbasic arcs are fixed at $0$ (set $L$) or at their capacity (set $U$), and the basic solution follows.

---

**Next:** [8.2 Bases and spanning trees](bases-and-spanning-trees.md)

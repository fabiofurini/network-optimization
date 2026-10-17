---
title: "Basic solutions"
---

# 7.2 Basic solutions { #sez-ta-sec-basic }

<div class="info-capitolo" markdown>

**Part 3 · Flows · Chapter 7** · [:material-book-open-variant: Chapter 7: Transportation and assignment](index.md) · [:material-file-pdf-box: Lecture notes, volume 3 (PDF)](../../pdf/lecture-notes-3-flows.pdf) · [:material-presentation: Slides](../../pdf/slides-transportation-and-assignment.pdf) · [:material-pencil: Exercises: Transportation and assignment](../../exercises/transportation-and-assignment.md) · [:material-gesture-tap: App: Transportation: initial solution and potentials method](../../lab/transportation-potentials-method.md) · [:material-gesture-tap: App: Assignment: the Hungarian algorithm](../../lab/assignment-hungarian-algorithm.md)

</div>

- The column of $x_{ij}$ in the constraints of the $\mathrm{TP}$ model has two entries equal to $1$, in the row of the supply of $i$ and in the row of the demand of $j$. Changing the sign of the demand rows gives the incidence matrix $\mat{B}$ of the complete bipartite network, and changes neither the rank nor the linear dependences of the columns.

<a id="box-7-ta-prop-rank"></a>

!!! teorema "Proposition 7.4: rank of the transportation model"

    The $m+n$ constraints of the $\mathrm{TP}$ model have rank $m+n-1$. In a balanced instance each constraint is implied by the others.

??? dimostrazione "Proof"

    Every origin is joined to every destination, so the complete bipartite network is connected, and its incidence matrix has rank $m+n-1$ by the Theorem «rank of the incidence matrix» of [Chapter 1](https://fabiofurini.github.io/network-optimization/graphs/graphs/the-rank-of-the-incidence-matrix/). The sum of the supply rows minus the sum of the demand rows is zero, since both sums contain every variable once, and the same combination of the right-hand sides is $\sum_{i \in P} a_i-\sum_{j \in D} d_j=0$: any constraint is a combination of the others. <span class="qed">□</span>

<a id="box-8-ta-def-basis"></a>

!!! definizione "Definition 7.5: basis and basic solution"

    A <strong>basis</strong> of the $\mathrm{TP}$ model is a set $T$ of $m+n-1$ cells whose arcs form a spanning tree of the complete bipartite network; its cells are the <strong>basic cells</strong>. A <strong>basic solution</strong> of $T$ is a solution of the constraints [(7.1b)](the-transportation-problem.md#mjx-eqn:ta:supply) and [(7.1c)](the-transportation-problem.md#mjx-eqn:ta:demand) with $x_{ij}=0$ for every cell outside $T$. It is a <strong>basic feasible solution</strong> if $\vet{x} \ge \vet{0}$, and it is <strong>degenerate</strong> if some basic cell has $x_{ij}=0$.

<a id="box-9-ta-th-basis"></a>

!!! teorema "Theorem 7.6: bases are spanning trees"

    - **(a)** A set of $m+n-1$ cells has linearly independent columns if and only if its arcs form a spanning tree.

    - **(b)** In a balanced instance, every basis $T$ has exactly one basic solution. It is found by fixing, again and again, the cell of a leaf of the tree, and it is integer when the supplies and the demands are integer.

??? dimostrazione "Proof"

    Part (a) is the Corollary «bases of the incidence matrix» of [Chapter 1](https://fabiofurini.github.io/network-optimization/graphs/graphs/the-rank-of-the-incidence-matrix/), since the sign of the demand rows does not change the dependences of the columns. For part (b):

    1. <em>Uniqueness.</em> Two basic solutions of $T$ differ by a vector $\vet{y}$ that is zero outside $T$ and satisfies the constraints with zero right-hand sides; the columns of $T$ are independent by (a), so $\vet{y}=\vet{0}$.

    2. <em>Construction.</em> The tree has a leaf $v$ (Lemma «leaves» of [Chapter 1](https://fabiofurini.github.io/network-optimization/graphs/graphs/trees-and-forests/)), with only one cell $e$ of $T$. The constraint of $v$ contains no other basic cell, so $x_e$ equals the supply or demand of $v$.

    3. We remove $v$ and $e$, and subtract $x_e$ from the supply or demand of the other endpoint of $e$. The remaining cells form a spanning tree of the remaining nodes, and the remaining supplies and demands still have equal sums.

    4. When a single cell is left, both its endpoints are leaves, and the equal sums give the same value for both constraints. Every value is obtained by sums and differences of the data, so it is integer for integer data. <span class="qed">□</span>

<a id="box-10-ta-prop-vertex"></a>

!!! teorema "Proposition 7.7: vertices are basic"

    Every vertex $\bar{\vet{x}}$ of the feasible region of the $\mathrm{TP}$ model is a basic feasible solution: its cells with $\bar{x}_{ij}>0$ form a forest, contained in a basis $T$, and $\bar{\vet{x}}$ is the basic solution of $T$.

??? dimostrazione "Proof"

    Let $F$ be the cells with $\bar{x}_{ij}>0$.

    1. The columns of $F$ are linearly independent, by the first step of the proof of the Theorem «integer vertices» of [Chapter 4](https://fabiofurini.github.io/network-optimization/flows/network-flow-models/total-unimodularity-and-integrality/): here the cells strictly between their bounds are those of $F$. A cycle has dependent columns (Lemma «columns of a cycle» of Chapter 1), so $F$ is a forest.

    2. The network is connected: while the forest has two or more components, some arc joins one of them to another one, and adding it creates no cycle (Lemma «adding an edge» of Chapter 1). We end with a spanning tree $T \supseteq F$.

    3. $\bar{\vet{x}}$ is zero outside $F \subseteq T$, so it is the basic solution of $T$, unique by <span style="color:#1971c2">[Theorem 7.6](#box-9-ta-th-basis)</span>. <span class="qed">□</span>

- A cycle of the bipartite network alternates origins and destinations. In the tableau it is a closed path through cells of the set, moving alternately along a row and along a column: a set of cells is a basis if it has $m+n-1$ cells and no such closed path.

- A basic feasible solution has at most $m+n-1$ positive amounts; it has fewer when it is degenerate.

<a id="box-11-ta-ex-bases"></a>

!!! esempio "Example 7.4: bases of the transportation instance"

    In <span style="color:#1971c2">[Example 7.1](the-transportation-problem.md#box-3-ta-ex-tp)</span> a basis has $m+n-1=3+4-1=6$ cells.

    - The cells $(1,4)$, $(1,5)$, $(2,4)$, $(2,5)$, $(3,6)$, $(3,7)$ are not a basis: $(1,4)$, $(2,4)$, $(2,5)$, $(1,5)$ form the cycle $1,4,2,5,1$, and indeed $\mat{A}_{14}-\mat{A}_{24}+\mat{A}_{25}-\mat{A}_{15}=\vet{0}$ for their columns $\mat{A}_{ij}$.

    - The cells $(1,4)$, $(1,5)$, $(1,6)$, $(1,7)$, $(2,7)$, $(3,7)$ form a spanning tree. Its leaves $2,3,4,5,6$ fix $x_{27}=30$, $x_{37}=30$, $x_{14}=10$, $x_{15}=25$, $x_{16}=15$; then the row of origin $1$ gives

        $$
        x_{17}=30-10-25-15=-20 .
        $$

        The basic solution exists, but it is not feasible.

!!! chiave ""

    The constraints of the $\mathrm{TP}$ model have rank $m+n-1$. A basis is a spanning tree of the bipartite network, with $m+n-1$ cells; its basic solution is found leaf by leaf, it is integer for integer data, and every vertex is a basic feasible solution.

---

**Next:** [7.3 Initial basic feasible solutions](initial-basic-feasible-solutions.md)

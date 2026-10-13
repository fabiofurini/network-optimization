---
title: "Total unimodularity and integrality"
---

# 4.6 Total unimodularity and integrality { #sez-sec-nf-tu }

<div class="info-capitolo" markdown>

**Part 3 · Flows · Chapter 4** · [:material-book-open-variant: Chapter 4: Flow models](index.md) · [:material-file-pdf-box: Lecture notes, volume 3 (PDF)](../../pdf/lecture-notes-3-flows.pdf) · [:material-pencil: Exercises: Flow models](../../exercises/network-flow-models.md)

</div>

<a id="box-18-nf-def-tu"></a>

!!! definizione "Definition 4.13: totally unimodular matrix"

    An integer matrix $\mat{M}$ is <strong>totally unimodular</strong> (TU) if the determinant of every square submatrix of $\mat{M}$ is $0$, $+1$ or $-1$. A square submatrix is obtained by choosing $k$ rows and $k$ columns, for any $k \ge 1$.

- With $k=1$ the definition requires every entry of a TU matrix to be $0$, $+1$ or $-1$.

<a id="box-19-nf-th-tu"></a>

!!! teorema "Theorem 4.14: the incidence matrix is totally unimodular"

    The node–arc incidence matrix $\mat{B}$ of every directed graph $G=(N,A)$ is totally unimodular.

??? dimostrazione "Proof"

    Let $\mat{M}$ be a $k \times k$ submatrix of $\mat{B}$; we prove $\det(\mat{M}) \in \{0,+1,-1\}$ by induction on $k$. For $k=1$ the entry is $0$, $+1$ or $-1$. Let $k \ge 2$. Every column of $\mat{B}$ has exactly one $+1$ and one $-1$, so every column of $\mat{M}$ has at most two nonzero entries; there are three cases.

    1. <em>A column of $\mat{M}$ is zero.</em> Then $\det(\mat{M})=0$.

    2. <em>A column of $\mat{M}$ has exactly one nonzero entry, $\pm 1$.</em> The Laplace expansion along this column gives $\det(\mat{M})=\pm\det(\mat{M}')$, where $\mat{M}'$ is a $(k-1) \times (k-1)$ submatrix of $\mat{B}$: by induction $\det(\mat{M}') \in \{0,+1,-1\}$.

    3. <em>Every column of $\mat{M}$ has two nonzero entries, $+1$ and $-1$.</em> Then the rows of $\mat{M}$ add up to the zero vector, they are linearly dependent, and $\det(\mat{M})=0$. <span class="qed">□</span>

<a id="box-20-nf-ex-tu"></a>

!!! esempio "Example 4.6: submatrices of the reference incidence matrix"

    We take rows $2,3,4$ of the incidence matrix $\mat{B}$ of the reference graph and two choices of three columns.

    $$
    \begin{array}{c|rrr}
    & a_1 & a_3 & a_5\\ \hline
    2 & -1 & 1 & 0\\
    3 & 0 & 0 & 1\\
    4 & 0 & -1 & 0
    \end{array}
    \qquad\qquad
    \begin{array}{c|rrr}
    & a_3 & a_4 & a_6\\ \hline
    2 & 1 & -1 & 0\\
    3 & 0 & 1 & -1\\
    4 & -1 & 0 & 1
    \end{array}
    $$

    - The column of $a_1=(1,2)$ in the first matrix has one nonzero entry (case 2): expanding along it, and then along the column of $a_5$, the determinant is $-1$.

    - The arcs $a_3=(2,4)$, $a_4=(3,2)$, $a_6=(4,3)$ of the second matrix form the cycle $2,4,3,2$, and all their endpoints are among the chosen rows: every column has $+1$ and $-1$ (case 3), and the determinant is $0$.

    - The matrix $\mat{B}$ has $5004$ square submatrices; computing all their determinants confirms that they take only the values $-1$, $0$ and $+1$.

## 4.6.1 Integer vertices

- A point $\bar{\vet{x}}$ of a polyhedron $P$ is a <strong>vertex</strong> if it is not the midpoint of two distinct points of $P$, as in [Chapter 15 «The geometry of Linear Programming»](https://fabiofurini.github.io/linear-programming/advanced-methods/15-geometry/) of the module Linear Programming.

- For a set of arcs $F$, we denote by $\mat{B}_F$ the submatrix of the columns of $F$, and by $\vet{x}_F$ the corresponding entries of $\vet{x}$.

<a id="box-21-nf-th-vertices"></a>

!!! teorema "Theorem 4.15: integer vertices"

    Let $G=(N,A)$ be a network with integer balances $\vet{b}$, integer lower bounds $\vet{l}$ and capacities $\vet{u}$ that are integer or $+\infty$. Then every vertex of

    $$
    P=\big\{\, \vet{x} \in \R^m : \mat{B}\vet{x}=\vet{b},~ \vet{l} \le \vet{x} \le \vet{u} \,\big\}
    $$

    is an integer vector.

??? dimostrazione "Proof"

    Let $\bar{\vet{x}}$ be a vertex of $P$, and let $F=\{\, a \in A : l_a<\bar{x}_a<u_a \,\}$ be the arcs strictly between their bounds. If $F=\emptyset$, every entry of $\bar{\vet{x}}$ is a bound, hence an integer.

    1. <em>The columns of $\mat{B}_F$ are linearly independent.</em> Otherwise $\mat{B}_F\vet{d}_F=\vet{0}$ for some $\vet{d} \neq \vet{0}$ with $d_a=0$ for $a \notin F$. For a small $\varepsilon>0$ both $\bar{\vet{x}}+\varepsilon \vet{d}$ and $\bar{\vet{x}}-\varepsilon\vet{d}$ satisfy the strict bounds on $F$ and $\mat{B}\vet{x}=\vet{b}$, so they lie in $P$, and $\bar{\vet{x}}$ is their midpoint: a contradiction.

    2. <em>The system for $\bar{\vet{x}}_F$ has integer data.</em> Every $a \notin F$ has $\bar{x}_a \in \{l_a,u_a\}$, an integer, so $\mat{B}_F\bar{\vet{x}}_F=\vet{b}-\sum_{a \notin F} \mat{B}_a\bar{x}_a=:\hat{\vet{b}}$ is integer.

    3. <em>Cramer's rule.</em> $\mat{B}_F$ has rank $|F|$, so some $|F|$ of its rows form a nonsingular square matrix $\mat{M}$, and $\mat{M}\bar{\vet{x}}_F=\hat{\vet{b}}_R$ on these rows $R$. By Cramer's rule each entry of $\bar{\vet{x}}_F$ is $\det(\mat{M}_a)/\det(\mat{M})$, with $\mat{M}_a$ an integer matrix.

    4. By <span style="color:#1971c2">[Theorem 4.14](#box-19-nf-th-tu)</span>, $\det(\mat{M})=\pm 1$, so every entry of $\bar{\vet{x}}_F$ is an integer. <span class="qed">□</span>

<a id="box-22-nf-cor-integral"></a>

!!! teorema "Corollary 4.16: integrality of the minimum cost flow model"

    Let the balances, the lower bounds and the capacities be integer, with every capacity finite. If the $\mathrm{MCF}$ model has a feasible solution, then it has an integer optimal solution, for any costs $\vet{c}$.

??? dimostrazione "Proof"

    The polyhedron $P$ is nonempty and bounded, since $\vet{l} \le \vet{x} \le \vet{u}$ with finite bounds. A linear function attains its minimum over a nonempty bounded polyhedron at a vertex ([Chapter 15 «The geometry of Linear Programming»](https://fabiofurini.github.io/linear-programming/advanced-methods/15-geometry/)), and every vertex of $P$ is integer by <span style="color:#1971c2">[Theorem 4.15](#box-21-nf-th-vertices)</span>. <span class="qed">□</span>

- The simplex algorithm ends at a vertex, so with integer data it returns an integer optimal flow: the integer requirement $x_{ij} \in \Z_{\ge 0}$ comes for free.

- Total unimodularity is a property of the matrix: for a matrix that is not TU, an integer right-hand side can give fractional vertices.

<a id="box-23-nf-ex-nottu"></a>

!!! esempio "Example 4.7: a matrix that is not totally unimodular"

    The undirected triangle with vertices $1,2,3$ and edges $e_1=\{1,2\}$, $e_2=\{1,3\}$, $e_3=\{2,3\}$ has the vertex–edge incidence matrix

    $$
    \mat{M}=\begin{pmatrix} 1 & 1 & 0\\ 1 & 0 & 1\\ 0 & 1 & 1 \end{pmatrix}, \qquad \det(\mat{M})=-2,
    $$

    so $\mat{M}$ is not TU. The polyhedron $\{\vet{y} \in \R^3 : \mat{M}\vet{y}=\vet{1},~ \vet{y} \ge \vet{0}\}$ contains the single point $\vet{y}=(\frac{1}{2},\frac{1}{2},\frac{1}{2})$, since $\mat{M}$ is nonsingular: this vertex is fractional, although the data are integer.

!!! chiave ""

    The incidence matrix of a directed graph is totally unimodular. Hence, with integer balances and bounds, every vertex of the feasible region is integer, and the $\mathrm{MCF}$ model has an integer optimal solution.

---

**Next:** [4.7 The dual model and the reduced costs](the-dual-model-and-the-reduced-costs.md)

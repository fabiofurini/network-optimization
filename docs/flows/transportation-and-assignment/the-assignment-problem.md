---
title: "The assignment problem"
---

# 7.5 The assignment problem

<div class="info-capitolo" markdown>

**Part 3 · Flows · Chapter 7** · [:material-book-open-variant: Chapter 7: Transportation and assignment](index.md) · [:material-file-pdf-box: Lecture notes, volume 3 (PDF)](../../pdf/lecture-notes-3-flows.pdf) · [:material-presentation: Slides](../../pdf/slides-transportation-and-assignment.pdf) · [:material-pencil: Exercises: Transportation and assignment](../../exercises/transportation-and-assignment.md) · [:material-gesture-tap: App: Transportation: initial solution and potentials method](../../lab/transportation-potentials-method.md) · [:material-gesture-tap: App: Assignment: the Hungarian algorithm](../../lab/assignment-hungarian-algorithm.md)

</div>

<a id="sez-ta-sec-assignment"></a>

<a id="box-22-ta-def-ap"></a>

!!! definizione "Definition 7.14: assignment problem"

    There are $n$ workers, the origins $P=\{1,2,\dots,n\}$, and $n$ jobs, the destinations $D=\{n+1,n+2,\dots,2n\}$; $c_{ij}$ is the cost of assigning worker $i$ to job $j$. An <strong>assignment</strong> gives every worker exactly one job and every job to exactly one worker. The <strong>assignment problem</strong> asks for an assignment of minimum total cost.

- We use one binary variable $x_{ij}$ for every pair $i \in P$, $j \in D$, equal to $1$ if worker $i$ gets job $j$.

!!! chiave ""

    Using these variables, an Integer Linear Programming (ILP) model for the assignment problem reads as follows:

    <a id="eq-ta-AP"></a>

    \begin{align*}
    &&   \min \;\;{\sum_{i \in P} \sum_{j \in D} c_{ij} \, x_{ij}}                                \label{ta:aobj}  \tag{7.3a}\\[1ex]
    && \text{subject to} \quad  \sum_{j \in D} x_{ij} &= 1, & \forall i \in P,                \label{ta:arow}  \tag{7.3b}\\[1ex]
    && \sum_{i \in P} x_{ij} &= 1, & \forall j \in D,                                        \label{ta:acol}  \tag{7.3c}\\[1ex]
    && x_{ij} &\in \{0,1\}, & \forall i \in P,~\forall j \in D.                               \label{ta:adom} \tag{7.3d}
    \end{align*}

    This model is referred to as the $\mathrm{AP}$ model.

- Description of the objective function and constraints of the $\mathrm{AP}$ model:

    - the objective function $\eqref{ta:aobj}$ minimizes the total cost of the assignment;

    - constraints $\eqref{ta:arow}$ give every worker exactly one job;

    - constraints $\eqref{ta:acol}$ give every job to exactly one worker;

    - finally, constraints $\eqref{ta:adom}$ define the binary variables of the model.

- An $n \times n$ matrix with entries in $\{0,1\}$ and exactly one $1$ in every row and in every column is a <strong>permutation matrix</strong>. The feasible solutions of the $\mathrm{AP}$ model are the permutation matrices: there are $n!$ assignments.

<a id="box-23-ta-prop-ap"></a>

!!! teorema "Proposition 7.15: the LP relaxation of the assignment model"

    The LP relaxation of the $\mathrm{AP}$ model, with $x_{ij} \ge 0$ in place of $\eqref{ta:adom}$, is the $\mathrm{TP}$ model with $a_i=1$ and $d_j=1$. Its vertices are permutation matrices, and it has an optimal solution that is an assignment.

??? dimostrazione "Proof"

    The constraints $\eqref{ta:arow}$ and $\eqref{ta:acol}$ are [(7.1b)](the-transportation-problem.md#mjx-eqn:ta:supply) and [(7.1c)](the-transportation-problem.md#mjx-eqn:ta:demand) with unit supplies and demands, and the instance is balanced, with total $n$. By <span style="color:#1971c2">[Proposition 7.2](the-transportation-problem.md#box-2-ta-prop-exist)</span> it has an optimal solution at a vertex, and every vertex is integer by the Theorem «integer vertices» of [Chapter 4](https://fabiofurini.github.io/network-optimization/flows/network-flow-models/total-unimodularity-and-integrality/). An integer feasible solution has $0 \le x_{ij} \le 1$, since $x_{ij}$ is at most the sum of its row: it is a permutation matrix. <span class="qed">□</span>

<a id="box-24-ta-ex-ap"></a>

!!! esempio "Example 7.9: four workers and four jobs"

    Four workers $1,2,3,4$ and four jobs $5,6,7,8$ have the costs

    $$
    \begin{array}{c|cccc}
    \hline {c_{ij}} & {5} & {6} & {7} & {8} \\
    \hline {1} & {2} & {4} & {3} & {5} \\
    {2} & {4} & {8} & {1} & {1} \\
    {3} & {2} & {6} & {9} & {6} \\
    {4} & {1} & {9} & {8} & {6} \\
    \hline
    \end{array}
    $$

    The $4!=24$ assignments, enumerated, have a unique minimum: worker $1$ gets job $7$, worker $2$ job $8$, worker $3$ job $6$, worker $4$ job $5$, with cost $3+1+6+1=11$. Gurobi gives the same assignment as the optimal solution of the LP relaxation.

### 7.5.1 Degeneracy of the potential method

- A basis of the LP relaxation has $2n-1$ cells, but an assignment has only $n$ cells with $x_{ij}=1$: every basic feasible solution has $n-1$ basic cells with value $0$, and it is degenerate.

- The potential method solves the LP relaxation, but many of its pivots have $\theta=0$. On <span style="color:#1971c2">[Example 7.9](#box-24-ta-ex-ap)</span> the north-west corner rule gives the basis below, with three basic zeros; from it the potential method reaches the optimum after $6$ pivots, $4$ of them degenerate.

<div class="tabella" markdown="0"><table>
<tr>
<th><span class="arithmatex">\(\bar{x}_{ij}\)</span></th>
<th><span class="arithmatex">\(5\)</span></th>
<th><span class="arithmatex">\(6\)</span></th>
<th><span class="arithmatex">\(7\)</span></th>
<th><span class="arithmatex">\(8\)</span></th>
<th><span class="arithmatex">\(a_i\)</span></th>
</tr>
<tr>
<td><span class="arithmatex">\(1\)</span></td>
<td class="cella-blu"><span class="arithmatex">\(1\)</span></td>
<td></td>
<td></td>
<td></td>
<td><span class="arithmatex">\(1\)</span></td>
</tr>
<tr>
<td><span class="arithmatex">\(2\)</span></td>
<td class="cella-blu"><span class="arithmatex">\(0\)</span></td>
<td class="cella-blu"><span class="arithmatex">\(1\)</span></td>
<td></td>
<td></td>
<td><span class="arithmatex">\(1\)</span></td>
</tr>
<tr>
<td><span class="arithmatex">\(3\)</span></td>
<td></td>
<td class="cella-blu"><span class="arithmatex">\(0\)</span></td>
<td class="cella-blu"><span class="arithmatex">\(1\)</span></td>
<td></td>
<td><span class="arithmatex">\(1\)</span></td>
</tr>
<tr>
<td><span class="arithmatex">\(4\)</span></td>
<td></td>
<td></td>
<td class="cella-blu"><span class="arithmatex">\(0\)</span></td>
<td class="cella-blu"><span class="arithmatex">\(1\)</span></td>
<td><span class="arithmatex">\(1\)</span></td>
</tr>
<tr>
<td><span class="arithmatex">\(d_j\)</span></td>
<td><span class="arithmatex">\(1\)</span></td>
<td><span class="arithmatex">\(1\)</span></td>
<td><span class="arithmatex">\(1\)</span></td>
<td><span class="arithmatex">\(1\)</span></td>
<td></td>
</tr>
</table></div>

### 7.5.2 Reductions and potentials

<a id="box-25-ta-lem-reduce"></a>

!!! teorema "Lemma 7.16: reduced costs of an assignment"

    For potentials $\vet{\pi}$, let $\bar{c}_{ij}=c_{ij}-\pi_i+\pi_j$. For every $\vet{x}$ that satisfies $\eqref{ta:arow}$ and $\eqref{ta:acol}$,

    $$
    \sum_{i \in P}\sum_{j \in D} c_{ij}\,x_{ij}=\sum_{i \in P}\sum_{j \in D} \bar{c}_{ij}\,x_{ij}+\sum_{i \in P}\pi_i-
    \sum_{j \in D}\pi_j .
    $$

    Hence subtracting a constant from a row or from a column of the cost matrix changes the cost of every assignment by the same constant, and the optimal assignments do not change.

??? dimostrazione "Proof"

    It is the identity of <span style="color:#1971c2">Section [7.4](the-potential-method.md#sez-ta-sec-potentials)</span> with $a_i=d_j=1$. Subtracting $r$ from row $i$ gives the reduced costs of $\pi_i=r$ and the other potentials $0$; subtracting $s$ from column $j$ those of $\pi_j=-s$. <span class="qed">□</span>

<a id="box-26-ta-cor-zero"></a>

!!! teorema "Corollary 7.17: zero-cost assignments are optimal"

    If $\bar{c}_{ij} \ge 0$ for every cell and an assignment uses only cells with $\bar{c}_{ij}=0$, then it is optimal, even for the LP relaxation, its cost is $\sum_{i \in P}\pi_i-\sum_{j \in D}\pi_j$, and $\vet{\pi}$ is optimal for the dual of the LP relaxation, the $D(\mathrm{TP})$ model with $a_i=d_j=1$.

??? dimostrazione "Proof"

    By <span style="color:#1971c2">[Lemma 7.16](#box-25-ta-lem-reduce)</span>, the assignment costs $\sum_{i \in P}\pi_i-\sum_{j \in D}\pi_j$, and every $\vet{x} \ge \vet{0}$ satisfying $\eqref{ta:arow}$ and $\eqref{ta:acol}$ costs at least as much, since $\bar{c} \ge 0$. The potentials satisfy $\pi_i-\pi_j \le c_{ij}$ with the same value, so they are optimal by weak duality. <span class="qed">□</span>

### 7.5.3 Independent zeros and lines

<a id="box-27-ta-def-cover"></a>

!!! definizione "Definition 7.18: independent zeros and covers"

    Let $\bar{c}$ be an $n \times n$ matrix with non-negative entries. A set of zero entries is <strong>independent</strong> if no two of them lie in the same row or in the same column. A set of <strong>lines</strong>, rows and columns, <strong>covers</strong> the zeros if every zero entry lies in at least one of the lines.

- $n$ independent zeros form an assignment of reduced cost zero, optimal by <span style="color:#1971c2">[Corollary 7.17](#box-26-ta-cor-zero)</span>.

- In the bipartite network whose arcs are the cells with $\bar{c}_{ij}=0$, a set of independent zeros is a matching, a set of arcs without common endpoints as in [Chapter 5 «Maximum flow»](https://fabiofurini.github.io/network-optimization/flows/maximum-flow/), and a cover is a set of nodes that touches every arc.

<a id="box-28-ta-th-konig"></a>

!!! teorema "Theorem 7.19: König and Egerváry"

    The maximum number of independent zeros of a matrix equals the minimum number of lines that cover all its zeros.

??? dimostrazione "Proof"

    Let $M$ be a maximum set of independent zeros. A row or a column is <strong>matched</strong> if it contains a zero of $M$.

    1. <em>Lines $\ge$ zeros.</em> The zeros of $M$ lie in different rows and columns, so a line contains at most one of them, and a cover needs at least $|M|$ lines.

    2. <em>Alternating paths.</em> An <strong>alternating path</strong> starts at an unmatched row, goes from a row to a column through a zero not in $M$, and from a column to a row through the zero of $M$ of that column. Let $R$ and $K$ be the rows and the columns reached by alternating paths, the unmatched rows included.

    3. <em>Every column of $K$ is matched.</em> Otherwise an alternating path ends at an unmatched column. Along it, the zeros not in $M$ are one more than the zeros of $M$: exchanging them gives an independent set with $|M|+1$ zeros, against the maximality of $M$.

    4. <em>The lines.</em> Let $L$ be the rows not in $R$ and the columns in $K$. A zero $(i,j)$ with row $i \in R$ has column $j \in K$: if it is not in $M$, a path to $i$ continues to $j$; if it is in $M$, row $i$ is matched, so it was reached from its column $j$. Hence $L$ covers all the zeros.

    5. <em>Counting.</em> The rows not in $R$ are matched, since the unmatched rows are in $R$, and the columns of $K$ are matched. A zero of $M$ in a column of $K$ has its row in $R$, so it lies on exactly one line of $L$. Lines and zeros of $M$ correspond one to one, and $|L|=|M|$. <span class="qed">□</span>

- The proof is constructive: it gives the lines of a minimum cover from a maximum set of independent zeros, and a set that is not maximum is enlarged along an alternating path ending at an unmatched column.

### 7.5.4 The Hungarian algorithm

!!! algoritmo "Algorithm: The Hungarian algorithm"

    <div class="pseudocodice" markdown="0"><div class="pc" style="--liv:0"><strong>Input:</strong> an <span class="arithmatex">\(n \times n\)</span> cost matrix <span class="arithmatex">\(c_{ij}\)</span>, <span class="arithmatex">\(i \in P\)</span>, <span class="arithmatex">\(j \in D\)</span></div><div class="pc" style="--liv:0"><strong>Output:</strong> an optimal assignment and optimal potentials <span class="arithmatex">\(\vet{\pi}\)</span></div><div class="pc" style="--liv:0"><span class="pc-n">1</span><strong>Step 0 (reduction).</strong> Subtract from each row its minimum, <span class="arithmatex">\(\pi_i\)</span>; then subtract from each column of the result
    its minimum, <span class="arithmatex">\(-\pi_j\)</span>. Let <span class="arithmatex">\(\bar{c}\)</span> be the reduced matrix.</div><div class="pc" style="--liv:0"><span class="pc-n">2</span><strong>Step 1 (independent zeros).</strong> Find a maximum set <span class="arithmatex">\(M\)</span> of independent zeros of <span class="arithmatex">\(\bar{c}\)</span>.</div><div class="pc" style="--liv:0"><span class="pc-n">3</span>  If <span class="arithmatex">\(|M|=n\)</span>, <code>STOP</code>: <span class="arithmatex">\(M\)</span> is an optimal assignment.</div><div class="pc" style="--liv:0"><span class="pc-n">4</span><strong>Step 2 (lines).</strong> Cover the zeros with <span class="arithmatex">\(|M|<n\)</span> lines, as in the proof of the theorem of König and Egerváry.</div><div class="pc" style="--liv:0"><span class="pc-n">5</span><strong>Step 3 (adjustment).</strong> Let <span class="arithmatex">\(\delta\)</span> be the minimum uncovered entry. Subtract <span class="arithmatex">\(\delta\)</span> from the uncovered
    entries and add it to the entries covered twice: <span class="arithmatex">\(\pi_i:=\pi_i+\delta\)</span> for every uncovered row, <span class="arithmatex">\(\pi_j:=\pi_j+\delta\)</span>
    for every covered column. Go to Step 1.</div></div>

- <strong>Rule of the examples.</strong> In Step 1 the set $M$ is built row by row, in increasing order: each row looks for an alternating path to an unmatched column, depth first, trying the columns in increasing order.

- The algorithm is due to H. W. Kuhn (1955), who named it after the Hungarian mathematicians D. König and J. Egerváry.

<a id="box-29-ta-th-hungarian"></a>

!!! teorema "Theorem 7.20: correctness of the Hungarian algorithm"

    At every iteration $\bar{c}_{ij}=c_{ij}-\pi_i+\pi_j \ge 0$ for every cell, and Step 3 increases the dual value $\sum_{i \in P}\pi_i-\sum_{j \in D}\pi_j$ by $\delta\,(n-k)>0$, where $k<n$ is the number of lines. With integer costs the algorithm stops after a finite number of iterations with an optimal assignment, and $\vet{\pi}$ is optimal for the dual of the LP relaxation.

??? dimostrazione "Proof"

    1. <em>Step 0.</em> Subtracting the minimum of a row leaves non-negative entries and a zero in the row; the column minima are then $\ge 0$, and subtracting them keeps the entries non-negative. By construction $\bar{c}_{ij}=c_{ij}- \pi_i+\pi_j$.

    2. <em>Step 3.</em> All zeros are covered, so $\delta>0$, and the uncovered entries stay $\ge 0$. The update of the potentials gives $-\delta$ on uncovered row and column, $-\delta+\delta=0$ on uncovered row and covered column, $+\delta$ on covered row and column, $0$ on covered row and uncovered column: exactly the adjustment.

    3. <em>Dual value.</em> With $k_r$ covered rows and $k_c$ covered columns, the value grows by $\delta\,(n-k_r)-\delta\,k_c=\delta\,(n-k)$, and $k=|M|<n$ by <span style="color:#1971c2">[Theorem 7.19](#box-28-ta-th-konig)</span>.

    4. <em>Termination.</em> By <span style="color:#1971c2">[Lemma 7.16](#box-25-ta-lem-reduce)</span> the dual value never exceeds the cost of an assignment. With integer costs every $\delta$ is an integer $\ge 1$, so the number of adjustments is finite. At the stop $M$ is an assignment of zeros, optimal with $\vet{\pi}$ by <span style="color:#1971c2">[Corollary 7.17](#box-26-ta-cor-zero)</span>. <span class="qed">□</span>

### 7.5.5 The Hungarian algorithm on the example

<a id="box-30-ta-ex-hungarian"></a>

!!! esempio "Example 7.10: the Hungarian algorithm"

    We run the algorithm on <span style="color:#1971c2">[Example 7.9](#box-24-ta-ex-ap)</span>.

    <strong>Step 0.</strong> The row minima are $2,1,2,1$, so $\pi_1=2$, $\pi_2=1$, $\pi_3=2$, $\pi_4=1$, and the rows become

    $$
    \begin{array}{c|cccc}
    \hline {c_{ij}-\pi_i} & {5} & {6} & {7} & {8} \\
    \hline {1} & {0} & {2} & {1} & {3} \\
    {2} & {3} & {7} & {0} & {0} \\
    {3} & {0} & {4} & {7} & {4} \\
    {4} & {0} & {8} & {7} & {5} \\
    \hline
    \end{array}
    $$

    The column minima are $0,2,0,0$: only column $6$ changes, and $\pi_6=-2$. The dual value $2+1+2+1+2=8$ is a lower bound on the cost of every assignment.

    In each of the following matrices the independent zeros are boxed, the lines blue and the cell of $\delta$ red; the potentials are on the margins.

    <div class="tabella" markdown="0"><table>
    <tr>
    <th colspan="6"><strong>Iteration 1</strong></th>
    </tr>
    <tr>
    <td><span class="arithmatex">\(\bar{c}_{ij}\)</span></td>
    <td><span class="arithmatex">\(5\)</span></td>
    <td><span class="arithmatex">\(6\)</span></td>
    <td><span class="arithmatex">\(7\)</span></td>
    <td><span class="arithmatex">\(8\)</span></td>
    <td><span class="arithmatex">\(\pi_i\)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">\(1\)</span></td>
    <td class="cella-blu"><span class="arithmatex">\(0\)</span></td>
    <td class="cella-blu"><span class="arithmatex">\(\boxed{0}\)</span></td>
    <td class="cella-blu"><span class="arithmatex">\(1\)</span></td>
    <td class="cella-blu"><span class="arithmatex">\(3\)</span></td>
    <td><span class="arithmatex">\(2\)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">\(2\)</span></td>
    <td class="cella-blu"><span class="arithmatex">\(3\)</span></td>
    <td class="cella-blu"><span class="arithmatex">\(5\)</span></td>
    <td class="cella-blu"><span class="arithmatex">\(\boxed{0}\)</span></td>
    <td class="cella-blu"><span class="arithmatex">\(0\)</span></td>
    <td><span class="arithmatex">\(1\)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">\(3\)</span></td>
    <td class="cella-blu"><span class="arithmatex">\(\boxed{0}\)</span></td>
    <td class="cella-rossa"><span class="arithmatex">\(2\)</span></td>
    <td><span class="arithmatex">\(7\)</span></td>
    <td><span class="arithmatex">\(4\)</span></td>
    <td><span class="arithmatex">\(2\)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">\(4\)</span></td>
    <td class="cella-blu"><span class="arithmatex">\(0\)</span></td>
    <td><span class="arithmatex">\(6\)</span></td>
    <td><span class="arithmatex">\(7\)</span></td>
    <td><span class="arithmatex">\(5\)</span></td>
    <td><span class="arithmatex">\(1\)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">\(\pi_j\)</span></td>
    <td><span class="arithmatex">\(0\)</span></td>
    <td><span class="arithmatex">\(-2\)</span></td>
    <td><span class="arithmatex">\(0\)</span></td>
    <td><span class="arithmatex">\(0\)</span></td>
    <td></td>
    </tr>
    </table></div>

    - A maximum set of independent zeros (boxed) has $3$ elements: $(1,6)$, $(2,7)$, $(3,5)$.

    - The $3<4$ lines (blue) are the rows $1$ and $2$ and the column $5$.

    - The minimum uncovered entry is $\delta=2$, in the cell $(3,6)$ (red). We subtract it from the uncovered entries and add it to the entries covered twice: $\pi_i$ grows by $2$ for the uncovered rows $3$ and $4$ and $\pi_j$ grows by $2$ for the covered column $5$. The dual value grows by $2\cdot(4-3)=2$.

    <div class="tabella" markdown="0"><table>
    <tr>
    <th colspan="6"><strong>Iteration 2</strong></th>
    </tr>
    <tr>
    <td><span class="arithmatex">\(\bar{c}_{ij}\)</span></td>
    <td><span class="arithmatex">\(5\)</span></td>
    <td><span class="arithmatex">\(6\)</span></td>
    <td><span class="arithmatex">\(7\)</span></td>
    <td><span class="arithmatex">\(8\)</span></td>
    <td><span class="arithmatex">\(\pi_i\)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">\(1\)</span></td>
    <td class="cella-blu"><span class="arithmatex">\(2\)</span></td>
    <td class="cella-blu"><span class="arithmatex">\(\boxed{0}\)</span></td>
    <td class="cella-rossa"><span class="arithmatex">\(1\)</span></td>
    <td><span class="arithmatex">\(3\)</span></td>
    <td><span class="arithmatex">\(2\)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">\(2\)</span></td>
    <td class="cella-blu"><span class="arithmatex">\(5\)</span></td>
    <td class="cella-blu"><span class="arithmatex">\(5\)</span></td>
    <td class="cella-blu"><span class="arithmatex">\(\boxed{0}\)</span></td>
    <td class="cella-blu"><span class="arithmatex">\(0\)</span></td>
    <td><span class="arithmatex">\(1\)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">\(3\)</span></td>
    <td class="cella-blu"><span class="arithmatex">\(\boxed{0}\)</span></td>
    <td class="cella-blu"><span class="arithmatex">\(0\)</span></td>
    <td><span class="arithmatex">\(5\)</span></td>
    <td><span class="arithmatex">\(2\)</span></td>
    <td><span class="arithmatex">\(4\)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">\(4\)</span></td>
    <td class="cella-blu"><span class="arithmatex">\(0\)</span></td>
    <td class="cella-blu"><span class="arithmatex">\(4\)</span></td>
    <td><span class="arithmatex">\(5\)</span></td>
    <td><span class="arithmatex">\(3\)</span></td>
    <td><span class="arithmatex">\(3\)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">\(\pi_j\)</span></td>
    <td><span class="arithmatex">\(2\)</span></td>
    <td><span class="arithmatex">\(-2\)</span></td>
    <td><span class="arithmatex">\(0\)</span></td>
    <td><span class="arithmatex">\(0\)</span></td>
    <td></td>
    </tr>
    </table></div>

    - A maximum set of independent zeros (boxed) has $3$ elements: $(1,6)$, $(2,7)$, $(3,5)$.

    - The $3<4$ lines (blue) are the row $2$ and the columns $5$ and $6$.

    - The minimum uncovered entry is $\delta=1$, in the cell $(1,7)$ (red). We subtract it from the uncovered entries and add it to the entries covered twice: $\pi_i$ grows by $1$ for the uncovered rows $1$, $3$ and $4$ and $\pi_j$ grows by $1$ for the covered columns $5$ and $6$. The dual value grows by $1\cdot(4-3)=1$.

    <div class="tabella" markdown="0"><table>
    <tr>
    <th colspan="6"><strong>Iteration 3</strong></th>
    </tr>
    <tr>
    <td><span class="arithmatex">\(\bar{c}_{ij}\)</span></td>
    <td><span class="arithmatex">\(5\)</span></td>
    <td><span class="arithmatex">\(6\)</span></td>
    <td><span class="arithmatex">\(7\)</span></td>
    <td><span class="arithmatex">\(8\)</span></td>
    <td><span class="arithmatex">\(\pi_i\)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">\(1\)</span></td>
    <td class="cella-blu"><span class="arithmatex">\(2\)</span></td>
    <td class="cella-blu"><span class="arithmatex">\(0\)</span></td>
    <td class="cella-blu"><span class="arithmatex">\(\boxed{0}\)</span></td>
    <td class="cella-blu"><span class="arithmatex">\(2\)</span></td>
    <td><span class="arithmatex">\(3\)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">\(2\)</span></td>
    <td class="cella-blu"><span class="arithmatex">\(6\)</span></td>
    <td class="cella-blu"><span class="arithmatex">\(6\)</span></td>
    <td class="cella-blu"><span class="arithmatex">\(0\)</span></td>
    <td class="cella-blu"><span class="arithmatex">\(\boxed{0}\)</span></td>
    <td><span class="arithmatex">\(1\)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">\(3\)</span></td>
    <td class="cella-blu"><span class="arithmatex">\(0\)</span></td>
    <td class="cella-blu"><span class="arithmatex">\(\boxed{0}\)</span></td>
    <td class="cella-blu"><span class="arithmatex">\(4\)</span></td>
    <td class="cella-blu"><span class="arithmatex">\(1\)</span></td>
    <td><span class="arithmatex">\(5\)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">\(4\)</span></td>
    <td class="cella-blu"><span class="arithmatex">\(\boxed{0}\)</span></td>
    <td class="cella-blu"><span class="arithmatex">\(4\)</span></td>
    <td class="cella-blu"><span class="arithmatex">\(4\)</span></td>
    <td class="cella-blu"><span class="arithmatex">\(2\)</span></td>
    <td><span class="arithmatex">\(4\)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">\(\pi_j\)</span></td>
    <td><span class="arithmatex">\(3\)</span></td>
    <td><span class="arithmatex">\(-1\)</span></td>
    <td><span class="arithmatex">\(0\)</span></td>
    <td><span class="arithmatex">\(0\)</span></td>
    <td></td>
    </tr>
    </table></div>

    - A maximum set of independent zeros (boxed) has $4$ elements: $(1,7)$, $(2,8)$, $(3,6)$, $(4,5)$.

    - They form an assignment of zero reduced cost: the algorithm stops, and the assignment is optimal.

- The optimal assignment is $1 \to 7$, $2 \to 8$, $3 \to 6$, $4 \to 5$, with cost $3+1+6+1=11$, the unique optimum of <span style="color:#1971c2">[Example 7.9](#box-24-ta-ex-ap)</span>.

- The final potentials $\pi_1=3$, $\pi_2=1$, $\pi_3=5$, $\pi_4=4$ and $\pi_5=3$, $\pi_6=-1$, $\pi_7=0$, $\pi_8=0$ are an optimal dual solution, of value $(3+1+5+4)-(3-1+0+0)=11$. The dual value grew from $8$ to $10$ and then to $11$.

- The lines are those of the proof of <span style="color:#1971c2">[Theorem 7.19](#box-28-ta-th-konig)</span>. In iteration $1$ row $4$ is unmatched; from it an alternating path reaches column $5$ through its zero, and then row $3$, matched to column $5$. Hence $R=\{3,4\}$, $K=\{5\}$, and the lines are the rows $1$, $2$ and the column $5$.

!!! chiave ""

    The assignment problem is a transportation problem with unit supplies and demands, on which the potential method makes many degenerate pivots. The Hungarian algorithm keeps $\bar{c}_{ij}=c_{ij}-\pi_i+\pi_j \ge 0$, covers the zeros with the minimum number of lines (König–Egerváry), and raises the dual value until $n$ independent zeros give an optimal assignment.

## 7.6 Typical mistakes

!!! attenzione "Warning"

    - <strong>Solving an unbalanced instance as it is.</strong> With more supply than demand the equality constraints have no solution: add a dummy destination with zero costs, or a dummy origin when the demand exceeds the supply.

    - <strong>Dropping a basic zero.</strong> A degenerate basis still has $m+n-1$ cells; without the cell of value $0$ the tree is disconnected and the potentials cannot be computed.

    - <strong>Taking a set with a cycle as a basis.</strong> $m+n-1$ cells are a basis only if they contain no closed path alternating rows and columns.

    - <strong>Mixing the sign conventions.</strong> Here $\bar{c}_{ij}=c_{ij}-\pi_i+\pi_j$ with $\pi_i-\pi_j=c_{ij}$ on the basic cells; with $u_i+v_j=c_{ij}$ the destination potentials change sign.

    - <strong>Computing $\theta$ on all the cells of the cycle.</strong> $\theta$ is the minimum on the cells with sign $-$ only; the entering cell receives $\theta$.

    - <strong>Covering the zeros with too many lines.</strong> The lines of the Hungarian algorithm must be a minimum cover, as many as the independent zeros; with more lines $\delta$ may be wrong or the stop missed.

    - <strong>Forgetting the entries covered twice.</strong> In Step 3 of the Hungarian algorithm $\delta$ is subtracted from the uncovered entries and added to those covered by a row and a column.

    - <strong>Running the algorithms on profits.</strong> They minimize: with profits $p_{ij}$ to maximize, use the costs $c_{ij}=-p_{ij}$, or $c_{ij}=p_{\max}-p_{ij}$ with $p_{\max}$ the largest profit, to keep them non-negative.

## 7.7 In summary

!!! chiave "In summary"

    - The $\mathrm{TP}$ model ships the supplies $a_i$ of $m$ origins to the demands $d_j$ of $n$ destinations; it is an $\mathrm{MCF}$ model on the complete bipartite network, feasible exactly when it is balanced.

    - An uncapacitated transshipment instance becomes a transportation instance with the distances as costs.

    - A basis is a spanning tree of the bipartite network, with $m+n-1$ cells; its basic solution is found leaf by leaf and is integer for integer data.

    - The north-west corner and the minimum cost rules build a basic feasible solution, one line per step.

    - The potential method: potentials with $\bar{c}_{ij}=0$ on the basis and $\pi_{m+n}=0$; optimal when $\bar{c} \ge 0$; otherwise $\theta$ units move around the cycle of the entering cell, and the cost drops by $\theta\,|\bar{c}_e|$.

    - The $\mathrm{AP}$ model is a $\mathrm{TP}$ model with unit data; the Hungarian algorithm reduces rows and columns, covers the zeros with a minimum number of lines (König–Egerváry) and adjusts by $\delta$, raising the dual value.

    <strong>The instances at a glance.</strong>

    <div class="tabella" markdown="0"><table>
    <tr>
    <td>warehouses and stores</td>
    <td>north-west <span class="arithmatex">\(440\)</span>, minimum cost <span class="arithmatex">\(170\)</span>, optimum <span class="arithmatex">\(165\)</span></td>
    </tr>
    <tr>
    <td>potential method</td>
    <td><span class="arithmatex">\(4\)</span> pivots from north-west, <span class="arithmatex">\(1\)</span> from minimum cost</td>
    </tr>
    <tr>
    <td>optimal potentials</td>
    <td><span class="arithmatex">\(\tilde{\vet{\pi}}=(3,2,5,2,4,1,0)\)</span>, with <span class="arithmatex">\(\pi_7=0\)</span></td>
    </tr>
    <tr>
    <td>with <span class="arithmatex">\(a_1=40\)</span></td>
    <td>dummy destination <span class="arithmatex">\(8\)</span>, optimum <span class="arithmatex">\(155\)</span></td>
    </tr>
    <tr>
    <td>degenerate instance</td>
    <td><span class="arithmatex">\(\theta=0\)</span>, then <span class="arithmatex">\(\theta=5\)</span>; optimum <span class="arithmatex">\(235\)</span></td>
    </tr>
    <tr>
    <td>transshipment, no capacities</td>
    <td>optimum <span class="arithmatex">\(49\)</span></td>
    </tr>
    <tr>
    <td>workers and jobs</td>
    <td>bound <span class="arithmatex">\(8\)</span>, <span class="arithmatex">\(\delta=2\)</span>, <span class="arithmatex">\(\delta=1\)</span>, optimum <span class="arithmatex">\(11\)</span></td>
    </tr>
    </table></div>

---

**Exercises on this chapter:** [:material-pencil: Transportation and assignment](../../exercises/transportation-and-assignment.md)


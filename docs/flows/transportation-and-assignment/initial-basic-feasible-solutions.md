---
title: "Initial basic feasible solutions"
---

# 7.3 Initial basic feasible solutions { #sez-ta-sec-initial }

<div class="info-capitolo" markdown>

**Part 3 · Flows · Chapter 7** · [:material-book-open-variant: Chapter 7: Transportation and assignment](index.md) · [:material-file-pdf-box: Lecture notes, volume 3 (PDF)](../../pdf/lecture-notes-3-flows.pdf) · [:material-pencil: Exercises: Transportation and assignment](../../exercises/transportation-and-assignment.md)

</div>

- A basic feasible solution is built by filling the tableau one cell at a time. A row or a column is <strong>active</strong> until it is crossed out; the residual supply $\bar{a}_i$ and the residual demand $\bar{d}_j$ are what is left to ship and to receive.

- The two rules below differ only in the choice of the next cell.

!!! algoritmo "Algorithm: Initial basic feasible solution"

    <div class="pseudocodice" markdown="0"><div class="pc" style="--liv:0"><strong>Input:</strong> a balanced instance with supplies <span class="arithmatex">\(a_i\)</span>, demands <span class="arithmatex">\(d_j\)</span> and costs <span class="arithmatex">\(c_{ij}\)</span></div><div class="pc" style="--liv:0"><strong>Output:</strong> a basis <span class="arithmatex">\(T\)</span> and its basic feasible solution <span class="arithmatex">\(\bar{\vet{x}}\)</span></div><div class="pc" style="--liv:0"><span class="pc-n">1</span><strong>Step 0 (initialization).</strong> All rows and columns are active; <span class="arithmatex">\(\bar{a}_i:=a_i\)</span>, <span class="arithmatex">\(\bar{d}_j:=d_j\)</span>, <span class="arithmatex">\(T:=\emptyset\)</span>.</div><div class="pc" style="--liv:0"><span class="pc-n">2</span><strong>Step 1 (choice of the cell).</strong> Choose a cell <span class="arithmatex">\((i,j)\)</span> with active row and column:</div><div class="pc" style="--liv:0"><span class="pc-n">3</span>  <em>north-west corner rule</em>: the cell with the smallest <span class="arithmatex">\(i\)</span> and the smallest <span class="arithmatex">\(j\)</span>;</div><div class="pc" style="--liv:0"><span class="pc-n">4</span>  <em>minimum cost rule</em>: the cell with the smallest <span class="arithmatex">\(c_{ij}\)</span> (the smallest <span class="arithmatex">\(i\)</span>, then <span class="arithmatex">\(j\)</span>, on ties).</div><div class="pc" style="--liv:0"><span class="pc-n">5</span><strong>Step 2 (amount).</strong> Set <span class="arithmatex">\(\bar{x}_{ij}:=\min\{\bar{a}_i,\bar{d}_j\}\)</span>, add <span class="arithmatex">\((i,j)\)</span> to <span class="arithmatex">\(T\)</span>, and subtract
    <span class="arithmatex">\(\bar{x}_{ij}\)</span> from <span class="arithmatex">\(\bar{a}_i\)</span> and from <span class="arithmatex">\(\bar{d}_j\)</span>.</div><div class="pc" style="--liv:0"><span class="pc-n">6</span><strong>Step 3 (crossing out).</strong> If <span class="arithmatex">\(\bar{a}_i=0\)</span> and another row is active, cross out row <span class="arithmatex">\(i\)</span>; otherwise cross out
    column <span class="arithmatex">\(j\)</span>.</div><div class="pc" style="--liv:0"><span class="pc-n">7</span>  If no column is active, <code>STOP</code>; otherwise go to Step 1.</div></div>

- When $\bar{a}_i=\bar{d}_j=0$ at the same time, only the row is crossed out: the column stays active with residual demand $0$, and a later cell of that column gets the amount $0$. This basic cell with value $0$ keeps $T$ a spanning tree, and the solution is degenerate.

<a id="box-12-ta-th-initial"></a>

!!! teorema "Theorem 7.8: the initial solution is basic"

    With either rule, the algorithm «Initial basic feasible solution» stops after $m+n-1$ steps, and $T$ is a basis with basic feasible solution $\bar{\vet{x}}$.

??? dimostrazione "Proof"

    1. <em>Invariant.</em> The residual supplies of the active rows and the residual demands of the active columns have equal sums: true at the start, and Step 2 subtracts the same amount from both sides.

    2. <em>A crossed line has residual $0$.</em> A crossed row has $\bar{a}_i=0$. A column is crossed when $\bar{a}_i>0$, and then $\bar{x}_{ij}=\bar{d}_j$ and $\bar{d}_j=0$, or when row $i$ is the only active row with $\bar{a}_i=0$, and then every active column has residual $0$ by the invariant.

    3. <em>Counting.</em> A row is crossed out only if another row is active, so one row $r$ is never crossed out, and the algorithm stops when the $n$ columns are crossed out. At the stop the active rows have residual $0$ by the invariant, and a row that reaches $0$ without being crossed out is the only active row. Hence the steps are $(m-1)+n=m+n-1$, one cell each, all different, since a cell is chosen in two active lines and one of them is then crossed out.

    4. <em>Feasibility.</em> At the stop every row and every column has residual $0$, so $\bar{\vet{x}} \ge \vet{0}$ satisfies all the constraints.

    5. <em>Tree.</em> Let $L_t$ be the line crossed at step $t$: no later cell lies in $L_t$. Backwards from the last step, the cells of steps $t,t+1,\dots$ form a tree: the cell of step $t$ joins the new node $L_t$ to its other line, which is still active, hence a node of the later cells or the row $r$. At $t=1$ the tree spans all the $m+n$ nodes. <span class="qed">□</span>

## 7.3.1 The north-west corner rule

<a id="box-13-ta-ex-nw"></a>

!!! esempio "Example 7.5: the north-west corner rule"

    On <span style="color:#1971c2">[Example 7.1](the-transportation-problem.md#box-3-ta-ex-tp)</span> the north-west corner rule starts at the cell $(1,4)$ and moves right or down. Its steps are:

    <div class="tabella" markdown="0"><table>
    <tr>
    <th>step</th>
    <th>cell</th>
    <th>amount</th>
    <th>crossed out</th>
    </tr>
    <tr>
    <td><span class="arithmatex">\(1\)</span></td>
    <td><span class="arithmatex">\((1,4)\)</span></td>
    <td><span class="arithmatex">\(10\)</span></td>
    <td>column <span class="arithmatex">\(4\)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">\(2\)</span></td>
    <td><span class="arithmatex">\((1,5)\)</span></td>
    <td><span class="arithmatex">\(20\)</span></td>
    <td>row <span class="arithmatex">\(1\)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">\(3\)</span></td>
    <td><span class="arithmatex">\((2,5)\)</span></td>
    <td><span class="arithmatex">\(5\)</span></td>
    <td>column <span class="arithmatex">\(5\)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">\(4\)</span></td>
    <td><span class="arithmatex">\((2,6)\)</span></td>
    <td><span class="arithmatex">\(15\)</span></td>
    <td>column <span class="arithmatex">\(6\)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">\(5\)</span></td>
    <td><span class="arithmatex">\((2,7)\)</span></td>
    <td><span class="arithmatex">\(10\)</span></td>
    <td>row <span class="arithmatex">\(2\)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">\(6\)</span></td>
    <td><span class="arithmatex">\((3,7)\)</span></td>
    <td><span class="arithmatex">\(30\)</span></td>
    <td>row <span class="arithmatex">\(3\)</span>, column <span class="arithmatex">\(7\)</span></td>
    </tr>
    </table></div>

    The basic feasible solution, with the basic cells in blue, is

    <div class="tabella" markdown="0"><table>
    <tr>
    <th><span class="arithmatex">\(\bar{x}_{ij}\)</span></th>
    <th><span class="arithmatex">\(4\)</span></th>
    <th><span class="arithmatex">\(5\)</span></th>
    <th><span class="arithmatex">\(6\)</span></th>
    <th><span class="arithmatex">\(7\)</span></th>
    <th><span class="arithmatex">\(a_i\)</span></th>
    </tr>
    <tr>
    <td><span class="arithmatex">\(1\)</span></td>
    <td class="cella-blu"><span class="arithmatex">\(10\)</span></td>
    <td class="cella-blu"><span class="arithmatex">\(20\)</span></td>
    <td></td>
    <td></td>
    <td><span class="arithmatex">\(30\)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">\(2\)</span></td>
    <td></td>
    <td class="cella-blu"><span class="arithmatex">\(5\)</span></td>
    <td class="cella-blu"><span class="arithmatex">\(15\)</span></td>
    <td class="cella-blu"><span class="arithmatex">\(10\)</span></td>
    <td><span class="arithmatex">\(30\)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">\(3\)</span></td>
    <td></td>
    <td></td>
    <td></td>
    <td class="cella-blu"><span class="arithmatex">\(30\)</span></td>
    <td><span class="arithmatex">\(30\)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">\(d_j\)</span></td>
    <td><span class="arithmatex">\(10\)</span></td>
    <td><span class="arithmatex">\(25\)</span></td>
    <td><span class="arithmatex">\(15\)</span></td>
    <td><span class="arithmatex">\(40\)</span></td>
    <td></td>
    </tr>
    </table></div>

    Its cost is

    $$
    1 \cdot 10+9 \cdot 20+4 \cdot 5+2 \cdot 15+2 \cdot 10+6 \cdot 30=440 .
    $$

    The six basic cells form the spanning tree below, with the amounts on the arcs.

    ![Figure 3](../../img/transportation-and-assignment/fig03.svg){ .fig loading=lazy  }

- The north-west corner rule ignores the costs: on this instance it ships $20$ units on the cell $(1,5)$, of cost $9$, and $30$ units on $(3,7)$, of cost $6$.

## 7.3.2 The minimum cost rule

<a id="box-14-ta-ex-mc"></a>

!!! esempio "Example 7.6: the minimum cost rule"

    On <span style="color:#1971c2">[Example 7.1](the-transportation-problem.md#box-3-ta-ex-tp)</span> the minimum cost rule chooses, at every step, the cheapest cell of the active rows and columns:

    <div class="tabella" markdown="0"><table>
    <tr>
    <th>step</th>
    <th>cell</th>
    <th>amount</th>
    <th>crossed out</th>
    </tr>
    <tr>
    <td><span class="arithmatex">\(1\)</span></td>
    <td><span class="arithmatex">\((1,4)\)</span></td>
    <td><span class="arithmatex">\(10\)</span></td>
    <td>column <span class="arithmatex">\(4\)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">\(2\)</span></td>
    <td><span class="arithmatex">\((3,5)\)</span></td>
    <td><span class="arithmatex">\(25\)</span></td>
    <td>column <span class="arithmatex">\(5\)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">\(3\)</span></td>
    <td><span class="arithmatex">\((1,6)\)</span></td>
    <td><span class="arithmatex">\(15\)</span></td>
    <td>column <span class="arithmatex">\(6\)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">\(4\)</span></td>
    <td><span class="arithmatex">\((2,7)\)</span></td>
    <td><span class="arithmatex">\(30\)</span></td>
    <td>row <span class="arithmatex">\(2\)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">\(5\)</span></td>
    <td><span class="arithmatex">\((1,7)\)</span></td>
    <td><span class="arithmatex">\(5\)</span></td>
    <td>row <span class="arithmatex">\(1\)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">\(6\)</span></td>
    <td><span class="arithmatex">\((3,7)\)</span></td>
    <td><span class="arithmatex">\(5\)</span></td>
    <td>row <span class="arithmatex">\(3\)</span>, column <span class="arithmatex">\(7\)</span></td>
    </tr>
    </table></div>

    - At step $1$ the cells $(1,4)$ and $(3,5)$ both cost $1$, and $(1,4)$ goes first, since its row is smaller. At step $3$ the cells $(1,6)$, $(2,6)$, $(2,7)$ cost $2$, and $(1,6)$ goes first.

    - At step $4$ only column $7$ is active: it takes the whole supply of row $2$, then $5$ units from row $1$ and $5$ from row $3$.

    The basic feasible solution is

    <div class="tabella" markdown="0"><table>
    <tr>
    <th><span class="arithmatex">\(\bar{x}_{ij}\)</span></th>
    <th><span class="arithmatex">\(4\)</span></th>
    <th><span class="arithmatex">\(5\)</span></th>
    <th><span class="arithmatex">\(6\)</span></th>
    <th><span class="arithmatex">\(7\)</span></th>
    <th><span class="arithmatex">\(a_i\)</span></th>
    </tr>
    <tr>
    <td><span class="arithmatex">\(1\)</span></td>
    <td class="cella-blu"><span class="arithmatex">\(10\)</span></td>
    <td></td>
    <td class="cella-blu"><span class="arithmatex">\(15\)</span></td>
    <td class="cella-blu"><span class="arithmatex">\(5\)</span></td>
    <td><span class="arithmatex">\(30\)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">\(2\)</span></td>
    <td></td>
    <td></td>
    <td></td>
    <td class="cella-blu"><span class="arithmatex">\(30\)</span></td>
    <td><span class="arithmatex">\(30\)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">\(3\)</span></td>
    <td></td>
    <td class="cella-blu"><span class="arithmatex">\(25\)</span></td>
    <td></td>
    <td class="cella-blu"><span class="arithmatex">\(5\)</span></td>
    <td><span class="arithmatex">\(30\)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">\(d_j\)</span></td>
    <td><span class="arithmatex">\(10\)</span></td>
    <td><span class="arithmatex">\(25\)</span></td>
    <td><span class="arithmatex">\(15\)</span></td>
    <td><span class="arithmatex">\(40\)</span></td>
    <td></td>
    </tr>
    </table></div>

    with cost

    $$
    1 \cdot 10+2 \cdot 15+3 \cdot 5+2 \cdot 30+1 \cdot 25+6 \cdot 5=170 .
    $$

!!! chiave ""

    Filling one cell per step and crossing out one line per step gives a basic feasible solution with $m+n-1$ basic cells. The north-west corner rule ignores the costs; the minimum cost rule usually starts much closer to the optimum ($170$ instead of $440$ on the example).

---

**Next:** [7.4 The potential method](the-potential-method.md)

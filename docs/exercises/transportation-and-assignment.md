---
title: "Exercises · Transportation and assignment"
---

# Exercises · Transportation and assignment

<div class="info-capitolo" markdown>

**Exercises · Chapter 7** · each solution opens with a click · [:material-book-open-variant: Chapter 7: Transportation and assignment](../flows/transportation-and-assignment/index.md) · [:material-file-pdf-box: Exercises, volume 3 (PDF)](../pdf/exercises-3-flows.pdf)

</div>

!!! formula "Rules used in these exercises"

    The definitions and the results of the chapter [«Transportation and assignment»](https://fabiofurini.github.io/network-optimization/flows/transportation-and-assignment/). The origins are $1,2,\dots,m$ with supplies $a_i$, the destinations $m+1,m+2,\dots,m+n$ with demands $d_j$, and the cells $(i,j)$ are taken in row–column order.

    - **(F1)** <strong>Model.</strong> $\min \sum_{i}\sum_{j} c_{ij}x_{ij}$ with row sums $a_i$, column sums $d_j$ and $\vet{x} \ge \vet{0}$; feasible if and only if $\sum_i a_i=\sum_j d_j$. An excess of supply goes to a dummy destination with costs $0$.

    - **(F2)** <strong>Bases.</strong> A basis is a set of $m+n-1$ cells forming a spanning tree of the bipartite network (no closed path alternating rows and columns). Its basic solution is found leaf by leaf; it is degenerate if a basic cell has value $0$.

    - **(F3)** <strong>Initial solutions.</strong> North-west corner: the active cell with the smallest row and column. Minimum cost: the cheapest active cell, the smallest $i$ and then $j$ on ties. The amount is $\min\{\bar{a}_i,\bar{d}_j\}$; if $\bar{a}_i=0$ and another row is active, the row is crossed out, otherwise the column.

    - **(F4)** <strong>Potential method.</strong> $\pi_i-\pi_j=c_{ij}$ on the basic cells, $\pi_{m+n}=0$; $\bar{c}_{ij}=c_{ij}-\pi_i+\pi_j$. Optimal if $\bar{c} \ge 0$, unique if $\bar{c}_{ij}>0$ outside the basis. Otherwise the most negative $\bar{c}_e$ enters (ties: smallest $i$, then $j$); the cycle starts at $e$ along its row with signs $+,-,+,\dots$; $\theta$ is the minimum on the cells $-$, and the first of them with $\bar{x}=\theta$ in row–column order leaves; the cost changes by $\theta\,\bar{c}_e$.

    - **(F5)** <strong>Hungarian algorithm.</strong> Subtract the row minima ($\pi_i$) and then the column minima ($-\pi_j$). Find a maximum set of independent zeros (row by row, alternating paths, columns in increasing order); if it has $n$ zeros, stop. Otherwise the lines are the rows not reached and the columns reached by alternating paths from the unmatched rows; $\delta$ is the minimum uncovered entry, subtracted from the uncovered entries and added to those covered twice ($\pi_i \mathrel{+}=\delta$ on uncovered rows, $\pi_j \mathrel{+}=\delta$ on covered columns). The dual value $\sum_i\pi_i-\sum_j\pi_j$ grows by $\delta\,(n-k)$ with $k$ lines.

<a id="esercizio-7-1"></a>

!!! esercizio "Exercise 7.1: Initial basic feasible solutions"

    !!! esercizio "Exercise"

        Three plants $1,2,3$ supply $a_1=30$, $a_2=40$, $a_3=20$ units of a product, and three customers $4,5,6$ demand $d_4=15$, $d_5=25$, $d_6=40$ units. Every demand must be met, and every plant ships at most its supply. The unit shipping costs are:

        $$
        \begin{array}{c|ccc|c}
        \hline {c_{ij}} & {4} & {5} & {6} & {a_i} \\
        \hline {1} & {7} & {4} & {7} & {30} \\
        {2} & {1} & {6} & {8} & {40} \\
        {3} & {9} & {9} & {6} & {20} \\
        \hline {d_j} & {15} & {25} & {40} &  \\
        \hline
        \end{array}
        $$

    **Questions**

    1. Is the instance balanced? Add a dummy destination as in (F1) and write the transportation tableau.

    2. Build an initial basic feasible solution with the north-west corner rule: list the steps, write the solution in the tableau and compute its cost.

    3. Build an initial basic feasible solution with the minimum cost rule, and compare the two costs.

    4. Check that both solutions have $m+n-1$ basic cells forming a spanning tree. How much supply does each plant leave unused in the two solutions?

??? soluzione "Solution"

    We use the rules (F1)–(F5) of the box at the beginning of these exercises.

    1. The total supply is $30+40+20=90$ and the total demand is $15+25+40=80$: the instance is not balanced, with an excess of $10$ units. We add the dummy destination $7$ with demand $d_{7}=10$ and costs $c_{17}=c_{27}=c_{37}=0$:

        $$
        \begin{array}{c|cccc|c}
        \hline {c_{ij}} & {4} & {5} & {6} & {7} & {a_i} \\
        \hline {1} & {7} & {4} & {7} & {0} & {30} \\
        {2} & {1} & {6} & {8} & {0} & {40} \\
        {3} & {9} & {9} & {6} & {0} & {20} \\
        \hline {d_j} & {15} & {25} & {40} & {10} & {90} \\
        \hline
        \end{array}
        $$

    2. The steps of the north-west corner rule are

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
        <td><span class="arithmatex">\(15\)</span></td>
        <td>column <span class="arithmatex">\(4\)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">\(2\)</span></td>
        <td><span class="arithmatex">\((1,5)\)</span></td>
        <td><span class="arithmatex">\(15\)</span></td>
        <td>row <span class="arithmatex">\(1\)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">\(3\)</span></td>
        <td><span class="arithmatex">\((2,5)\)</span></td>
        <td><span class="arithmatex">\(10\)</span></td>
        <td>column <span class="arithmatex">\(5\)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">\(4\)</span></td>
        <td><span class="arithmatex">\((2,6)\)</span></td>
        <td><span class="arithmatex">\(30\)</span></td>
        <td>row <span class="arithmatex">\(2\)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">\(5\)</span></td>
        <td><span class="arithmatex">\((3,6)\)</span></td>
        <td><span class="arithmatex">\(10\)</span></td>
        <td>column <span class="arithmatex">\(6\)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">\(6\)</span></td>
        <td><span class="arithmatex">\((3,7)\)</span></td>
        <td><span class="arithmatex">\(10\)</span></td>
        <td>row <span class="arithmatex">\(3\)</span>, column <span class="arithmatex">\(7\)</span></td>
        </tr>
        </table></div>

        and the solution is

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
        <td class="cella-blu"><span class="arithmatex">\(15\)</span></td>
        <td class="cella-blu"><span class="arithmatex">\(15\)</span></td>
        <td></td>
        <td></td>
        <td><span class="arithmatex">\(30\)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">\(2\)</span></td>
        <td></td>
        <td class="cella-blu"><span class="arithmatex">\(10\)</span></td>
        <td class="cella-blu"><span class="arithmatex">\(30\)</span></td>
        <td></td>
        <td><span class="arithmatex">\(40\)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">\(3\)</span></td>
        <td></td>
        <td></td>
        <td class="cella-blu"><span class="arithmatex">\(10\)</span></td>
        <td class="cella-blu"><span class="arithmatex">\(10\)</span></td>
        <td><span class="arithmatex">\(20\)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">\(d_j\)</span></td>
        <td><span class="arithmatex">\(15\)</span></td>
        <td><span class="arithmatex">\(25\)</span></td>
        <td><span class="arithmatex">\(40\)</span></td>
        <td><span class="arithmatex">\(10\)</span></td>
        <td></td>
        </tr>
        </table></div>

        Its cost is $7 \cdot 15+4 \cdot 15+6 \cdot 10+8 \cdot 30+6 \cdot 10+0 \cdot 10=525$.

    3. The steps of the minimum cost rule are

        <div class="tabella" markdown="0"><table>
        <tr>
        <th>step</th>
        <th>cell</th>
        <th>amount</th>
        <th>crossed out</th>
        </tr>
        <tr>
        <td><span class="arithmatex">\(1\)</span></td>
        <td><span class="arithmatex">\((1,7)\)</span></td>
        <td><span class="arithmatex">\(10\)</span></td>
        <td>column <span class="arithmatex">\(7\)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">\(2\)</span></td>
        <td><span class="arithmatex">\((2,4)\)</span></td>
        <td><span class="arithmatex">\(15\)</span></td>
        <td>column <span class="arithmatex">\(4\)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">\(3\)</span></td>
        <td><span class="arithmatex">\((1,5)\)</span></td>
        <td><span class="arithmatex">\(20\)</span></td>
        <td>row <span class="arithmatex">\(1\)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">\(4\)</span></td>
        <td><span class="arithmatex">\((2,5)\)</span></td>
        <td><span class="arithmatex">\(5\)</span></td>
        <td>column <span class="arithmatex">\(5\)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">\(5\)</span></td>
        <td><span class="arithmatex">\((3,6)\)</span></td>
        <td><span class="arithmatex">\(20\)</span></td>
        <td>row <span class="arithmatex">\(3\)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">\(6\)</span></td>
        <td><span class="arithmatex">\((2,6)\)</span></td>
        <td><span class="arithmatex">\(20\)</span></td>
        <td>row <span class="arithmatex">\(2\)</span>, column <span class="arithmatex">\(6\)</span></td>
        </tr>
        </table></div>

        At step $1$ the three dummy cells cost $0$, and the rule takes $(1,7)$, the smallest row. The solution is

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
        <td></td>
        <td class="cella-blu"><span class="arithmatex">\(20\)</span></td>
        <td></td>
        <td class="cella-blu"><span class="arithmatex">\(10\)</span></td>
        <td><span class="arithmatex">\(30\)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">\(2\)</span></td>
        <td class="cella-blu"><span class="arithmatex">\(15\)</span></td>
        <td class="cella-blu"><span class="arithmatex">\(5\)</span></td>
        <td class="cella-blu"><span class="arithmatex">\(20\)</span></td>
        <td></td>
        <td><span class="arithmatex">\(40\)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">\(3\)</span></td>
        <td></td>
        <td></td>
        <td class="cella-blu"><span class="arithmatex">\(20\)</span></td>
        <td></td>
        <td><span class="arithmatex">\(20\)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">\(d_j\)</span></td>
        <td><span class="arithmatex">\(15\)</span></td>
        <td><span class="arithmatex">\(25\)</span></td>
        <td><span class="arithmatex">\(40\)</span></td>
        <td><span class="arithmatex">\(10\)</span></td>
        <td></td>
        </tr>
        </table></div>

        Its cost is $4 \cdot 20+0 \cdot 10+1 \cdot 15+6 \cdot 5+8 \cdot 20+6 \cdot 20=405$, lower than the $525$ of the north-west corner rule.

    4. Each rule makes $m+n-1=3+4-1=6$ steps, one cell per step; the cells form a spanning tree because the crossed line of each step contains no later cell. The flow on the dummy column is the unused supply: with the north-west corner rule plant $1$ keeps $0$, plant $2$ keeps $0$ and plant $3$ keeps $10$; with the minimum cost rule plant $1$ keeps $10$, plant $2$ keeps $0$ and plant $3$ keeps $0$.

    !!! chiave ""

        With the dummy destination $7$ ($d_{7}=10$, zero costs) the north-west corner rule costs $525$ and the minimum cost rule $405$.

<a id="esercizio-7-2"></a>

!!! esercizio "Exercise 7.2: The potential method"

    !!! esercizio "Exercise"

        We consider the transportation instance with origins $1,2,3$, destinations $4,5,6,7$, and the costs, supplies and demands of the tableau:

        $$
        \begin{array}{c|cccc|c}
        \hline {c_{ij}} & {4} & {5} & {6} & {7} & {a_i} \\
        \hline {1} & {4} & {6} & {8} & {8} & {30} \\
        {2} & {2} & {2} & {7} & {7} & {15} \\
        {3} & {8} & {7} & {3} & {2} & {25} \\
        \hline {d_j} & {15} & {5} & {45} & {5} & {70} \\
        \hline
        \end{array}
        $$

    **Questions**

    1. Build the initial basic feasible solution with the north-west corner rule and compute its cost.

    2. Compute the potentials of its basis ($\pi_7=0$) and the reduced costs. Is the solution optimal?

    3. Run the potential method until the optimal solution, with the rules of (F4).

    4. Write the optimal potentials and check that the value of the dual model equals the optimal cost. Is the optimal solution unique?

??? soluzione "Solution"

    We use the rules (F1)–(F5) of the box at the beginning of these exercises.

    1. The north-west corner rule gives

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
        <td><span class="arithmatex">\(15\)</span></td>
        <td>column <span class="arithmatex">\(4\)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">\(2\)</span></td>
        <td><span class="arithmatex">\((1,5)\)</span></td>
        <td><span class="arithmatex">\(5\)</span></td>
        <td>column <span class="arithmatex">\(5\)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">\(3\)</span></td>
        <td><span class="arithmatex">\((1,6)\)</span></td>
        <td><span class="arithmatex">\(10\)</span></td>
        <td>row <span class="arithmatex">\(1\)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">\(4\)</span></td>
        <td><span class="arithmatex">\((2,6)\)</span></td>
        <td><span class="arithmatex">\(15\)</span></td>
        <td>row <span class="arithmatex">\(2\)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">\(5\)</span></td>
        <td><span class="arithmatex">\((3,6)\)</span></td>
        <td><span class="arithmatex">\(20\)</span></td>
        <td>column <span class="arithmatex">\(6\)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">\(6\)</span></td>
        <td><span class="arithmatex">\((3,7)\)</span></td>
        <td><span class="arithmatex">\(5\)</span></td>
        <td>row <span class="arithmatex">\(3\)</span>, column <span class="arithmatex">\(7\)</span></td>
        </tr>
        </table></div>

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
        <td class="cella-blu"><span class="arithmatex">\(15\)</span></td>
        <td class="cella-blu"><span class="arithmatex">\(5\)</span></td>
        <td class="cella-blu"><span class="arithmatex">\(10\)</span></td>
        <td></td>
        <td><span class="arithmatex">\(30\)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">\(2\)</span></td>
        <td></td>
        <td></td>
        <td class="cella-blu"><span class="arithmatex">\(15\)</span></td>
        <td></td>
        <td><span class="arithmatex">\(15\)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">\(3\)</span></td>
        <td></td>
        <td></td>
        <td class="cella-blu"><span class="arithmatex">\(20\)</span></td>
        <td class="cella-blu"><span class="arithmatex">\(5\)</span></td>
        <td><span class="arithmatex">\(25\)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">\(d_j\)</span></td>
        <td><span class="arithmatex">\(15\)</span></td>
        <td><span class="arithmatex">\(5\)</span></td>
        <td><span class="arithmatex">\(45\)</span></td>
        <td><span class="arithmatex">\(5\)</span></td>
        <td></td>
        </tr>
        </table></div>

        with cost $4 \cdot 15+6 \cdot 5+8 \cdot 10+7 \cdot 15+3 \cdot 20+2 \cdot 5=345$.

    2. From $\pi_7=0$ along the basic cells: $\pi_{1}=7,\ \pi_{2}=6,\ \pi_{3}=2,\ \pi_{4}=3,\ \pi_{5}=1,\ \pi_{6}=-1,\ \pi_{7}=0$. The reduced costs of the non-basic cells are in the first tableau of the next answer; $\bar{c}_{25}=-3$ and $\bar{c}_{24}=-1$ are negative, so the solution is not optimal.

    3. The tableaux contain the amounts of the basic cells (blue, bold) and the reduced costs of the other cells; the potentials are on the margins. <br><strong>Iteration 1</strong><br> Potentials: $\pi_{1}=7,\ \pi_{2}=6,\ \pi_{3}=2,\ \pi_{4}=3,\ \pi_{5}=1,\ \pi_{6}=-1,\ \pi_{7}=0$.

        <div class="tabella" markdown="0"><table>
        <tr>
        <th></th>
        <th><span class="arithmatex">\(4\)</span></th>
        <th><span class="arithmatex">\(5\)</span></th>
        <th><span class="arithmatex">\(6\)</span></th>
        <th><span class="arithmatex">\(7\)</span></th>
        <th><span class="arithmatex">\(\pi_i\)</span></th>
        </tr>
        <tr>
        <td><span class="arithmatex">\(1\)</span></td>
        <td class="cella-blu"><span class="arithmatex">\(\mathbf{15}\)</span></td>
        <td class="cella-blu"><span class="arithmatex">\(\mathbf{5}\,\ominus\)</span></td>
        <td class="cella-blu"><span class="arithmatex">\(\mathbf{10}\,\oplus\)</span></td>
        <td><span class="arithmatex">\(1\)</span></td>
        <td><span class="arithmatex">\(7\)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">\(2\)</span></td>
        <td><span class="arithmatex">\(-1\)</span></td>
        <td class="cella-rossa"><span class="arithmatex">\(-3\,\oplus\)</span></td>
        <td class="cella-blu"><span class="arithmatex">\(\mathbf{15}\,\ominus\)</span></td>
        <td><span class="arithmatex">\(1\)</span></td>
        <td><span class="arithmatex">\(6\)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">\(3\)</span></td>
        <td><span class="arithmatex">\(9\)</span></td>
        <td><span class="arithmatex">\(6\)</span></td>
        <td class="cella-blu"><span class="arithmatex">\(\mathbf{20}\)</span></td>
        <td class="cella-blu"><span class="arithmatex">\(\mathbf{5}\)</span></td>
        <td><span class="arithmatex">\(2\)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">\(\pi_j\)</span></td>
        <td><span class="arithmatex">\(3\)</span></td>
        <td><span class="arithmatex">\(1\)</span></td>
        <td><span class="arithmatex">\(-1\)</span></td>
        <td><span class="arithmatex">\(0\)</span></td>
        <td></td>
        </tr>
        </table></div>

        - The negative reduced costs are $\bar{c}_{25}=-3$, $\bar{c}_{24}=-1$; the cell $(2,5)$ enters the basis.

        - The cycle is $\,(2,5)^{+},\ (2,6)^{-},\ (1,6)^{+},\ (1,5)^{-}$.

        - The cells with sign $-$ have $\bar{x}_{26}=15$ and $\bar{x}_{15}=5$: $\theta=5$, and the cell $(1,5)$ leaves the basis.

        - The cost goes from $345$ to $345+5\cdot(-3)=330$.

        <strong>Iteration 2</strong><br> Potentials: $\pi_{1}=7,\ \pi_{2}=6,\ \pi_{3}=2,\ \pi_{4}=3,\ \pi_{5}=4,\ \pi_{6}=-1,\ \pi_{7}=0$.

        <div class="tabella" markdown="0"><table>
        <tr>
        <th></th>
        <th><span class="arithmatex">\(4\)</span></th>
        <th><span class="arithmatex">\(5\)</span></th>
        <th><span class="arithmatex">\(6\)</span></th>
        <th><span class="arithmatex">\(7\)</span></th>
        <th><span class="arithmatex">\(\pi_i\)</span></th>
        </tr>
        <tr>
        <td><span class="arithmatex">\(1\)</span></td>
        <td class="cella-blu"><span class="arithmatex">\(\mathbf{15}\,\ominus\)</span></td>
        <td><span class="arithmatex">\(3\)</span></td>
        <td class="cella-blu"><span class="arithmatex">\(\mathbf{15}\,\oplus\)</span></td>
        <td><span class="arithmatex">\(1\)</span></td>
        <td><span class="arithmatex">\(7\)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">\(2\)</span></td>
        <td class="cella-rossa"><span class="arithmatex">\(-1\,\oplus\)</span></td>
        <td class="cella-blu"><span class="arithmatex">\(\mathbf{5}\)</span></td>
        <td class="cella-blu"><span class="arithmatex">\(\mathbf{10}\,\ominus\)</span></td>
        <td><span class="arithmatex">\(1\)</span></td>
        <td><span class="arithmatex">\(6\)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">\(3\)</span></td>
        <td><span class="arithmatex">\(9\)</span></td>
        <td><span class="arithmatex">\(9\)</span></td>
        <td class="cella-blu"><span class="arithmatex">\(\mathbf{20}\)</span></td>
        <td class="cella-blu"><span class="arithmatex">\(\mathbf{5}\)</span></td>
        <td><span class="arithmatex">\(2\)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">\(\pi_j\)</span></td>
        <td><span class="arithmatex">\(3\)</span></td>
        <td><span class="arithmatex">\(4\)</span></td>
        <td><span class="arithmatex">\(-1\)</span></td>
        <td><span class="arithmatex">\(0\)</span></td>
        <td></td>
        </tr>
        </table></div>

        - The only negative reduced cost is $\bar{c}_{24}=-1$: the cell $(2,4)$ enters the basis.

        - The cycle is $\,(2,4)^{+},\ (2,6)^{-},\ (1,6)^{+},\ (1,4)^{-}$.

        - The cells with sign $-$ have $\bar{x}_{26}=10$ and $\bar{x}_{14}=15$: $\theta=10$, and the cell $(2,6)$ leaves the basis.

        - The cost goes from $330$ to $330+10\cdot(-1)=320$.

        <strong>Iteration 3</strong><br> Potentials: $\pi_{1}=7,\ \pi_{2}=5,\ \pi_{3}=2,\ \pi_{4}=3,\ \pi_{5}=3,\ \pi_{6}=-1,\ \pi_{7}=0$.

        <div class="tabella" markdown="0"><table>
        <tr>
        <th></th>
        <th><span class="arithmatex">\(4\)</span></th>
        <th><span class="arithmatex">\(5\)</span></th>
        <th><span class="arithmatex">\(6\)</span></th>
        <th><span class="arithmatex">\(7\)</span></th>
        <th><span class="arithmatex">\(\pi_i\)</span></th>
        </tr>
        <tr>
        <td><span class="arithmatex">\(1\)</span></td>
        <td class="cella-blu"><span class="arithmatex">\(\mathbf{5}\)</span></td>
        <td><span class="arithmatex">\(2\)</span></td>
        <td class="cella-blu"><span class="arithmatex">\(\mathbf{25}\)</span></td>
        <td><span class="arithmatex">\(1\)</span></td>
        <td><span class="arithmatex">\(7\)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">\(2\)</span></td>
        <td class="cella-blu"><span class="arithmatex">\(\mathbf{10}\)</span></td>
        <td class="cella-blu"><span class="arithmatex">\(\mathbf{5}\)</span></td>
        <td><span class="arithmatex">\(1\)</span></td>
        <td><span class="arithmatex">\(2\)</span></td>
        <td><span class="arithmatex">\(5\)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">\(3\)</span></td>
        <td><span class="arithmatex">\(9\)</span></td>
        <td><span class="arithmatex">\(8\)</span></td>
        <td class="cella-blu"><span class="arithmatex">\(\mathbf{20}\)</span></td>
        <td class="cella-blu"><span class="arithmatex">\(\mathbf{5}\)</span></td>
        <td><span class="arithmatex">\(2\)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">\(\pi_j\)</span></td>
        <td><span class="arithmatex">\(3\)</span></td>
        <td><span class="arithmatex">\(3\)</span></td>
        <td><span class="arithmatex">\(-1\)</span></td>
        <td><span class="arithmatex">\(0\)</span></td>
        <td></td>
        </tr>
        </table></div>

        - All the reduced costs are non-negative: the basic feasible solution is optimal, with cost $z=320$.

    4. The optimal potentials are $\pi_{1}=7,\ \pi_{2}=5,\ \pi_{3}=2,\ \pi_{4}=3,\ \pi_{5}=3,\ \pi_{6}=-1,\ \pi_{7}=0$, and the dual value is

        $$
        \sum_{i} a_i\pi_i-\sum_{j} d_j\pi_j=335-15=320,
        $$

        equal to the optimal cost. Every non-basic cell has $\bar{c}_{ij}>0$, so the optimal solution is unique.

    !!! chiave ""

        From the north-west corner (cost $345$) the potential method makes $2$ pivots and reaches the unique optimum $\tilde{x}_{14}=5$, $\tilde{x}_{16}=25$, $\tilde{x}_{24}=10$, $\tilde{x}_{25}=5$, $\tilde{x}_{36}=20$, $\tilde{x}_{37}=5$, with cost $320$.

<a id="esercizio-7-3"></a>

!!! esercizio "Exercise 7.3: Degeneracy"

    !!! esercizio "Exercise"

        We consider the transportation instance with origins $1,2,3$ and destinations $4,5,6$:

        $$
        \begin{array}{c|ccc|c}
        \hline {c_{ij}} & {4} & {5} & {6} & {a_i} \\
        \hline {1} & {7} & {3} & {7} & {20} \\
        {2} & {5} & {3} & {1} & {10} \\
        {3} & {6} & {7} & {8} & {25} \\
        \hline {d_j} & {10} & {10} & {35} & {55} \\
        \hline
        \end{array}
        $$

    **Questions**

    1. Build the north-west corner solution. At which step are a row and a column exhausted at the same time? Which basic cell has value $0$, and why must it stay in the basis?

    2. Run the potential method from this solution, with the rules of (F4).

    3. Which pivot is degenerate, and what changes in it? Give the optimal solution and its cost.

??? soluzione "Solution"

    We use the rules (F1)–(F5) of the box at the beginning of these exercises.

    1. The north-west corner rule gives

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
        <td><span class="arithmatex">\(10\)</span></td>
        <td>row <span class="arithmatex">\(1\)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">\(3\)</span></td>
        <td><span class="arithmatex">\((2,5)\)</span></td>
        <td><span class="arithmatex">\(0\)</span></td>
        <td>column <span class="arithmatex">\(5\)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">\(4\)</span></td>
        <td><span class="arithmatex">\((2,6)\)</span></td>
        <td><span class="arithmatex">\(10\)</span></td>
        <td>row <span class="arithmatex">\(2\)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">\(5\)</span></td>
        <td><span class="arithmatex">\((3,6)\)</span></td>
        <td><span class="arithmatex">\(25\)</span></td>
        <td>row <span class="arithmatex">\(3\)</span>, column <span class="arithmatex">\(6\)</span></td>
        </tr>
        </table></div>

        At step $2$ the cell $(1,5)$ exhausts both row $1$ and column $5$. Only the row is crossed out, and the next cell $(2,5)$ of column $5$ gets the amount $0$:

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">\(\bar{x}_{ij}\)</span></th>
        <th><span class="arithmatex">\(4\)</span></th>
        <th><span class="arithmatex">\(5\)</span></th>
        <th><span class="arithmatex">\(6\)</span></th>
        <th><span class="arithmatex">\(a_i\)</span></th>
        </tr>
        <tr>
        <td><span class="arithmatex">\(1\)</span></td>
        <td class="cella-blu"><span class="arithmatex">\(10\)</span></td>
        <td class="cella-blu"><span class="arithmatex">\(10\)</span></td>
        <td></td>
        <td><span class="arithmatex">\(20\)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">\(2\)</span></td>
        <td></td>
        <td class="cella-blu"><span class="arithmatex">\(0\)</span></td>
        <td class="cella-blu"><span class="arithmatex">\(10\)</span></td>
        <td><span class="arithmatex">\(10\)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">\(3\)</span></td>
        <td></td>
        <td></td>
        <td class="cella-blu"><span class="arithmatex">\(25\)</span></td>
        <td><span class="arithmatex">\(25\)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">\(d_j\)</span></td>
        <td><span class="arithmatex">\(10\)</span></td>
        <td><span class="arithmatex">\(10\)</span></td>
        <td><span class="arithmatex">\(35\)</span></td>
        <td></td>
        </tr>
        </table></div>

        The solution, of cost $310$, is degenerate. The basis needs $m+n-1=5$ cells: without $(2,5)$ the other cells do not span the $6$ nodes, and the potentials cannot be computed.

    2. <strong>Iteration 1</strong><br> Potentials: $\pi_{1}=1,\ \pi_{2}=1,\ \pi_{3}=8,\ \pi_{4}=-6,\ \pi_{5}=-2,\ \pi_{6}=0$.

        <div class="tabella" markdown="0"><table>
        <tr>
        <th></th>
        <th><span class="arithmatex">\(4\)</span></th>
        <th><span class="arithmatex">\(5\)</span></th>
        <th><span class="arithmatex">\(6\)</span></th>
        <th><span class="arithmatex">\(\pi_i\)</span></th>
        </tr>
        <tr>
        <td><span class="arithmatex">\(1\)</span></td>
        <td class="cella-blu"><span class="arithmatex">\(\mathbf{10}\,\ominus\)</span></td>
        <td class="cella-blu"><span class="arithmatex">\(\mathbf{10}\,\oplus\)</span></td>
        <td><span class="arithmatex">\(6\)</span></td>
        <td><span class="arithmatex">\(1\)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">\(2\)</span></td>
        <td><span class="arithmatex">\(-2\)</span></td>
        <td class="cella-blu"><span class="arithmatex">\(\mathbf{0}\,\ominus\)</span></td>
        <td class="cella-blu"><span class="arithmatex">\(\mathbf{10}\,\oplus\)</span></td>
        <td><span class="arithmatex">\(1\)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">\(3\)</span></td>
        <td class="cella-rossa"><span class="arithmatex">\(-8\,\oplus\)</span></td>
        <td><span class="arithmatex">\(-3\)</span></td>
        <td class="cella-blu"><span class="arithmatex">\(\mathbf{25}\,\ominus\)</span></td>
        <td><span class="arithmatex">\(8\)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">\(\pi_j\)</span></td>
        <td><span class="arithmatex">\(-6\)</span></td>
        <td><span class="arithmatex">\(-2\)</span></td>
        <td><span class="arithmatex">\(0\)</span></td>
        <td></td>
        </tr>
        </table></div>

        - The negative reduced costs are $\bar{c}_{34}=-8$, $\bar{c}_{35}=-3$, $\bar{c}_{24}=-2$; the cell $(3,4)$ enters the basis.

        - The cycle is $\,(3,4)^{+},\ (3,6)^{-},\ (2,6)^{+},\ (2,5)^{-},\ (1,5)^{+},\ (1,4)^{-}$.

        - The cells with sign $-$ have $\bar{x}_{36}=25$, $\bar{x}_{25}=0$ and $\bar{x}_{14}=10$: $\theta=0$, and the cell $(2,5)$ leaves the basis.

        - The pivot is degenerate: the solution and its cost $z=310$ do not change, only the basis does.

        <strong>Iteration 2</strong><br> Potentials: $\pi_{1}=9,\ \pi_{2}=1,\ \pi_{3}=8,\ \pi_{4}=2,\ \pi_{5}=6,\ \pi_{6}=0$.

        <div class="tabella" markdown="0"><table>
        <tr>
        <th></th>
        <th><span class="arithmatex">\(4\)</span></th>
        <th><span class="arithmatex">\(5\)</span></th>
        <th><span class="arithmatex">\(6\)</span></th>
        <th><span class="arithmatex">\(\pi_i\)</span></th>
        </tr>
        <tr>
        <td><span class="arithmatex">\(1\)</span></td>
        <td class="cella-blu"><span class="arithmatex">\(\mathbf{10}\,\ominus\)</span></td>
        <td class="cella-blu"><span class="arithmatex">\(\mathbf{10}\)</span></td>
        <td class="cella-rossa"><span class="arithmatex">\(-2\,\oplus\)</span></td>
        <td><span class="arithmatex">\(9\)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">\(2\)</span></td>
        <td><span class="arithmatex">\(6\)</span></td>
        <td><span class="arithmatex">\(8\)</span></td>
        <td class="cella-blu"><span class="arithmatex">\(\mathbf{10}\)</span></td>
        <td><span class="arithmatex">\(1\)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">\(3\)</span></td>
        <td class="cella-blu"><span class="arithmatex">\(\mathbf{0}\,\oplus\)</span></td>
        <td><span class="arithmatex">\(5\)</span></td>
        <td class="cella-blu"><span class="arithmatex">\(\mathbf{25}\,\ominus\)</span></td>
        <td><span class="arithmatex">\(8\)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">\(\pi_j\)</span></td>
        <td><span class="arithmatex">\(2\)</span></td>
        <td><span class="arithmatex">\(6\)</span></td>
        <td><span class="arithmatex">\(0\)</span></td>
        <td></td>
        </tr>
        </table></div>

        - The only negative reduced cost is $\bar{c}_{16}=-2$: the cell $(1,6)$ enters the basis.

        - The cycle is $\,(1,6)^{+},\ (1,4)^{-},\ (3,4)^{+},\ (3,6)^{-}$.

        - The cells with sign $-$ have $\bar{x}_{14}=10$ and $\bar{x}_{36}=25$: $\theta=10$, and the cell $(1,4)$ leaves the basis.

        - The cost goes from $310$ to $310+10\cdot(-2)=290$.

        <strong>Iteration 3</strong><br> Potentials: $\pi_{1}=7,\ \pi_{2}=1,\ \pi_{3}=8,\ \pi_{4}=2,\ \pi_{5}=4,\ \pi_{6}=0$.

        <div class="tabella" markdown="0"><table>
        <tr>
        <th></th>
        <th><span class="arithmatex">\(4\)</span></th>
        <th><span class="arithmatex">\(5\)</span></th>
        <th><span class="arithmatex">\(6\)</span></th>
        <th><span class="arithmatex">\(\pi_i\)</span></th>
        </tr>
        <tr>
        <td><span class="arithmatex">\(1\)</span></td>
        <td><span class="arithmatex">\(2\)</span></td>
        <td class="cella-blu"><span class="arithmatex">\(\mathbf{10}\)</span></td>
        <td class="cella-blu"><span class="arithmatex">\(\mathbf{10}\)</span></td>
        <td><span class="arithmatex">\(7\)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">\(2\)</span></td>
        <td><span class="arithmatex">\(6\)</span></td>
        <td><span class="arithmatex">\(6\)</span></td>
        <td class="cella-blu"><span class="arithmatex">\(\mathbf{10}\)</span></td>
        <td><span class="arithmatex">\(1\)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">\(3\)</span></td>
        <td class="cella-blu"><span class="arithmatex">\(\mathbf{10}\)</span></td>
        <td><span class="arithmatex">\(3\)</span></td>
        <td class="cella-blu"><span class="arithmatex">\(\mathbf{15}\)</span></td>
        <td><span class="arithmatex">\(8\)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">\(\pi_j\)</span></td>
        <td><span class="arithmatex">\(2\)</span></td>
        <td><span class="arithmatex">\(4\)</span></td>
        <td><span class="arithmatex">\(0\)</span></td>
        <td></td>
        </tr>
        </table></div>

        - All the reduced costs are non-negative: the basic feasible solution is optimal, with cost $z=290$.

    3. The first pivot has $\theta=0$: the cell $(3,4)$ enters with value $0$ and $(2,5)$ leaves; the solution and its cost do not change, but the new potentials show a negative reduced cost. The optimal solution is $\tilde{x}_{15}=10$, $\tilde{x}_{16}=10$, $\tilde{x}_{26}=10$, $\tilde{x}_{34}=10$, $\tilde{x}_{36}=15$, with cost $290$, and it is unique, since every non-basic cell has $\bar{c}_{ij}>0$.

    !!! chiave ""

        The north-west corner solution is degenerate (the basic cell $(2,5)$ has value $0$); the first pivot has $\theta=0$, the second pivot reaches the optimum, of cost $290$.

<a id="esercizio-7-4"></a>

!!! esercizio "Exercise 7.4: The Hungarian algorithm"

    !!! esercizio "Exercise"

        Five workers $1,2,3,4,5$ must be assigned to five jobs $6,7,8,9,10$, one job each, at minimum total cost. The costs are:

        $$
        \begin{array}{c|ccccc}
        \hline {c_{ij}} & {6} & {7} & {8} & {9} & {10} \\
        \hline {1} & {6} & {10} & {10} & {5} & {3} \\
        {2} & {11} & {12} & {9} & {7} & {7} \\
        {3} & {8} & {1} & {12} & {6} & {11} \\
        {4} & {12} & {7} & {10} & {8} & {2} \\
        {5} & {3} & {4} & {11} & {6} & {1} \\
        \hline
        \end{array}
        $$

    **Questions**

    1. Reduce the rows and then the columns of the matrix. Which potentials do the reductions give, and which lower bound on the optimal cost?

    2. Run the Hungarian algorithm: at each iteration give a maximum set of independent zeros, the lines of (F5) and the adjustment $\delta$.

    3. Give the optimal assignment and its cost, and check that the final potentials are an optimal dual solution.

??? soluzione "Solution"

    We use the rules (F1)–(F5) of the box at the beginning of these exercises.

    1. The row minima are $3,7,1,2,1$, so $\pi_{1}=3$, $\pi_{2}=7$, $\pi_{3}=1$, $\pi_{4}=2$, $\pi_{5}=1$:

        $$
        \begin{array}{c|ccccc}
        \hline {c_{ij}-\pi_i} & {6} & {7} & {8} & {9} & {10} \\
        \hline {1} & {3} & {7} & {7} & {2} & {0} \\
        {2} & {4} & {5} & {2} & {0} & {0} \\
        {3} & {7} & {0} & {11} & {5} & {10} \\
        {4} & {10} & {5} & {8} & {6} & {0} \\
        {5} & {2} & {3} & {10} & {5} & {0} \\
        \hline
        \end{array}
        $$

        The column minima are then $2,0,2,0,0$, so $\pi_{6}=-2$ and $\pi_{8}=-2$, and the other $\pi_j$ are $0$. The dual value $\sum_i\pi_i-\sum_j\pi_j=18$ is a lower bound on the cost of every assignment.

    2. In each matrix the independent zeros are boxed, the lines blue and the cell of $\delta$ red; the potentials are on the margins. <br><strong>Iteration 1</strong>

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">\(\bar{c}_{ij}\)</span></th>
        <th><span class="arithmatex">\(6\)</span></th>
        <th><span class="arithmatex">\(7\)</span></th>
        <th><span class="arithmatex">\(8\)</span></th>
        <th><span class="arithmatex">\(9\)</span></th>
        <th><span class="arithmatex">\(10\)</span></th>
        <th><span class="arithmatex">\(\pi_i\)</span></th>
        </tr>
        <tr>
        <td><span class="arithmatex">\(1\)</span></td>
        <td class="cella-rossa"><span class="arithmatex">\(1\)</span></td>
        <td><span class="arithmatex">\(7\)</span></td>
        <td><span class="arithmatex">\(5\)</span></td>
        <td><span class="arithmatex">\(2\)</span></td>
        <td class="cella-blu"><span class="arithmatex">\(\boxed{0}\)</span></td>
        <td><span class="arithmatex">\(3\)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">\(2\)</span></td>
        <td class="cella-blu"><span class="arithmatex">\(2\)</span></td>
        <td class="cella-blu"><span class="arithmatex">\(5\)</span></td>
        <td class="cella-blu"><span class="arithmatex">\(\boxed{0}\)</span></td>
        <td class="cella-blu"><span class="arithmatex">\(0\)</span></td>
        <td class="cella-blu"><span class="arithmatex">\(0\)</span></td>
        <td><span class="arithmatex">\(7\)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">\(3\)</span></td>
        <td class="cella-blu"><span class="arithmatex">\(5\)</span></td>
        <td class="cella-blu"><span class="arithmatex">\(\boxed{0}\)</span></td>
        <td class="cella-blu"><span class="arithmatex">\(9\)</span></td>
        <td class="cella-blu"><span class="arithmatex">\(5\)</span></td>
        <td class="cella-blu"><span class="arithmatex">\(10\)</span></td>
        <td><span class="arithmatex">\(1\)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">\(4\)</span></td>
        <td><span class="arithmatex">\(8\)</span></td>
        <td><span class="arithmatex">\(5\)</span></td>
        <td><span class="arithmatex">\(6\)</span></td>
        <td><span class="arithmatex">\(6\)</span></td>
        <td class="cella-blu"><span class="arithmatex">\(0\)</span></td>
        <td><span class="arithmatex">\(2\)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">\(5\)</span></td>
        <td class="cella-blu"><span class="arithmatex">\(\boxed{0}\)</span></td>
        <td class="cella-blu"><span class="arithmatex">\(3\)</span></td>
        <td class="cella-blu"><span class="arithmatex">\(8\)</span></td>
        <td class="cella-blu"><span class="arithmatex">\(5\)</span></td>
        <td class="cella-blu"><span class="arithmatex">\(0\)</span></td>
        <td><span class="arithmatex">\(1\)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">\(\pi_j\)</span></td>
        <td><span class="arithmatex">\(-2\)</span></td>
        <td><span class="arithmatex">\(0\)</span></td>
        <td><span class="arithmatex">\(-2\)</span></td>
        <td><span class="arithmatex">\(0\)</span></td>
        <td><span class="arithmatex">\(0\)</span></td>
        <td></td>
        </tr>
        </table></div>

        - A maximum set of independent zeros (boxed) has $4$ elements: $(1,10)$, $(2,8)$, $(3,7)$, $(5,6)$.

        - The $4<5$ lines (blue) are the rows $2$, $3$ and $5$ and the column $10$.

        - The minimum uncovered entry is $\delta=1$, in the cell $(1,6)$ (red). We subtract it from the uncovered entries and add it to the entries covered twice: $\pi_i$ grows by $1$ for the uncovered rows $1$ and $4$ and $\pi_j$ grows by $1$ for the covered column $10$. The dual value grows by $1\cdot(5-4)=1$.

        <strong>Iteration 2</strong>

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">\(\bar{c}_{ij}\)</span></th>
        <th><span class="arithmatex">\(6\)</span></th>
        <th><span class="arithmatex">\(7\)</span></th>
        <th><span class="arithmatex">\(8\)</span></th>
        <th><span class="arithmatex">\(9\)</span></th>
        <th><span class="arithmatex">\(10\)</span></th>
        <th><span class="arithmatex">\(\pi_i\)</span></th>
        </tr>
        <tr>
        <td><span class="arithmatex">\(1\)</span></td>
        <td class="cella-blu"><span class="arithmatex">\(\boxed{0}\)</span></td>
        <td><span class="arithmatex">\(6\)</span></td>
        <td><span class="arithmatex">\(4\)</span></td>
        <td class="cella-rossa"><span class="arithmatex">\(1\)</span></td>
        <td class="cella-blu"><span class="arithmatex">\(0\)</span></td>
        <td><span class="arithmatex">\(4\)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">\(2\)</span></td>
        <td class="cella-blu"><span class="arithmatex">\(2\)</span></td>
        <td class="cella-blu"><span class="arithmatex">\(5\)</span></td>
        <td class="cella-blu"><span class="arithmatex">\(\boxed{0}\)</span></td>
        <td class="cella-blu"><span class="arithmatex">\(0\)</span></td>
        <td class="cella-blu"><span class="arithmatex">\(1\)</span></td>
        <td><span class="arithmatex">\(7\)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">\(3\)</span></td>
        <td class="cella-blu"><span class="arithmatex">\(5\)</span></td>
        <td class="cella-blu"><span class="arithmatex">\(\boxed{0}\)</span></td>
        <td class="cella-blu"><span class="arithmatex">\(9\)</span></td>
        <td class="cella-blu"><span class="arithmatex">\(5\)</span></td>
        <td class="cella-blu"><span class="arithmatex">\(11\)</span></td>
        <td><span class="arithmatex">\(1\)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">\(4\)</span></td>
        <td class="cella-blu"><span class="arithmatex">\(7\)</span></td>
        <td><span class="arithmatex">\(4\)</span></td>
        <td><span class="arithmatex">\(5\)</span></td>
        <td><span class="arithmatex">\(5\)</span></td>
        <td class="cella-blu"><span class="arithmatex">\(\boxed{0}\)</span></td>
        <td><span class="arithmatex">\(3\)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">\(5\)</span></td>
        <td class="cella-blu"><span class="arithmatex">\(0\)</span></td>
        <td><span class="arithmatex">\(3\)</span></td>
        <td><span class="arithmatex">\(8\)</span></td>
        <td><span class="arithmatex">\(5\)</span></td>
        <td class="cella-blu"><span class="arithmatex">\(1\)</span></td>
        <td><span class="arithmatex">\(1\)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">\(\pi_j\)</span></td>
        <td><span class="arithmatex">\(-2\)</span></td>
        <td><span class="arithmatex">\(0\)</span></td>
        <td><span class="arithmatex">\(-2\)</span></td>
        <td><span class="arithmatex">\(0\)</span></td>
        <td><span class="arithmatex">\(1\)</span></td>
        <td></td>
        </tr>
        </table></div>

        - A maximum set of independent zeros (boxed) has $4$ elements: $(1,6)$, $(2,8)$, $(3,7)$, $(4,10)$.

        - The $4<5$ lines (blue) are the rows $2$ and $3$ and the columns $6$ and $10$.

        - The minimum uncovered entry is $\delta=1$, in the cell $(1,9)$ (red). We subtract it from the uncovered entries and add it to the entries covered twice: $\pi_i$ grows by $1$ for the uncovered rows $1$, $4$ and $5$ and $\pi_j$ grows by $1$ for the covered columns $6$ and $10$. The dual value grows by $1\cdot(5-4)=1$.

        <strong>Iteration 3</strong>

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">\(\bar{c}_{ij}\)</span></th>
        <th><span class="arithmatex">\(6\)</span></th>
        <th><span class="arithmatex">\(7\)</span></th>
        <th><span class="arithmatex">\(8\)</span></th>
        <th><span class="arithmatex">\(9\)</span></th>
        <th><span class="arithmatex">\(10\)</span></th>
        <th><span class="arithmatex">\(\pi_i\)</span></th>
        </tr>
        <tr>
        <td><span class="arithmatex">\(1\)</span></td>
        <td class="cella-blu"><span class="arithmatex">\(0\)</span></td>
        <td class="cella-blu"><span class="arithmatex">\(5\)</span></td>
        <td class="cella-blu"><span class="arithmatex">\(3\)</span></td>
        <td class="cella-blu"><span class="arithmatex">\(\boxed{0}\)</span></td>
        <td class="cella-blu"><span class="arithmatex">\(0\)</span></td>
        <td><span class="arithmatex">\(5\)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">\(2\)</span></td>
        <td class="cella-blu"><span class="arithmatex">\(3\)</span></td>
        <td class="cella-blu"><span class="arithmatex">\(5\)</span></td>
        <td class="cella-blu"><span class="arithmatex">\(\boxed{0}\)</span></td>
        <td class="cella-blu"><span class="arithmatex">\(0\)</span></td>
        <td class="cella-blu"><span class="arithmatex">\(2\)</span></td>
        <td><span class="arithmatex">\(7\)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">\(3\)</span></td>
        <td class="cella-blu"><span class="arithmatex">\(6\)</span></td>
        <td class="cella-blu"><span class="arithmatex">\(\boxed{0}\)</span></td>
        <td class="cella-blu"><span class="arithmatex">\(9\)</span></td>
        <td class="cella-blu"><span class="arithmatex">\(5\)</span></td>
        <td class="cella-blu"><span class="arithmatex">\(12\)</span></td>
        <td><span class="arithmatex">\(1\)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">\(4\)</span></td>
        <td class="cella-blu"><span class="arithmatex">\(7\)</span></td>
        <td class="cella-blu"><span class="arithmatex">\(3\)</span></td>
        <td class="cella-blu"><span class="arithmatex">\(4\)</span></td>
        <td class="cella-blu"><span class="arithmatex">\(4\)</span></td>
        <td class="cella-blu"><span class="arithmatex">\(\boxed{0}\)</span></td>
        <td><span class="arithmatex">\(4\)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">\(5\)</span></td>
        <td class="cella-blu"><span class="arithmatex">\(\boxed{0}\)</span></td>
        <td class="cella-blu"><span class="arithmatex">\(2\)</span></td>
        <td class="cella-blu"><span class="arithmatex">\(7\)</span></td>
        <td class="cella-blu"><span class="arithmatex">\(4\)</span></td>
        <td class="cella-blu"><span class="arithmatex">\(1\)</span></td>
        <td><span class="arithmatex">\(2\)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">\(\pi_j\)</span></td>
        <td><span class="arithmatex">\(-1\)</span></td>
        <td><span class="arithmatex">\(0\)</span></td>
        <td><span class="arithmatex">\(-2\)</span></td>
        <td><span class="arithmatex">\(0\)</span></td>
        <td><span class="arithmatex">\(2\)</span></td>
        <td></td>
        </tr>
        </table></div>

        - A maximum set of independent zeros (boxed) has $5$ elements: $(1,9)$, $(2,8)$, $(3,7)$, $(4,10)$, $(5,6)$.

        - They form an assignment of zero reduced cost: the algorithm stops, and the assignment is optimal.

    3. The optimal assignment is $1 \to 9$, $2 \to 8$, $3 \to 7$, $4 \to 10$, $5 \to 6$, with cost $5+9+1+2+3=20$. The final potentials give $\sum_i\pi_i-\sum_j\pi_j=19-(-1)=20$, equal to the cost; all the reduced costs are non-negative, so the potentials are dual feasible and both solutions are optimal. The optimum is unique, as the enumeration of the $120$ assignments confirms.

    !!! chiave ""

        The reductions give the bound $18$; two adjustments, with $\delta=1$ and $\delta=1$, lead to the optimal assignment $1 \to 9$, $2 \to 8$, $3 \to 7$, $4 \to 10$, $5 \to 6$, of cost $20$.

<a id="esercizio-7-5"></a>

!!! esercizio "Exercise 7.5: Bases, cycles and the minimum cost rule"

    !!! esercizio "Exercise"

        We consider the transportation instance with origins $1,2,3$ and destinations $4,5,6$:

        $$
        \begin{array}{c|ccc|c}
        \hline {c_{ij}} & {4} & {5} & {6} & {a_i} \\
        \hline {1} & {2} & {4} & {1} & {30} \\
        {2} & {4} & {8} & {5} & {20} \\
        {3} & {9} & {1} & {1} & {15} \\
        \hline {d_j} & {35} & {10} & {20} & {65} \\
        \hline
        \end{array}
        $$

        and the three sets of cells

        $$
        T_1=\{(1,4),(2,4),(2,6),(3,5),(3,6)\},\qquad T_2=\{(1,6),(2,4),(2,6),(3,5),(3,6)\},
        $$

        $$
        T_3=\{(2,4),(2,5),(2,6),(3,5),(3,6)\}.
        $$

    **Questions**

    1. Which of $T_1$, $T_2$, $T_3$ are bases? For each basis compute its basic solution and say whether it is feasible.

    2. Prove that adding a constant $k$ to all the costs of row $i$ adds $k\,a_i$ to the cost of every feasible solution, so that the optimal solutions do not change. What happens adding $k$ to a column $j$?

    3. Build the minimum cost solution and decide with the potentials whether it is optimal. Is the minimum cost rule always optimal?

??? soluzione "Solution"

    We use the rules (F1)–(F5) of the box at the beginning of these exercises.

    1. Each set has $m+n-1=5$ cells, so it is a basis exactly when it contains no cycle (F2).

        - $T_1$ has no cycle: it is a spanning tree. Leaf by leaf, leaf $1$ gives $x_{14}=30$, leaf $4$ gives $x_{24}=5$, leaf $2$ gives $x_{26}=15$, leaf $5$ gives $x_{35}=10$, leaf $3$ gives $x_{36}=5$: the basic solution is feasible.

        - $T_2$ has no cycle: it is a spanning tree. Leaf by leaf, leaf $1$ gives $x_{16}=30$, leaf $4$ gives $x_{24}=35$, leaf $2$ gives $x_{26}=-15$, leaf $5$ gives $x_{35}=10$, leaf $3$ gives $x_{36}=5$: the value $-15$ is negative, and the basic solution is not feasible.

        - $T_3$ contains the cells $(2,5)$, $(3,5)$, $(3,6)$, $(2,6)$, which form the cycle $2,5,3,6,2$ alternating rows and columns: their columns are linearly dependent, and $T_3$ is not a basis.

    2. Let $c'_{ij}=c_{ij}+k$ for every $j$ and $c'_{hj}=c_{hj}$ for $h \neq i$. For every feasible $\vet{x}$

        $$
        \sum_{h}\sum_{j} c'_{hj}x_{hj}=\sum_{h}\sum_{j} c_{hj}x_{hj}+k\sum_{j} x_{ij}=\sum_{h}\sum_{j} c_{hj}x_{hj}+k\,a_i ,
        $$

        because row $i$ of a feasible solution adds up to $a_i$. All the costs change by the same constant, so the order of the feasible solutions, and the optimal ones, do not change. In the same way, adding $k$ to column $j$ adds $k\,d_j$ to every cost. In the potential method this is a change of $\pi_i$ by $k$ (or of $\pi_j$ by $-k$), up to the normalization, and the reduced costs do not change.

    3. The minimum cost rule gives

        <div class="tabella" markdown="0"><table>
        <tr>
        <th>step</th>
        <th>cell</th>
        <th>amount</th>
        <th>crossed out</th>
        </tr>
        <tr>
        <td><span class="arithmatex">\(1\)</span></td>
        <td><span class="arithmatex">\((1,6)\)</span></td>
        <td><span class="arithmatex">\(20\)</span></td>
        <td>column <span class="arithmatex">\(6\)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">\(2\)</span></td>
        <td><span class="arithmatex">\((3,5)\)</span></td>
        <td><span class="arithmatex">\(10\)</span></td>
        <td>column <span class="arithmatex">\(5\)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">\(3\)</span></td>
        <td><span class="arithmatex">\((1,4)\)</span></td>
        <td><span class="arithmatex">\(10\)</span></td>
        <td>row <span class="arithmatex">\(1\)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">\(4\)</span></td>
        <td><span class="arithmatex">\((2,4)\)</span></td>
        <td><span class="arithmatex">\(20\)</span></td>
        <td>row <span class="arithmatex">\(2\)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">\(5\)</span></td>
        <td><span class="arithmatex">\((3,4)\)</span></td>
        <td><span class="arithmatex">\(5\)</span></td>
        <td>row <span class="arithmatex">\(3\)</span>, column <span class="arithmatex">\(4\)</span></td>
        </tr>
        </table></div>

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">\(\bar{x}_{ij}\)</span></th>
        <th><span class="arithmatex">\(4\)</span></th>
        <th><span class="arithmatex">\(5\)</span></th>
        <th><span class="arithmatex">\(6\)</span></th>
        <th><span class="arithmatex">\(a_i\)</span></th>
        </tr>
        <tr>
        <td><span class="arithmatex">\(1\)</span></td>
        <td class="cella-blu"><span class="arithmatex">\(10\)</span></td>
        <td></td>
        <td class="cella-blu"><span class="arithmatex">\(20\)</span></td>
        <td><span class="arithmatex">\(30\)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">\(2\)</span></td>
        <td class="cella-blu"><span class="arithmatex">\(20\)</span></td>
        <td></td>
        <td></td>
        <td><span class="arithmatex">\(20\)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">\(3\)</span></td>
        <td class="cella-blu"><span class="arithmatex">\(5\)</span></td>
        <td class="cella-blu"><span class="arithmatex">\(10\)</span></td>
        <td></td>
        <td><span class="arithmatex">\(15\)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">\(d_j\)</span></td>
        <td><span class="arithmatex">\(35\)</span></td>
        <td><span class="arithmatex">\(10\)</span></td>
        <td><span class="arithmatex">\(20\)</span></td>
        <td></td>
        </tr>
        </table></div>

        with cost $175$. Its potentials and reduced costs are

        <div class="tabella" markdown="0"><table>
        <tr>
        <th></th>
        <th><span class="arithmatex">\(4\)</span></th>
        <th><span class="arithmatex">\(5\)</span></th>
        <th><span class="arithmatex">\(6\)</span></th>
        <th><span class="arithmatex">\(\pi_i\)</span></th>
        </tr>
        <tr>
        <td><span class="arithmatex">\(1\)</span></td>
        <td class="cella-blu"><span class="arithmatex">\(\mathbf{10}\,\oplus\)</span></td>
        <td><span class="arithmatex">\(10\)</span></td>
        <td class="cella-blu"><span class="arithmatex">\(\mathbf{20}\,\ominus\)</span></td>
        <td><span class="arithmatex">\(1\)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">\(2\)</span></td>
        <td class="cella-blu"><span class="arithmatex">\(\mathbf{20}\)</span></td>
        <td><span class="arithmatex">\(12\)</span></td>
        <td><span class="arithmatex">\(2\)</span></td>
        <td><span class="arithmatex">\(3\)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">\(3\)</span></td>
        <td class="cella-blu"><span class="arithmatex">\(\mathbf{5}\,\ominus\)</span></td>
        <td class="cella-blu"><span class="arithmatex">\(\mathbf{10}\)</span></td>
        <td class="cella-rossa"><span class="arithmatex">\(-7\,\oplus\)</span></td>
        <td><span class="arithmatex">\(8\)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">\(\pi_j\)</span></td>
        <td><span class="arithmatex">\(-1\)</span></td>
        <td><span class="arithmatex">\(7\)</span></td>
        <td><span class="arithmatex">\(0\)</span></td>
        <td></td>
        </tr>
        </table></div>

        - The only negative reduced cost is $\bar{c}_{36}=-7$: the cell $(3,6)$ enters the basis.

        - The cycle is $\,(3,6)^{+},\ (3,4)^{-},\ (1,4)^{+},\ (1,6)^{-}$.

        - The cells with sign $-$ have $\bar{x}_{34}=5$ and $\bar{x}_{16}=20$: $\theta=5$, and the cell $(3,4)$ leaves the basis.

        - The cost goes from $175$ to $175+5\cdot(-7)=140$.

        The solution is not optimal: one pivot gives the optimum, of cost $140$. The minimum cost rule looks at one cell at a time and is not always optimal; this instance is a counterexample.

    !!! chiave ""

        $T_1$ is a basis with a feasible basic solution, $T_2$ a basis with a negative value, $T_3$ contains a cycle. The minimum cost solution (cost $175$) is not optimal: the optimum is $140$.

<a id="esercizio-7-6"></a>

!!! esercizio "Exercise 7.6: An assignment of maximum profit"

    !!! esercizio "Exercise"

        Four salespeople $1,2,3,4$ must be assigned to four regions $5,6,7,8$, one region each. The expected profits $p_{ij}$ are:

        $$
        \begin{array}{c|cccc}
        \hline {p_{ij}} & {5} & {6} & {7} & {8} \\
        \hline {1} & {9} & {4} & {5} & {1} \\
        {2} & {8} & {5} & {3} & {3} \\
        {3} & {2} & {1} & {1} & {1} \\
        {4} & {2} & {2} & {6} & {8} \\
        \hline
        \end{array}
        $$

        We look for an assignment of maximum total profit.

    **Questions**

    1. Turn the problem into an assignment problem of minimum cost with non-negative costs.

    2. Solve it with the Hungarian algorithm.

    3. Give the assignment of maximum profit and its profit.

??? soluzione "Solution"

    We use the rules (F1)–(F5) of the box at the beginning of these exercises.

    1. The largest profit is $p_{\max}=9$. With $c_{ij}=9-p_{ij}$ every assignment costs $4 \cdot 9$ minus its profit, so minimizing the cost maximizes the profit:

        $$
        \begin{array}{c|cccc}
        \hline {c_{ij}} & {5} & {6} & {7} & {8} \\
        \hline {1} & {0} & {5} & {4} & {8} \\
        {2} & {1} & {4} & {6} & {6} \\
        {3} & {7} & {8} & {8} & {8} \\
        {4} & {7} & {7} & {3} & {1} \\
        \hline
        \end{array}
        $$

    2. The row minima are $0,1,7,1$ and then the column minima $0,1,1,0$: <br><strong>Iteration 1</strong>

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">\(\bar{c}_{ij}\)</span></th>
        <th><span class="arithmatex">\(5\)</span></th>
        <th><span class="arithmatex">\(6\)</span></th>
        <th><span class="arithmatex">\(7\)</span></th>
        <th><span class="arithmatex">\(8\)</span></th>
        <th><span class="arithmatex">\(\pi_i\)</span></th>
        </tr>
        <tr>
        <td><span class="arithmatex">\(1\)</span></td>
        <td class="cella-blu"><span class="arithmatex">\(\boxed{0}\)</span></td>
        <td><span class="arithmatex">\(4\)</span></td>
        <td><span class="arithmatex">\(3\)</span></td>
        <td><span class="arithmatex">\(8\)</span></td>
        <td><span class="arithmatex">\(0\)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">\(2\)</span></td>
        <td class="cella-blu"><span class="arithmatex">\(0\)</span></td>
        <td class="cella-rossa"><span class="arithmatex">\(2\)</span></td>
        <td><span class="arithmatex">\(4\)</span></td>
        <td><span class="arithmatex">\(5\)</span></td>
        <td><span class="arithmatex">\(1\)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">\(3\)</span></td>
        <td class="cella-blu"><span class="arithmatex">\(0\)</span></td>
        <td class="cella-blu"><span class="arithmatex">\(\boxed{0}\)</span></td>
        <td class="cella-blu"><span class="arithmatex">\(0\)</span></td>
        <td class="cella-blu"><span class="arithmatex">\(1\)</span></td>
        <td><span class="arithmatex">\(7\)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">\(4\)</span></td>
        <td class="cella-blu"><span class="arithmatex">\(6\)</span></td>
        <td class="cella-blu"><span class="arithmatex">\(5\)</span></td>
        <td class="cella-blu"><span class="arithmatex">\(1\)</span></td>
        <td class="cella-blu"><span class="arithmatex">\(\boxed{0}\)</span></td>
        <td><span class="arithmatex">\(1\)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">\(\pi_j\)</span></td>
        <td><span class="arithmatex">\(0\)</span></td>
        <td><span class="arithmatex">\(-1\)</span></td>
        <td><span class="arithmatex">\(-1\)</span></td>
        <td><span class="arithmatex">\(0\)</span></td>
        <td></td>
        </tr>
        </table></div>

        - A maximum set of independent zeros (boxed) has $3$ elements: $(1,5)$, $(3,6)$, $(4,8)$.

        - The $3<4$ lines (blue) are the rows $3$ and $4$ and the column $5$.

        - The minimum uncovered entry is $\delta=2$, in the cell $(2,6)$ (red). We subtract it from the uncovered entries and add it to the entries covered twice: $\pi_i$ grows by $2$ for the uncovered rows $1$ and $2$ and $\pi_j$ grows by $2$ for the covered column $5$. The dual value grows by $2\cdot(4-3)=2$.

        <strong>Iteration 2</strong>

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">\(\bar{c}_{ij}\)</span></th>
        <th><span class="arithmatex">\(5\)</span></th>
        <th><span class="arithmatex">\(6\)</span></th>
        <th><span class="arithmatex">\(7\)</span></th>
        <th><span class="arithmatex">\(8\)</span></th>
        <th><span class="arithmatex">\(\pi_i\)</span></th>
        </tr>
        <tr>
        <td><span class="arithmatex">\(1\)</span></td>
        <td class="cella-blu"><span class="arithmatex">\(\boxed{0}\)</span></td>
        <td class="cella-blu"><span class="arithmatex">\(2\)</span></td>
        <td class="cella-blu"><span class="arithmatex">\(1\)</span></td>
        <td class="cella-blu"><span class="arithmatex">\(6\)</span></td>
        <td><span class="arithmatex">\(2\)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">\(2\)</span></td>
        <td class="cella-blu"><span class="arithmatex">\(0\)</span></td>
        <td class="cella-blu"><span class="arithmatex">\(\boxed{0}\)</span></td>
        <td class="cella-blu"><span class="arithmatex">\(2\)</span></td>
        <td class="cella-blu"><span class="arithmatex">\(3\)</span></td>
        <td><span class="arithmatex">\(3\)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">\(3\)</span></td>
        <td class="cella-blu"><span class="arithmatex">\(2\)</span></td>
        <td class="cella-blu"><span class="arithmatex">\(0\)</span></td>
        <td class="cella-blu"><span class="arithmatex">\(\boxed{0}\)</span></td>
        <td class="cella-blu"><span class="arithmatex">\(1\)</span></td>
        <td><span class="arithmatex">\(7\)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">\(4\)</span></td>
        <td class="cella-blu"><span class="arithmatex">\(8\)</span></td>
        <td class="cella-blu"><span class="arithmatex">\(5\)</span></td>
        <td class="cella-blu"><span class="arithmatex">\(1\)</span></td>
        <td class="cella-blu"><span class="arithmatex">\(\boxed{0}\)</span></td>
        <td><span class="arithmatex">\(1\)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">\(\pi_j\)</span></td>
        <td><span class="arithmatex">\(2\)</span></td>
        <td><span class="arithmatex">\(-1\)</span></td>
        <td><span class="arithmatex">\(-1\)</span></td>
        <td><span class="arithmatex">\(0\)</span></td>
        <td></td>
        </tr>
        </table></div>

        - A maximum set of independent zeros (boxed) has $4$ elements: $(1,5)$, $(2,6)$, $(3,7)$, $(4,8)$.

        - They form an assignment of zero reduced cost: the algorithm stops, and the assignment is optimal.

    3. The optimal assignment is $1 \to 5$, $2 \to 6$, $3 \to 7$, $4 \to 8$, with cost $13$ and profit

        $$
        9+5+1+8=23=4 \cdot 9-13.
        $$

        The enumeration of the $24$ assignments confirms that it is the unique optimum.

    !!! chiave ""

        With $c_{ij}=9-p_{ij}$ the Hungarian algorithm gives $1 \to 5$, $2 \to 6$, $3 \to 7$, $4 \to 8$, with profit $23$.

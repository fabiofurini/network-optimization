---
title: "An uncapacitated example"
---

# 8.6 An uncapacitated example { #sez-sec-ns-example-a }

<div class="info-capitolo" markdown>

**Part 4 · The network simplex · Chapter 8** · [:material-book-open-variant: Chapter 8: Network simplex](index.md) · [:material-file-pdf-box: Lecture notes, volume 4 (PDF)](../../pdf/lecture-notes-4-network-simplex.pdf) · [:material-presentation: Slides](../../pdf/slides-network-simplex.pdf) · [:material-pencil: Exercises: Network simplex](../../exercises/network-simplex.md) · [:material-gesture-tap: App: The network simplex, pivot by pivot](../../lab/network-simplex.md)

</div>

- We use the reference network with the balances $\vet{b}=(5,2,0,-3,0,-4)$ and the costs of <span style="color:#1971c2">[Example 8.2](bases-and-spanning-trees.md#box-8-ns-ex-tree)</span>, but without capacities: $u_{ij}=+\infty$ for every arc, so $U=\emptyset$.

- The initial tree structure sends the $5$ units of node $1$ along the path $1,3,5,4$ and the $2$ units of node $2$ along $(2,4)$; node $4$ keeps $3$ units and forwards $4$ units to node $6$:

    $$
    T=\{(1,3),(2,4),(3,5),(4,6),(5,4)\}, \qquad L=\{(1,2),(3,2),(4,3),(5,6)\}, \qquad U=\emptyset .
    $$

- Every tree solution of the example is nondegenerate. Each table gives the state of the arcs (T, L, U), the flows and the reduced costs; each cycle table lists the arcs of $C$ from the apex.

<a id="box-20-ns-ex-a"></a>

!!! esempio "Example 8.5: the network simplex without capacities"

    <strong>Iteration 1</strong><br> The potentials are $\vet{\pi}=(15,10,13,5,10,0)$ and the cost is $80$.

    <div class="tabella" markdown="0"><table>
    <tr>
    <th>arc</th>
    <th><span class="arithmatex">\((1,2)\)</span></th>
    <th><span class="arithmatex">\((1,3)\)</span></th>
    <th><span class="arithmatex">\((2,4)\)</span></th>
    <th><span class="arithmatex">\((3,2)\)</span></th>
    <th><span class="arithmatex">\((3,5)\)</span></th>
    <th><span class="arithmatex">\((4,3)\)</span></th>
    <th><span class="arithmatex">\((4,6)\)</span></th>
    <th><span class="arithmatex">\((5,4)\)</span></th>
    <th><span class="arithmatex">\((5,6)\)</span></th>
    </tr>
    <tr>
    <td>state</td>
    <td><span class="arithmatex">\(\mathrm{L}\)</span></td>
    <td><span class="arithmatex">\(\mathrm{T}\)</span></td>
    <td><span class="arithmatex">\(\mathrm{T}\)</span></td>
    <td><span class="arithmatex">\(\mathrm{L}\)</span></td>
    <td><span class="arithmatex">\(\mathrm{T}\)</span></td>
    <td><span class="arithmatex">\(\mathrm{L}\)</span></td>
    <td><span class="arithmatex">\(\mathrm{T}\)</span></td>
    <td><span class="arithmatex">\(\mathrm{T}\)</span></td>
    <td><span class="arithmatex">\(\mathrm{L}\)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">\(x_{ij}\)</span></td>
    <td><span class="arithmatex">\(0\)</span></td>
    <td><span class="arithmatex">\(5\)</span></td>
    <td><span class="arithmatex">\(2\)</span></td>
    <td><span class="arithmatex">\(0\)</span></td>
    <td><span class="arithmatex">\(5\)</span></td>
    <td><span class="arithmatex">\(0\)</span></td>
    <td><span class="arithmatex">\(4\)</span></td>
    <td><span class="arithmatex">\(5\)</span></td>
    <td><span class="arithmatex">\(0\)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">\(\bar{c}_{ij}\)</span></td>
    <td><span class="arithmatex">\(-3\)</span></td>
    <td><span class="arithmatex">\(0\)</span></td>
    <td><span class="arithmatex">\(0\)</span></td>
    <td><span class="arithmatex">\(-1\)</span></td>
    <td><span class="arithmatex">\(0\)</span></td>
    <td><span class="arithmatex">\(11\)</span></td>
    <td><span class="arithmatex">\(0\)</span></td>
    <td><span class="arithmatex">\(0\)</span></td>
    <td><span class="arithmatex">\(-7\)</span></td>
    </tr>
    </table></div>

    - The eligible arcs are $(1,2)$, $(3,2)$ and $(5,6)$; the entering arc is $e=(5,6)$, with $\bar{c}_{56}=-7$. It is in $L$, so $C$ follows $(5,6)$.

    - The tree paths to the root are $5,4,6$ and $6$: the apex is $w=6$, and $C$ is $6,4,5,6$.

        <div class="tabella" markdown="0"><table>
        <tr>
        <td>arc of <span class="arithmatex">\(C\)</span></td>
        <td><span class="arithmatex">\((4,6)\)</span></td>
        <td><span class="arithmatex">\((5,4)\)</span></td>
        <td><span class="arithmatex">\((5,6)\)</span></td>
        </tr>
        <tr>
        <td>direction</td>
        <td><span class="arithmatex">\(-\)</span></td>
        <td><span class="arithmatex">\(-\)</span></td>
        <td><span class="arithmatex">\(+\)</span></td>
        </tr>
        <tr>
        <td>residual</td>
        <td><span class="arithmatex">\(4\)</span></td>
        <td><span class="arithmatex">\(5\)</span></td>
        <td><span class="arithmatex">\(+\infty\)</span></td>
        </tr>
        </table></div>

    - $\theta=4$, and $(4,6)$ leaves the tree, to $L$. The $4$ units for node $6$ now travel on $(5,6)$ instead of $5,4,6$, and the cost becomes $80-4 \cdot 7=52$.

    - Removing $(4,6)$ cuts off $S=\{1,2,3,4,5\}$, which contains $k=5$: these potentials change by $\bar{c}_{56}=-7$.

    ![Figure 3](../../img/network-simplex/fig03.svg){ .fig loading=lazy  }

    <strong>Iteration 2</strong><br> The potentials are $\vet{\pi}=(8,3,6,-2,3,0)$ and the cost is $52$.

    <div class="tabella" markdown="0"><table>
    <tr>
    <th>arc</th>
    <th><span class="arithmatex">\((1,2)\)</span></th>
    <th><span class="arithmatex">\((1,3)\)</span></th>
    <th><span class="arithmatex">\((2,4)\)</span></th>
    <th><span class="arithmatex">\((3,2)\)</span></th>
    <th><span class="arithmatex">\((3,5)\)</span></th>
    <th><span class="arithmatex">\((4,3)\)</span></th>
    <th><span class="arithmatex">\((4,6)\)</span></th>
    <th><span class="arithmatex">\((5,4)\)</span></th>
    <th><span class="arithmatex">\((5,6)\)</span></th>
    </tr>
    <tr>
    <td>state</td>
    <td><span class="arithmatex">\(\mathrm{L}\)</span></td>
    <td><span class="arithmatex">\(\mathrm{T}\)</span></td>
    <td><span class="arithmatex">\(\mathrm{T}\)</span></td>
    <td><span class="arithmatex">\(\mathrm{L}\)</span></td>
    <td><span class="arithmatex">\(\mathrm{T}\)</span></td>
    <td><span class="arithmatex">\(\mathrm{L}\)</span></td>
    <td><span class="arithmatex">\(\mathrm{L}\)</span></td>
    <td><span class="arithmatex">\(\mathrm{T}\)</span></td>
    <td><span class="arithmatex">\(\mathrm{T}\)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">\(x_{ij}\)</span></td>
    <td><span class="arithmatex">\(0\)</span></td>
    <td><span class="arithmatex">\(5\)</span></td>
    <td><span class="arithmatex">\(2\)</span></td>
    <td><span class="arithmatex">\(0\)</span></td>
    <td><span class="arithmatex">\(5\)</span></td>
    <td><span class="arithmatex">\(0\)</span></td>
    <td><span class="arithmatex">\(0\)</span></td>
    <td><span class="arithmatex">\(1\)</span></td>
    <td><span class="arithmatex">\(4\)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">\(\bar{c}_{ij}\)</span></td>
    <td><span class="arithmatex">\(-3\)</span></td>
    <td><span class="arithmatex">\(0\)</span></td>
    <td><span class="arithmatex">\(0\)</span></td>
    <td><span class="arithmatex">\(-1\)</span></td>
    <td><span class="arithmatex">\(0\)</span></td>
    <td><span class="arithmatex">\(11\)</span></td>
    <td><span class="arithmatex">\(7\)</span></td>
    <td><span class="arithmatex">\(0\)</span></td>
    <td><span class="arithmatex">\(0\)</span></td>
    </tr>
    </table></div>

    - The eligible arcs are $(1,2)$ and $(3,2)$; the entering arc is $e=(1,2)$, with $\bar{c}_{12}=-3$, in $L$.

    - The tree paths to the root are $1,3,5,6$ and $2,4,5,6$: the apex is $w=5$, and $C$ is $5,3,1,2,4,5$.

        <div class="tabella" markdown="0"><table>
        <tr>
        <td>arc of <span class="arithmatex">\(C\)</span></td>
        <td><span class="arithmatex">\((3,5)\)</span></td>
        <td><span class="arithmatex">\((1,3)\)</span></td>
        <td><span class="arithmatex">\((1,2)\)</span></td>
        <td><span class="arithmatex">\((2,4)\)</span></td>
        <td><span class="arithmatex">\((5,4)\)</span></td>
        </tr>
        <tr>
        <td>direction</td>
        <td><span class="arithmatex">\(-\)</span></td>
        <td><span class="arithmatex">\(-\)</span></td>
        <td><span class="arithmatex">\(+\)</span></td>
        <td><span class="arithmatex">\(+\)</span></td>
        <td><span class="arithmatex">\(-\)</span></td>
        </tr>
        <tr>
        <td>residual</td>
        <td><span class="arithmatex">\(5\)</span></td>
        <td><span class="arithmatex">\(5\)</span></td>
        <td><span class="arithmatex">\(+\infty\)</span></td>
        <td><span class="arithmatex">\(+\infty\)</span></td>
        <td><span class="arithmatex">\(1\)</span></td>
        </tr>
        </table></div>

    - $\theta=1$, and $(5,4)$ leaves the tree, to $L$. The unit for node $4$ that travelled along $1,3,5,4$, at cost $10$, now travels along $1,2,4$, at cost $7$: the cost becomes $52-1 \cdot 3=49$.

    - Removing $(5,4)$ cuts off $S=\{2,4\}$, which contains $l=2$: these potentials change by $-\bar{c}_{12}=3$.

    ![Figure 4](../../img/network-simplex/fig04.svg){ .fig loading=lazy  }

    <strong>Iteration 3</strong><br> The potentials are $\vet{\pi}=(8,6,6,1,3,0)$ and the cost is $49$.

    <div class="tabella" markdown="0"><table>
    <tr>
    <th>arc</th>
    <th><span class="arithmatex">\((1,2)\)</span></th>
    <th><span class="arithmatex">\((1,3)\)</span></th>
    <th><span class="arithmatex">\((2,4)\)</span></th>
    <th><span class="arithmatex">\((3,2)\)</span></th>
    <th><span class="arithmatex">\((3,5)\)</span></th>
    <th><span class="arithmatex">\((4,3)\)</span></th>
    <th><span class="arithmatex">\((4,6)\)</span></th>
    <th><span class="arithmatex">\((5,4)\)</span></th>
    <th><span class="arithmatex">\((5,6)\)</span></th>
    </tr>
    <tr>
    <td>state</td>
    <td><span class="arithmatex">\(\mathrm{T}\)</span></td>
    <td><span class="arithmatex">\(\mathrm{T}\)</span></td>
    <td><span class="arithmatex">\(\mathrm{T}\)</span></td>
    <td><span class="arithmatex">\(\mathrm{L}\)</span></td>
    <td><span class="arithmatex">\(\mathrm{T}\)</span></td>
    <td><span class="arithmatex">\(\mathrm{L}\)</span></td>
    <td><span class="arithmatex">\(\mathrm{L}\)</span></td>
    <td><span class="arithmatex">\(\mathrm{L}\)</span></td>
    <td><span class="arithmatex">\(\mathrm{T}\)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">\(x_{ij}\)</span></td>
    <td><span class="arithmatex">\(1\)</span></td>
    <td><span class="arithmatex">\(4\)</span></td>
    <td><span class="arithmatex">\(3\)</span></td>
    <td><span class="arithmatex">\(0\)</span></td>
    <td><span class="arithmatex">\(4\)</span></td>
    <td><span class="arithmatex">\(0\)</span></td>
    <td><span class="arithmatex">\(0\)</span></td>
    <td><span class="arithmatex">\(0\)</span></td>
    <td><span class="arithmatex">\(4\)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">\(\bar{c}_{ij}\)</span></td>
    <td><span class="arithmatex">\(0\)</span></td>
    <td><span class="arithmatex">\(0\)</span></td>
    <td><span class="arithmatex">\(0\)</span></td>
    <td><span class="arithmatex">\(2\)</span></td>
    <td><span class="arithmatex">\(0\)</span></td>
    <td><span class="arithmatex">\(8\)</span></td>
    <td><span class="arithmatex">\(4\)</span></td>
    <td><span class="arithmatex">\(3\)</span></td>
    <td><span class="arithmatex">\(0\)</span></td>
    </tr>
    </table></div>

    All the arcs of $L$ have $\bar{c}_{ij}>0$: <code>STOP</code>. By <span style="color:#1971c2">[Theorem 8.10](potentials-and-optimality.md#box-12-ns-th-optimality)</span> the flow $x_{12}=1$, $x_{13}=4$, $x_{24}=3$, $x_{35}=4$, $x_{56}=4$ is the unique optimal flow, with value

    $$
    2 \cdot 1+2 \cdot 4+5 \cdot 3+3 \cdot 4+3 \cdot 4=49 .
    $$

    ![Figure 5](../../img/network-simplex/fig05.svg){ .fig loading=lazy  }

- Gurobi (gurobipy) confirms the optimal value $49$ and the optimal flow; enumerating all the feasible tree structures gives the same unique optimum.

- The optimal flow sends $4$ units on $(5,6)$, whose capacity in Chapter 4 is $u_{56}=2$: with the capacities this flow is not feasible, and the optimal value rises from $49$ to $60$.

!!! chiave ""

    Without capacities $U$ is empty and only backward arcs can block. On the reference network two pivots lower the cost from $80$ to $52$ and to $49$; the reduced costs of the last tree are positive on all the nonbasic arcs.

---

**Next:** [8.7 Degeneracy and strongly feasible trees](degeneracy-and-strongly-feasible-trees.md)

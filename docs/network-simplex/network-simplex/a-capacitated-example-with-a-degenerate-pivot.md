---
title: "A capacitated example with a degenerate pivot"
---

# 8.8 A capacitated example with a degenerate pivot { #sez-sec-ns-example-b }

<div class="info-capitolo" markdown>

**Part 4 · The network simplex · Chapter 8** · [:material-book-open-variant: Chapter 8: Network simplex](index.md) · [:material-file-pdf-box: Lecture notes, volume 4 (PDF)](../../pdf/lecture-notes-4-network-simplex.pdf) · [:material-pencil: Exercises: Network simplex](../../exercises/network-simplex.md)

</div>

- We solve the transshipment instance of [Chapter 4](https://fabiofurini.github.io/network-optimization/flows/network-flow-models/a-transshipment-instance/), the reference network with capacities, starting from the flow $\bar{\vet{x}}$ of cost $63$ with the strongly feasible tree structure of <span style="color:#1971c2">[Example 8.2](bases-and-spanning-trees.md#box-8-ns-ex-tree)</span>:

    $$
    T=\{(1,2),(2,4),(3,2),(4,6),(5,4)\}, \qquad L=\{(4,3)\}, \qquad U=\{(1,3),(3,5),(5,6)\} .
    $$

<a id="box-26-ns-ex-b"></a>

!!! esempio "Example 8.7: the network simplex with capacities"

    <strong>Iteration 1</strong><br> The potentials are $\vet{\pi}=(12,10,12,5,10,0)$ and the cost is $63$.

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
    <td><span class="arithmatex">\(\mathrm{U}\)</span></td>
    <td><span class="arithmatex">\(\mathrm{T}\)</span></td>
    <td><span class="arithmatex">\(\mathrm{T}\)</span></td>
    <td><span class="arithmatex">\(\mathrm{U}\)</span></td>
    <td><span class="arithmatex">\(\mathrm{L}\)</span></td>
    <td><span class="arithmatex">\(\mathrm{T}\)</span></td>
    <td><span class="arithmatex">\(\mathrm{T}\)</span></td>
    <td><span class="arithmatex">\(\mathrm{U}\)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">\(x_{ij}\)</span></td>
    <td><span class="arithmatex">\(1\)</span></td>
    <td><span class="arithmatex">\(4\)</span></td>
    <td><span class="arithmatex">\(3\)</span></td>
    <td><span class="arithmatex">\(0\)</span></td>
    <td><span class="arithmatex">\(4\)</span></td>
    <td><span class="arithmatex">\(0\)</span></td>
    <td><span class="arithmatex">\(2\)</span></td>
    <td><span class="arithmatex">\(2\)</span></td>
    <td><span class="arithmatex">\(2\)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">\(\bar{c}_{ij}\)</span></td>
    <td><span class="arithmatex">\(0\)</span></td>
    <td><span class="arithmatex">\(2\)</span></td>
    <td><span class="arithmatex">\(0\)</span></td>
    <td><span class="arithmatex">\(0\)</span></td>
    <td><span class="arithmatex">\(1\)</span></td>
    <td><span class="arithmatex">\(10\)</span></td>
    <td><span class="arithmatex">\(0\)</span></td>
    <td><span class="arithmatex">\(0\)</span></td>
    <td><span class="arithmatex">\(-7\)</span></td>
    </tr>
    </table></div>

    - This is the pivot of <span style="color:#1971c2">[Example 8.4](the-pivot.md#box-18-ns-ex-pivot)</span>: $e=(1,3) \in U$, apex $w=2$, $C=2,3,1,2$, residual capacities $0$, $4$, $3$.

    - $\theta=0$: the pivot is degenerate. The arc $(3,2)$ leaves the tree, to $L$, and $(1,3)$ enters it at its capacity. The cost stays $63$, and $\pi_3$ drops from $12$ to $10$.

    <strong>Iteration 2</strong><br> The potentials are $\vet{\pi}=(12,10,10,5,10,0)$ and the cost is $63$.

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
    <td><span class="arithmatex">\(\mathrm{U}\)</span></td>
    <td><span class="arithmatex">\(\mathrm{L}\)</span></td>
    <td><span class="arithmatex">\(\mathrm{T}\)</span></td>
    <td><span class="arithmatex">\(\mathrm{T}\)</span></td>
    <td><span class="arithmatex">\(\mathrm{U}\)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">\(x_{ij}\)</span></td>
    <td><span class="arithmatex">\(1\)</span></td>
    <td><span class="arithmatex">\(4\)</span></td>
    <td><span class="arithmatex">\(3\)</span></td>
    <td><span class="arithmatex">\(0\)</span></td>
    <td><span class="arithmatex">\(4\)</span></td>
    <td><span class="arithmatex">\(0\)</span></td>
    <td><span class="arithmatex">\(2\)</span></td>
    <td><span class="arithmatex">\(2\)</span></td>
    <td><span class="arithmatex">\(2\)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">\(\bar{c}_{ij}\)</span></td>
    <td><span class="arithmatex">\(0\)</span></td>
    <td><span class="arithmatex">\(0\)</span></td>
    <td><span class="arithmatex">\(0\)</span></td>
    <td><span class="arithmatex">\(2\)</span></td>
    <td><span class="arithmatex">\(3\)</span></td>
    <td><span class="arithmatex">\(8\)</span></td>
    <td><span class="arithmatex">\(0\)</span></td>
    <td><span class="arithmatex">\(0\)</span></td>
    <td><span class="arithmatex">\(-7\)</span></td>
    </tr>
    </table></div>

    - The only eligible arc is $e=(3,5) \in U$, with $\bar{c}_{35}=3$: $C$ is traversed against it, with $p=5$ and $q=3$.

    - The tree paths to the root are $3,1,2,4,6$ and $5,4,6$: the apex is $w=4$, and $C$ is $4,5,3,1,2,4$.

        <div class="tabella" markdown="0"><table>
        <tr>
        <td>arc of <span class="arithmatex">\(C\)</span></td>
        <td><span class="arithmatex">\((5,4)\)</span></td>
        <td><span class="arithmatex">\((3,5)\)</span></td>
        <td><span class="arithmatex">\((1,3)\)</span></td>
        <td><span class="arithmatex">\((1,2)\)</span></td>
        <td><span class="arithmatex">\((2,4)\)</span></td>
        </tr>
        <tr>
        <td>direction</td>
        <td><span class="arithmatex">\(-\)</span></td>
        <td><span class="arithmatex">\(-\)</span></td>
        <td><span class="arithmatex">\(-\)</span></td>
        <td><span class="arithmatex">\(+\)</span></td>
        <td><span class="arithmatex">\(+\)</span></td>
        </tr>
        <tr>
        <td>residual</td>
        <td><span class="arithmatex">\(2\)</span></td>
        <td><span class="arithmatex">\(4\)</span></td>
        <td><span class="arithmatex">\(4\)</span></td>
        <td><span class="arithmatex">\(3\)</span></td>
        <td><span class="arithmatex">\(1\)</span></td>
        </tr>
        </table></div>

    - $\theta=1$, and the blocking arc $(2,4)$, forward, leaves the tree and goes to $U$. One unit moves from the path $1,3,5,4$ to the path $1,2,4$, and the cost becomes $63-1 \cdot 3=60$.

    - Removing $(2,4)$ cuts off $S=\{1,2,3\}$, which contains $k=3$: these potentials change by $\bar{c}_{35}=3$.

    ![Figure 6](../../img/network-simplex/fig06.svg){ .fig loading=lazy  }

    <strong>Iteration 3</strong><br> The potentials are $\vet{\pi}=(15,13,13,5,10,0)$ and the cost is $60$.

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
    <td><span class="arithmatex">\(\mathrm{U}\)</span></td>
    <td><span class="arithmatex">\(\mathrm{L}\)</span></td>
    <td><span class="arithmatex">\(\mathrm{T}\)</span></td>
    <td><span class="arithmatex">\(\mathrm{L}\)</span></td>
    <td><span class="arithmatex">\(\mathrm{T}\)</span></td>
    <td><span class="arithmatex">\(\mathrm{T}\)</span></td>
    <td><span class="arithmatex">\(\mathrm{U}\)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">\(x_{ij}\)</span></td>
    <td><span class="arithmatex">\(2\)</span></td>
    <td><span class="arithmatex">\(3\)</span></td>
    <td><span class="arithmatex">\(4\)</span></td>
    <td><span class="arithmatex">\(0\)</span></td>
    <td><span class="arithmatex">\(3\)</span></td>
    <td><span class="arithmatex">\(0\)</span></td>
    <td><span class="arithmatex">\(2\)</span></td>
    <td><span class="arithmatex">\(1\)</span></td>
    <td><span class="arithmatex">\(2\)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">\(\bar{c}_{ij}\)</span></td>
    <td><span class="arithmatex">\(0\)</span></td>
    <td><span class="arithmatex">\(0\)</span></td>
    <td><span class="arithmatex">\(-3\)</span></td>
    <td><span class="arithmatex">\(2\)</span></td>
    <td><span class="arithmatex">\(0\)</span></td>
    <td><span class="arithmatex">\(11\)</span></td>
    <td><span class="arithmatex">\(0\)</span></td>
    <td><span class="arithmatex">\(0\)</span></td>
    <td><span class="arithmatex">\(-7\)</span></td>
    </tr>
    </table></div>

    The arcs of $L$ have $\bar{c}_{32}=2>0$ and $\bar{c}_{43}=11>0$, the arcs of $U$ have $\bar{c}_{24}=-3<0$ and $\bar{c}_{56}=-7<0$: <code>STOP</code>. The flow is the unique optimal flow of Chapter 4, with value $60$, and the potentials are those of its certificate.

    ![Figure 7](../../img/network-simplex/fig07.svg){ .fig loading=lazy  }

- The three tree structures are strongly feasible. In the second one the basic arc $(1,3)$ is at its capacity and points away from the root, as the definition requires.

- The degenerate pivot does not lower the cost: it only replaces $(3,2)$ with $(1,3)$ in the basis. It comes first because the entering rule prefers $|\bar{c}_{13}|=2$ to $|\bar{c}_{35}|=1$.

- Gurobi confirms the optimal value $60$, and enumerating the feasible tree structures gives the same unique optimum.

!!! chiave ""

    With capacities, arcs of $U$ enter by decreasing their flow, and a saturated arc can leave the tree to $U$. From the flow $\bar{\vet{x}}$ a degenerate pivot and a pivot with $\theta=1$ reach the optimal flow of Chapter 4, of value $60$.

---

**Next:** [8.9 The initial tree: Phase 0](the-initial-tree-phase-0.md)

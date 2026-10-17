---
title: "Optimality conditions with potentials"
---

# 6.4 Optimality conditions with potentials { #sez-sec-mc-potentials }

<div class="info-capitolo" markdown>

**Part 3 · Flows · Chapter 6** · [:material-book-open-variant: Chapter 6: Minimum cost flow](index.md) · [:material-file-pdf-box: Lecture notes, volume 3 (PDF)](../../pdf/lecture-notes-3-flows.pdf) · [:material-presentation: Slides](../../pdf/slides-min-cost-flow.pdf) · [:material-pencil: Exercises: Minimum cost flow](../../exercises/min-cost-flow.md) · [:material-gesture-tap: App: Minimum cost flow: cycle canceling and successive shortest paths](../../lab/minimum-cost-flow.md)

</div>

- Given potentials $\vet{\pi} \in \R^n$, the reduced cost of an arc $(i,j)$ of $G(\vet{x})$ is $c^x_{ij}-\pi_i+ \pi_j$. For a forward arc it is $\bar{c}_{ij}=c_{ij}-\pi_i+\pi_j$, the reduced cost of [Chapter 4](https://fabiofurini.github.io/network-optimization/flows/network-flow-models/the-dual-model-and-the-reduced-costs/); for the backward arc $(j,i)$ of $(i,j)$ it is $-c_{ij}-\pi_j+\pi_i=-\bar{c}_{ij}$.

- Along a cycle $W$ of $G(\vet{x})$ the potentials telescope, as in [Chapter 3](https://fabiofurini.github.io/network-optimization/trees-and-paths/shortest-paths/optimality-conditions-and-potentials/):

    $$
    c(W)=\sum_{(i,j) \in W}\big(c^x_{ij}-\pi_i+\pi_j\big).
    $$

<a id="box-12-mc-th-potentials"></a>

!!! teorema "Theorem 6.9: reduced cost optimality"

    A feasible flow $\vet{x}$ is optimal if and only if there are potentials $\vet{\pi} \in \R^n$ such that

    $$
    c^x_{ij}-\pi_i+\pi_j \ge 0 \qquad \text{for every arc } (i,j) \text{ of } G(\vet{x}).
    $$

??? dimostrazione "Proof"

    <em>If.</em> By the telescoping formula every cycle of $G(\vet{x})$ has $c(W) \ge 0$, and $\vet{x}$ is optimal by <span style="color:#1971c2">[Theorem 6.7](negative-cycle-optimality-conditions.md#box-9-mc-th-negcycle)</span>.

    <em>Only if.</em> Let $\vet{x}$ be optimal: by <span style="color:#1971c2">[Theorem 6.7](negative-cycle-optimality-conditions.md#box-9-mc-th-negcycle)</span>, $G(\vet{x})$ has no negative cycle.

    1. Add a node $r$ and an arc $(r,i)$ of cost $0$ for every $i \in N$. In the new graph every node is reachable from $r$, and the cycles are those of $G(\vet{x})$, since no arc enters $r$: none is negative.

    2. By Theorem «Bellman's equations» of [Chapter 3](https://fabiofurini.github.io/network-optimization/trees-and-paths/shortest-paths/shortest-path-problems/), the distances $d(i)$ from $r$ are finite and $d(j) \le d(i)+c^x_{ij}$ for every arc $(i,j)$ of $G(\vet{x})$.

    3. With $\pi_i=-d(i)$ we get $c^x_{ij}-\pi_i+\pi_j=c^x_{ij}+d(i)-d(j) \ge 0$. <span class="qed">□</span>

<a id="box-13-mc-cor-cs"></a>

!!! teorema "Corollary 6.10: complementary slackness"

    Let $\vet{x}$ be a feasible flow and $\vet{\pi} \in \R^n$. The condition of <span style="color:#1971c2">[Theorem 6.9](#box-12-mc-th-potentials)</span> holds if and only if, for every arc $(i,j) \in A$,

    $$
    \bar{c}_{ij}>0 \;\Rightarrow\; x_{ij}=l_{ij}, \qquad\qquad \bar{c}_{ij}<0 \;\Rightarrow\; x_{ij}=u_{ij} .
    $$

    In particular, $l_{ij}<x_{ij}<u_{ij}$ implies $\bar{c}_{ij}=0$.

??? dimostrazione "Proof"

    The arc $(i,j) \in A$ gives the forward arc, of reduced cost $\bar{c}_{ij}$, when $x_{ij}<u_{ij}$, and the backward arc, of reduced cost $-\bar{c}_{ij}$, when $x_{ij}>l_{ij}$. So the condition on the arcs coming from $(i,j)$ reads

    $$
    x_{ij}<u_{ij} \;\Rightarrow\; \bar{c}_{ij} \ge 0, \qquad\qquad x_{ij}>l_{ij} \;\Rightarrow\; \bar{c}_{ij} \le 0 .
    $$

    Since $l_{ij} \le x_{ij} \le u_{ij}$, the first implication is equivalent to $\bar{c}_{ij}<0 \Rightarrow x_{ij}=u_{ij}$, and the second to $\bar{c}_{ij}>0 \Rightarrow x_{ij}=l_{ij}$. If $l_{ij}<x_{ij}<u_{ij}$, both implications apply and $\bar{c}_{ij}=0$. <span class="qed">□</span>

- With $\vet{l}=\vet{0}$ these are the conditions of Corollary «reduced cost certificate» of [Chapter 4](https://fabiofurini.github.io/network-optimization/flows/network-flow-models/the-dual-model-and-the-reduced-costs/). There they were proved sufficient with LP duality; <span style="color:#1971c2">[Theorem 6.9](#box-12-mc-th-potentials)</span> shows that every optimal flow has such potentials, which with $\alpha_{ij}=\max\{0,-\bar{c}_{ij}\}$ form an optimal dual solution.

- The potentials of the proof are $\pi_i=-d(i)$, minus the distances from $r$, as $\pi_i=-\tilde{d}(i)$ in [Chapter 3](https://fabiofurini.github.io/network-optimization/trees-and-paths/shortest-paths/optimality-conditions-and-potentials/). They can be shifted by a constant; we normalize them with $\pi_n=0$.

<a id="box-14-mc-ex-potentials"></a>

!!! esempio "Example 6.4: the certificate of the optimal flow"

    We take $\tilde{\vet{x}}$ and the potentials $\vet{\pi}=(15,13,13,5,10,0)$ of Chapter 4. The reduced costs of the arcs of $G(\tilde{\vet{x}})$ are $\bar{c}_{ij}$ on the forward arcs and $-\bar{c}_{ij}$ on the backward arcs:

    <div class="tabella" markdown="0"><table>
    <tr>
    <th>arc <span class="arithmatex">\((i,j)\)</span></th>
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
    <td><span class="arithmatex">\(\tilde{x}_{ij}\)</span></td>
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
    <tr>
    <td>forward <span class="arithmatex">\((i,j)\)</span></td>
    <td><span class="arithmatex">\(0\)</span></td>
    <td><span class="arithmatex">\(0\)</span></td>
    <td>–</td>
    <td><span class="arithmatex">\(2\)</span></td>
    <td><span class="arithmatex">\(0\)</span></td>
    <td><span class="arithmatex">\(11\)</span></td>
    <td><span class="arithmatex">\(0\)</span></td>
    <td><span class="arithmatex">\(0\)</span></td>
    <td>–</td>
    </tr>
    <tr>
    <td>backward <span class="arithmatex">\((j,i)\)</span></td>
    <td><span class="arithmatex">\(0\)</span></td>
    <td><span class="arithmatex">\(0\)</span></td>
    <td><span class="arithmatex">\(3\)</span></td>
    <td>–</td>
    <td><span class="arithmatex">\(0\)</span></td>
    <td>–</td>
    <td><span class="arithmatex">\(0\)</span></td>
    <td><span class="arithmatex">\(0\)</span></td>
    <td><span class="arithmatex">\(7\)</span></td>
    </tr>
    </table></div>

    - All the $14$ arcs of $G(\tilde{\vet{x}})$ have non-negative reduced cost: by <span style="color:#1971c2">[Theorem 6.9](#box-12-mc-th-potentials)</span>, $\tilde{\vet{x}}$ is optimal. In the form of <span style="color:#1971c2">[Corollary 6.10](#box-13-mc-cor-cs)</span>: $(3,2)$ and $(4,3)$ are empty, $(2,4)$ and $(5,6)$ are saturated.

    - The potentials are minus the costs of the cheapest walks of $G(\tilde{\vet{x}})$ ending at each node. For example, the walk $6,4,5,3,1$ uses four backward arcs and costs $-5-5-3-2=-15=-\pi_1$: in $G$ it is the path $1,3,5,4,6$ of the spanning tree of Chapter 4.

!!! chiave ""

    A feasible flow is optimal if and only if some potentials give non-negative reduced costs on all the arcs of $G(\vet{x})$: positive $\bar{c}_{ij}$ only on arcs at the lower bound, negative only on saturated arcs. Such potentials are minus the distances in $G(\vet{x})$ from a node joined to all the others.

---

**Next:** [6.5 A first feasible flow](a-first-feasible-flow.md)

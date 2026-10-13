---
title: "The initial tree: Phase 0"
---

# 8.9 The initial tree: Phase 0

<div class="info-capitolo" markdown>

**Part 4 · The network simplex · Chapter 8** · [:material-book-open-variant: Chapter 8: Network simplex](index.md) · [:material-file-pdf-box: Lecture notes, volume 4 (PDF)](../../pdf/lecture-notes-4-network-simplex.pdf) · [:material-pencil: Exercises: Network simplex](../../exercises/network-simplex.md)

</div>

<a id="sez-sec-ns-phase0"></a>
<a id="box-27-ns-def-auxiliary"></a>

!!! definizione "Definition 8.20: auxiliary network"

    Let $G=(N,A)$ be a network with $\sum_{i \in N}b_i=0$. The <strong>auxiliary network</strong> $G^0$ adds to $G$ the <strong>artificial node</strong> $r=n+1$, with $b_r=0$, and one <strong>artificial arc</strong> for every node $i \in N$:

    $$
    (i,r) \ \text{ if } b_i \ge 0, \qquad\qquad (r,i) \ \text{ if } b_i<0,
    $$

    with capacity $+\infty$. The costs of Phase 0 are $c^0_{ij}=1$ on the artificial arcs and $c^0_{ij}=0$ on the arcs of $A$. <strong>Phase 0</strong> applies the network simplex algorithm to $G^0$ with the costs $c^0_{ij}$, starting from the tree of the artificial arcs, with $L=A$ and $U=\emptyset$; the root is the last node, $r$.

- The value of Phase 0 is the total flow on the artificial arcs: it measures how far the flow is from being a flow of $G$. This is the auxiliary problem of [Chapter 8 «Phase 0 of the simplex algorithm»](https://fabiofurini.github.io/linear-programming/simplex/08-phase-zero/), written on the network.

<a id="box-28-ns-prop-initial"></a>

!!! teorema "Proposition 8.21: the initial tree of Phase 0"

    The artificial arcs form a spanning tree of $G^0$. Its tree solution has $x_{ir}=b_i$ if $b_i \ge 0$, $x_{ri}=-b_i$ if $b_i<0$, and $x_{ij}=0$ on $A$; its cost is $\sum_{i \in N}|b_i|$, and the tree structure is strongly feasible.

??? dimostrazione "Proof"

    The $n$ artificial arcs join every node of $N$ to $r$: they form a connected graph with $n+1$ nodes and $n$ arcs, a spanning tree.

    - At a node $i \in N$ the only arc with flow is its artificial arc, so conservation holds. At $r$ the outflow minus the inflow is $\sum_{i:\,b_i<0}(-b_i)-\sum_{i:\,b_i \ge 0}b_i=-\sum_{i \in N}b_i=0=b_r$.

    - The tree arcs with zero flow are the arcs $(i,r)$ with $b_i=0$: their tail is $i$, so they point towards the root. No tree arc is at its capacity, which is $+\infty$.

    <p class="qed-riga"><span class="qed">□</span></p>

<a id="box-29-ns-th-phase0"></a>

!!! teorema "Theorem 8.22: Phase 0"

    Phase 0 stops after a finite number of pivots with an optimal value $z_0 \ge 0$. The network $G$ has a feasible flow if and only if $z_0=0$, and in that case the final flow of Phase 0, restricted to $A$, is a feasible flow of $G$.

??? dimostrazione "Proof"

    All the capacities of $G^0$ are positive and the initial tree structure is strongly feasible (<span style="color:#1971c2">[Proposition 8.21](#box-28-ns-prop-initial)</span>), so Phase 0 stops by <span style="color:#1971c2">[Theorem 8.19](degeneracy-and-strongly-feasible-trees.md#box-25-ns-th-finite)</span>.

    1. It cannot stop in Step 3: the costs $c^0_{ij}$ are non-negative, so no cycle has negative cost (<span style="color:#1971c2">[Proposition 8.14](the-pivot.md#box-17-ns-prop-unbounded)</span>). It stops in Step 1 with an optimal flow, of value $z_0 \ge 0$.

    2. If $G$ has a feasible flow, the same flow with zero on the artificial arcs is feasible for $G^0$ with cost $0$, so $z_0=0$.

    3. If $z_0=0$, every artificial arc carries zero flow, so the conservation constraints of the nodes of $N$ involve only arcs of $A$: the restriction to $A$ is a feasible flow of $G$. <span class="qed">□</span>

- When $z_0=0$ the final tree of Phase 0 still contains at least one artificial arc, since the root $r$ must be connected to the other nodes. The next proposition shows how to continue from this tree.

<a id="box-30-ns-prop-after"></a>

!!! teorema "Proposition 8.23: from Phase 0 to the network simplex"

    Let Phase 0 end with $z_0=0$, with flow $\tilde{\vet{x}}^0$, tree structure $(T,L,U)$ and reduced costs $\bar{c}^0_{ij}$. Apply the network simplex algorithm to $G^0$ from $(T,L,U)$, with the costs $c_{ij}$ on $A$ and $0$ on the artificial arcs, letting enter only the arcs with $\bar{c}^0_{ij}=0$. Then every flow met has zero flow on the artificial arcs, and the algorithm ends with an optimal flow of $G$, or proves that the $\mathrm{MCF}$ model is unbounded.

??? dimostrazione "Proof"

    Call <em>frozen</em> the arcs with $\bar{c}^0_{ij} \neq 0$. They are not in $T$, and by the optimality of Phase 0 those with $\bar{c}^0_{ij}>0$ are in $L$, with flow $0$, and those with $\bar{c}^0_{ij}<0$ are in $U$, with flow $u_{ij}$.

    1. <em>A key identity.</em> Let $\vet{y}$ be a flow of $G^0$ that satisfies conservation and the bounds. By [Chapter 4, Lemma «cost and reduced cost»](https://fabiofurini.github.io/network-optimization/flows/network-flow-models/the-dual-model-and-the-reduced-costs/), and since the cost of $\tilde{\vet{x}}^0$ is $z_0=0$,

        $$
        \sum_{a}c^0_ay_a=\sum_{a}\bar{c}^0_a\,(y_a-\tilde{x}^0_a) .
        $$

        Each term is $\bar{c}^0_ay_a \ge 0$ on the frozen arcs of $L$, $\bar{c}^0_a(y_a-u_a) \ge 0$ on the frozen arcs of $U$, and $0$ elsewhere.

    2. <em>No artificial flow.</em> The frozen arcs never enter the tree, so every flow met keeps their values, and every term of the identity is $0$. Hence the total artificial flow $\sum_{a}c^0_ay_a$ is $0$, and every artificial arc carries zero flow.

    3. <em>The feasible flows of $G$ keep the frozen values.</em> A feasible flow $\vet{y}$ of $G$, with zero on the artificial arcs, has $\sum_{a}c^0_ay_a=0$: every term of the identity vanishes, so $y_a=0$ on the frozen arcs of $L$ and $y_a=u_a$ on those of $U$.

    4. <em>Optimality.</em> Let the algorithm stop with flow $\vet{x}$ and potentials $\vet{\pi}$. As in <span style="color:#1971c2">[Theorem 8.10](potentials-and-optimality.md#box-12-ns-th-optimality)</span>, $\vet{c}'\vet{y}-\vet{c}'\vet{x}=\sum_{a}\bar{c}_a(y_a-x_a)$. The frozen arcs give $0$ by step 3, the tree arcs give $0$, and the other arcs of $L$ and $U$ satisfy the stopping conditions and give a non-negative term. Hence $\vet{c}'\vet{y} \ge \vet{c}'\vet{x}$.

    5. <em>Unboundedness.</em> If the algorithm stops in Step 3, the flows $\vet{x}+t\vet{x}^C$ of <span style="color:#1971c2">[Proposition 8.14](the-pivot.md#box-17-ns-prop-unbounded)</span> keep the frozen values: by the identity of step 1 they have zero artificial flow, so they are flows of $G$ with cost tending to $-\infty$.

    The structures met stay strongly feasible, and the algorithm stops, by <span style="color:#1971c2">[Theorem 8.19](degeneracy-and-strongly-feasible-trees.md#box-25-ns-th-finite)</span>. <span class="qed">□</span>

<a id="box-31-ns-ex-phase0"></a>

!!! esempio "Example 8.8: Phase 0 on the reference network"

    For the reference network with capacities, the auxiliary network has the artificial node $7$ and the artificial arcs $(1,7)$, $(2,7)$, $(3,7)$, $(5,7)$, since $b_1,b_2,b_3,b_5 \ge 0$, and $(7,4)$, $(7,6)$. The initial tree (blue) carries $5$, $2$, $0$, $0$, $3$, $4$ units on these arcs, all the arcs of $A$ are empty (they are not drawn), and $z_0=14$. The initial potentials are $\pi_i=1$ for the nodes with an arc $(i,7)$ and $\pi_i=-1$ for those with an arc $(7,i)$.

    ![Figure 8](../../img/network-simplex/fig08.svg){ .fig loading=lazy  }

    Phase 0 makes six pivots; every entering arc has $\bar{c}^0_{ij}=-2$, and every apex is the root $7$.

    <div class="tabella" markdown="0"><table>
    <tr>
    <th>pivot</th>
    <th>entering</th>
    <th><span class="arithmatex">\(\bar{c}^0_{ij}\)</span></th>
    <th>apex</th>
    <th><span class="arithmatex">\(\theta\)</span></th>
    <th>blocking arcs</th>
    <th>leaving</th>
    <th><span class="arithmatex">\(z_0\)</span> after</th>
    </tr>
    <tr>
    <td><span class="arithmatex">\(1\)</span></td>
    <td><span class="arithmatex">\((2,4)\)</span></td>
    <td><span class="arithmatex">\(-2\)</span></td>
    <td><span class="arithmatex">\(7\)</span></td>
    <td><span class="arithmatex">\(2\)</span></td>
    <td><span class="arithmatex">\((2,7)\)</span></td>
    <td><span class="arithmatex">\((2,7)\)</span></td>
    <td><span class="arithmatex">\(10\)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">\(2\)</span></td>
    <td><span class="arithmatex">\((1,2)\)</span></td>
    <td><span class="arithmatex">\(-2\)</span></td>
    <td><span class="arithmatex">\(7\)</span></td>
    <td><span class="arithmatex">\(1\)</span></td>
    <td><span class="arithmatex">\((7,4)\)</span></td>
    <td><span class="arithmatex">\((7,4)\)</span></td>
    <td><span class="arithmatex">\(8\)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">\(3\)</span></td>
    <td><span class="arithmatex">\((4,6)\)</span></td>
    <td><span class="arithmatex">\(-2\)</span></td>
    <td><span class="arithmatex">\(7\)</span></td>
    <td><span class="arithmatex">\(1\)</span></td>
    <td><span class="arithmatex">\((2,4)\)</span></td>
    <td><span class="arithmatex">\((2,4)\)</span></td>
    <td><span class="arithmatex">\(6\)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">\(4\)</span></td>
    <td><span class="arithmatex">\((5,4)\)</span></td>
    <td><span class="arithmatex">\(-2\)</span></td>
    <td><span class="arithmatex">\(7\)</span></td>
    <td><span class="arithmatex">\(0\)</span></td>
    <td><span class="arithmatex">\((5,7)\)</span></td>
    <td><span class="arithmatex">\((5,7)\)</span></td>
    <td><span class="arithmatex">\(6\)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">\(5\)</span></td>
    <td><span class="arithmatex">\((3,5)\)</span></td>
    <td><span class="arithmatex">\(-2\)</span></td>
    <td><span class="arithmatex">\(7\)</span></td>
    <td><span class="arithmatex">\(0\)</span></td>
    <td><span class="arithmatex">\((3,7)\)</span></td>
    <td><span class="arithmatex">\((3,7)\)</span></td>
    <td><span class="arithmatex">\(6\)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">\(6\)</span></td>
    <td><span class="arithmatex">\((1,3)\)</span></td>
    <td><span class="arithmatex">\(-2\)</span></td>
    <td><span class="arithmatex">\(7\)</span></td>
    <td><span class="arithmatex">\(3\)</span></td>
    <td><span class="arithmatex">\((1,7)\)</span>, <span class="arithmatex">\((5,4)\)</span>, <span class="arithmatex">\((7,6)\)</span></td>
    <td><span class="arithmatex">\((7,6)\)</span></td>
    <td><span class="arithmatex">\(0\)</span></td>
    </tr>
    </table></div>

    - Pivots $4$ and $5$ are degenerate. In pivot $3$ the arc $(2,4)$ reaches its capacity and goes to $U$.

    - In pivot $6$ the cycle is $7,1,3,5,4,6,7$, with three blocking arcs. The rule chooses $(7,6)$, the last one from the apex. With $(1,7)$ the tree would contain $(5,4)$ saturated pointing towards the root and $(7,6)$ empty pointing away from it; with $(5,4)$, the empty arc $(7,6)$ pointing away: neither tree would be strongly feasible.

    - Phase 0 ends with $z_0=0$, the tree $(1,2)$, $(1,3)$, $(1,7)$, $(3,5)$, $(4,6)$, $(5,4)$ and $U=\{(2,4)\}$. All the potentials of $N$ are $1$, so $\bar{c}^0_{ij}=0$ on every arc except $(7,4)$ and $(7,6)$, which have $\bar{c}^0_{ij}=2$ and are frozen.

    With the costs $c_{ij}$ the tree solution costs $74$. The arcs $(7,4)$ and $(7,6)$ have reduced costs $-10$ and $-15$, but they are frozen: the only arc that may enter is $(5,6)$, with $\bar{c}_{56}=-7$. Its residual capacity $u_{56}=2$ is the smallest along its cycle, so $(5,6)$ itself is the leaving arc and moves to $U$, and the cost becomes $74-2 \cdot 7=60$: the optimum of <span style="color:#1971c2">[Example 8.7](a-capacitated-example-with-a-degenerate-pivot.md#box-26-ns-ex-b)</span>. If $(7,6)$ could enter, $3$ units would travel from $1$ to $6$ through the artificial node, at cost $29$: not a flow of $G$.

!!! chiave ""

    Phase 0 starts from the strongly feasible star of the artificial arcs and minimizes the artificial flow: $z_0>0$ proves that no feasible flow exists. If $z_0=0$, the network simplex continues from the final tree, with the original costs, and only the arcs with zero reduced cost in Phase 0 may enter.

## 8.10 Typical mistakes

!!! attenzione "Warning"

    - <strong>Calling basic the arcs with positive flow.</strong> The basis is the tree $T$: an arc of $U$ has positive flow but is nonbasic, and a tree arc can have flow $0$ or $u_{ij}$.

    - <strong>Using the sign test of a maximization.</strong> In the $\mathrm{MCF}$ model, a minimization, an arc of $L$ is eligible if $\bar{c}_{ij}<0$ and an arc of $U$ if $\bar{c}_{ij}>0$.

    - <strong>Orienting the cycle as the entering arc when it is in $U$.</strong> Its flow must decrease, so the cycle goes against it, and the entering arc is backward.

    - <strong>Forgetting the entering arc in the ratio test.</strong> Its residual capacity is $u_{kl}$; if it is the only blocking arc, the tree does not change and the arc moves between $L$ and $U$.

    - <strong>Updating all the potentials.</strong> Only the potentials of the subtree cut off by the leaving arc change, all by $\bar{c}_{kl}$ or $-\bar{c}_{kl}$.

    - <strong>Choosing any blocking arc.</strong> The last blocking arc from the apex keeps the tree strongly feasible; another choice can lose this property and the guarantee against cycling.

    - <strong>Letting the frozen arcs enter after Phase 0.</strong> An arc with $\bar{c}^0_{ij} \neq 0$ can put flow on the artificial arcs; only the arcs with $\bar{c}^0_{ij}=0$ may enter.

## 8.11 In summary

!!! chiave "In summary"

    - In a connected network the equation of node $n$ is redundant, and the bases of the $\mathrm{MCF}$ model are the spanning trees; their matrices are triangular with determinant $\pm 1$.

    - A tree structure $(T,L,U)$ fixes the nonbasic arcs at $0$ or at their capacity; the tree solution follows from the leaves, and the potentials from the root, with $\pi_n=0$.

    - The reduced cost of a nonbasic arc is the cost of its fundamental cycle; $\bar{c} \ge 0$ on $L$ and $\bar{c} \le 0$ on $U$ certify optimality.

    - A pivot sends $\theta$ units around the cycle of the entering arc and lowers the cost by $\theta|\bar{c}_{kl}|$; the leaving arc is the last blocking arc from the apex, and only the potentials of one subtree change.

    - Strongly feasible trees and this leaving arc rule prevent cycling. Phase 0 on the auxiliary network gives a strongly feasible initial tree, or proves that no feasible flow exists.

    <strong>The reference network at a glance.</strong>

    <div class="tabella" markdown="0"><table>
    <tr>
    <td>without capacities</td>
    <td>costs <span class="arithmatex">\(80\)</span>, <span class="arithmatex">\(52\)</span>, <span class="arithmatex">\(49\)</span>; optimal tree <span class="arithmatex">\((1,2),(1,3),(2,4),(3,5),(5,6)\)</span></td>
    </tr>
    <tr>
    <td>with capacities, from <span class="arithmatex">\(\bar{\vet{x}}\)</span></td>
    <td>costs <span class="arithmatex">\(63\)</span>, <span class="arithmatex">\(63\)</span> (degenerate), <span class="arithmatex">\(60\)</span>; <span class="arithmatex">\(U=\{(2,4),(5,6)\}\)</span></td>
    </tr>
    <tr>
    <td>optimal potentials (<span class="arithmatex">\(\pi_6=0\)</span>)</td>
    <td><span class="arithmatex">\((8,6,6,1,3,0)\)</span> without capacities, <span class="arithmatex">\((15,13,13,5,10,0)\)</span> with</td>
    </tr>
    <tr>
    <td>Phase 0</td>
    <td><span class="arithmatex">\(z_0\)</span> from <span class="arithmatex">\(14\)</span> to <span class="arithmatex">\(0\)</span> in six pivots, then one pivot from <span class="arithmatex">\(74\)</span> to <span class="arithmatex">\(60\)</span></td>
    </tr>
    </table></div>

---

**Exercises on this chapter:** [:material-pencil: Network simplex](../../exercises/network-simplex.md)


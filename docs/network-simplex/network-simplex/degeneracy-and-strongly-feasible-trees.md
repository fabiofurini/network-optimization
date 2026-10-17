---
title: "Degeneracy and strongly feasible trees"
---

# 8.7 Degeneracy and strongly feasible trees { #sez-sec-ns-degeneracy }

<div class="info-capitolo" markdown>

**Part 4 · The network simplex · Chapter 8** · [:material-book-open-variant: Chapter 8: Network simplex](index.md) · [:material-file-pdf-box: Lecture notes, volume 4 (PDF)](../../pdf/lecture-notes-4-network-simplex.pdf) · [:material-presentation: Slides](../../pdf/slides-network-simplex.pdf) · [:material-pencil: Exercises: Network simplex](../../exercises/network-simplex.md) · [:material-gesture-tap: App: The network simplex, pivot by pivot](../../lab/network-simplex.md)

</div>

<a id="box-21-ns-def-strong"></a>

!!! definizione "Definition 8.16: strongly feasible tree structure"

    Let $(T,L,U)$ be a feasible tree structure with tree solution $\vet{x}$ and root $n$. For a node $i \neq n$, the tree arc between $i$ and the next node of its path to the root <strong>points towards the root</strong> if $i$ is its tail, and <strong>away from the root</strong> if $i$ is its head. The tree structure is <strong>strongly feasible</strong> if

    - every tree arc with $x_{ij}=0$ points towards the root, and

    - every tree arc with $x_{ij}=u_{ij}$ points away from the root.

- Equivalently, a positive amount of flow can be sent from every node to the root along its tree path. An arc pointing towards the root is traversed forward and needs $x_{ij}<u_{ij}$; an arc pointing away is traversed backward and needs $x_{ij}>0$.

- A nondegenerate feasible tree structure is strongly feasible.

- In a degenerate pivot the flow and the cost do not change, but the tree does. <span style="color:#1971c2">[Proposition 8.15](the-network-simplex-algorithm.md#box-19-ns-prop-finite)</span> does not exclude that a sequence of degenerate pivots comes back to a tree structure already met: the algorithm would then <strong>cycle</strong>, as the simplex algorithm of [Chapter 7 «Optimality conditions and pivot rules»](https://fabiofurini.github.io/linear-programming/simplex/07-optimality-pivot/).

<a id="box-22-ns-ex-strong"></a>

!!! esempio "Example 8.6: the four tree structures of $\bar{\vet{x}}$"

    In the flow $\bar{\vet{x}}$ of <span style="color:#1971c2">[Example 8.2](bases-and-spanning-trees.md#box-8-ns-ex-tree)</span> the arcs $(1,2)$, $(2,4)$, $(4,6)$, $(5,4)$ are strictly between their bounds, and they connect all the nodes except $3$. A spanning tree containing them adds one arc at a bound incident to node $3$, and each choice gives a tree structure with the same tree solution $\bar{\vet{x}}$:

    <div class="tabella" markdown="0"><table>
    <tr>
    <th>added arc</th>
    <th>flow</th>
    <th>path from <span class="arithmatex">\(3\)</span> to the root</th>
    <th>strongly feasible</th>
    </tr>
    <tr>
    <td><span class="arithmatex">\((3,2)\)</span></td>
    <td><span class="arithmatex">\(0\)</span></td>
    <td><span class="arithmatex">\(3,2,4,6\)</span>: the arc points towards the root</td>
    <td>yes</td>
    </tr>
    <tr>
    <td><span class="arithmatex">\((1,3)\)</span></td>
    <td><span class="arithmatex">\(4=u_{13}\)</span></td>
    <td><span class="arithmatex">\(3,1,2,4,6\)</span>: the arc points away from the root</td>
    <td>yes</td>
    </tr>
    <tr>
    <td><span class="arithmatex">\((3,5)\)</span></td>
    <td><span class="arithmatex">\(4=u_{35}\)</span></td>
    <td><span class="arithmatex">\(3,5,4,6\)</span>: the arc points towards the root</td>
    <td>no</td>
    </tr>
    <tr>
    <td><span class="arithmatex">\((4,3)\)</span></td>
    <td><span class="arithmatex">\(0\)</span></td>
    <td><span class="arithmatex">\(3,4,6\)</span>: the arc points away from the root</td>
    <td>no</td>
    </tr>
    </table></div>

    With $(3,5)$ in the tree, no flow can leave node $3$ towards the root, because $(3,5)$ is saturated; with $(4,3)$, no flow can reach $4$ from $3$, because $(4,3)$ is empty. The pivot of <span style="color:#1971c2">[Example 8.4](the-pivot.md#box-18-ns-ex-pivot)</span> goes from the first structure to the second.

<a id="box-23-ns-lem-degenerate"></a>

!!! teorema "Lemma 8.17: degenerate pivots"

    Let $(T,L,U)$ be strongly feasible, and let $C$ be the cycle of a pivot, traversed from the apex $w$: the tree path $P$ from $w$ to $p$, the arc $e$, the tree path $Q$ from $q$ to $w$. Then every arc of $Q$ and the arc $e$ have positive residual capacity. In particular, if $\theta=0$, all the blocking arcs lie on $P$.

??? dimostrazione "Proof"

    The residual capacity of $e$ is $u_{kl}>0$: it is $u_{kl}-0$ if $e \in L$ and $x_{kl}=u_{kl}$ if $e \in U$. The apex $w$ lies on the tree path from $q$ to the root, so $Q$ is the first part of this path, traversed towards the root. By strong feasibility a positive amount of flow can be sent from $q$ to the root along it: every arc of $Q$ has positive residual capacity in the direction of $C$. <span class="qed">□</span>

<a id="box-24-ns-th-strong"></a>

!!! teorema "Theorem 8.18: the leaving arc rule keeps strong feasibility"

    If $(T,L,U)$ is strongly feasible and $\theta<+\infty$, the tree structure obtained by the pivot, with the leaving arc of <span style="color:#1971c2">[Definition 8.11](the-pivot.md#box-14-ns-def-pivot)</span>, is strongly feasible.

??? dimostrazione "Proof"

    Let $C$ visit $w=v_0,v_1,\dots,v_r=w$ in its direction, with $f$ between $v_s$ and $v_{s+1}$, and let $\vet{x}'$ be the new flow. Let $i$ be a node and $y$ the first node of $C$ on its tree path to the root in $T$.

    1. <em>The new path.</em> If the path of $i$ does not meet $C$, it is the same in $T'$. Otherwise the path of $i$ in $T'$ goes from $i$ to $y$ as in $T$, then from $y$ to $w$ inside $C \setminus \{f\}$, then from $w$ to the root as in $T$. The two outer parts use no arc of $C$, so their flows do not change and they still carry positive flow towards the root.

    2. <em>The part inside $C$.</em> If $y=v_t$ with $t \le s$, the path goes $v_t,v_{t-1},\dots,v_0=w$, against the direction of $C$. If $t \ge s+1$, it goes $v_t,v_{t+1},\dots,v_r=w$, in the direction of $C$.

    3. <em>Case $\theta>0$.</em> Against $C$, the residual capacity of every arc grows by $\theta>0$. In the direction of $C$, the arcs after $f$ are not blocking, because $f$ is the last blocking arc: their residual capacity was larger than $\theta$, and it stays positive.

    4. <em>Case $\theta=0$.</em> The flow does not change, and $f$ lies on $P$ by <span style="color:#1971c2">[Lemma 8.17](#box-23-ns-lem-degenerate)</span>. For $t \le s$, the path from $v_t$ to $w$ goes up $P$: it is part of the tree path of $v_t$ in $T$, which carries positive flow towards the root. For $t \ge s+1$, the arcs of $P$ after $f$ are not blocking, and $e$ and the arcs of $Q$ have positive residual capacity by the same lemma.

    In all cases every node can send a positive amount of flow to the root in $T'$. <span class="qed">□</span>

<a id="box-25-ns-th-finite"></a>

!!! teorema "Theorem 8.19: finiteness of the network simplex algorithm"

    If the initial tree structure is strongly feasible and every pivot uses the leaving arc of <span style="color:#1971c2">[Definition 8.11](the-pivot.md#box-14-ns-def-pivot)</span>, then every tree structure met is strongly feasible, no tree structure is met twice, and the algorithm stops after a finite number of pivots. This holds for any rule that chooses the entering arc among the eligible arcs.

??? dimostrazione "Proof"

    Strong feasibility follows by induction from <span style="color:#1971c2">[Theorem 8.18](#box-24-ns-th-strong)</span>.

    1. A pivot with $\theta>0$ decreases the cost (<span style="color:#1971c2">[Proposition 8.12](the-pivot.md#box-15-ns-prop-pivot)</span>).

    2. In a degenerate pivot, $f$ lies on $P$ (<span style="color:#1971c2">[Lemma 8.17](#box-23-ns-lem-degenerate)</span>), so the path from $p$ to the root passes through $f$, and $p \in S$. If $e \in L$, then $p=k$ and the potentials of $S$ change by $\bar{c}_{kl}<0$; if $e \in U$, then $p=l$ and they change by $-\bar{c}_{kl}<0$ (<span style="color:#1971c2">[Proposition 8.13](the-pivot.md#box-16-ns-prop-update)</span>). Hence $\sum_{i \in N}\pi_i$ strictly decreases, while the cost does not change.

    3. A tree structure determines its cost and its potentials. At every pivot the pair $\big(\vet{c}'\vet{x},\, \sum_{i \in N}\pi_i\big)$ strictly decreases in lexicographic order, so no tree structure is met twice; there are finitely many of them. <span class="qed">□</span>

- The proof uses the rule in two points: in a degenerate pivot the leaving arc lies between the apex and $p$, and the new tree is strongly feasible. A different choice among the blocking arcs can produce a tree structure that is not strongly feasible.

- The theorem needs a strongly feasible initial tree structure: when none is known, it is built with an auxiliary network.

!!! chiave ""

    In a strongly feasible tree every node can push flow to the root. Choosing as leaving arc the last blocking arc from the apex keeps this property; then a degenerate pivot lowers the potentials of a subtree, and no tree structure repeats: the algorithm cannot cycle.

---

**Next:** [8.8 A capacitated example with a degenerate pivot](a-capacitated-example-with-a-degenerate-pivot.md)

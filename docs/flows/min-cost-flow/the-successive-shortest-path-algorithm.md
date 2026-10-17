---
title: "The successive shortest path algorithm"
---

# 6.7 The successive shortest path algorithm

<div class="info-capitolo" markdown>

**Part 3 · Flows · Chapter 6** · [:material-book-open-variant: Chapter 6: Minimum cost flow](index.md) · [:material-file-pdf-box: Lecture notes, volume 3 (PDF)](../../pdf/lecture-notes-3-flows.pdf) · [:material-presentation: Slides](../../pdf/slides-min-cost-flow.pdf) · [:material-pencil: Exercises: Minimum cost flow](../../exercises/min-cost-flow.md) · [:material-gesture-tap: App: Minimum cost flow: cycle canceling and successive shortest paths](../../lab/minimum-cost-flow.md)

</div>

<a id="sez-sec-mc-ssp"></a>

<a id="box-21-mc-def-pseudo"></a>

!!! definizione "Definition 6.15: pseudoflow and imbalances"

    A <strong>pseudoflow</strong> is a vector $\vet{x}$ with $\vet{l} \le \vet{x} \le \vet{u}$, which may violate flow conservation. The <strong>imbalance</strong> of node $i$ is

    $$
    e_i=b_i-\Big(\sum_{(i,j) \in \delta^+(i)} x_{ij}-\sum_{(j,i) \in \delta^-(i)} x_{ji}\Big):
    $$

    the supply that $i$ has still to send if $e_i>0$ (an <strong>excess node</strong>), the demand that it has still to receive if $e_i<0$ (a <strong>deficit node</strong>).

- A pseudoflow is a feasible flow exactly when $\vet{e}=\vet{0}$. The imbalances add up to zero, since the balances do and every arc adds $x_{ij}$ to its tail and subtracts it from its head.

- The residual network $G(\vet{x})$ of a pseudoflow is defined as in <span style="color:#1971c2">[Definition 6.1](the-residual-network-with-costs.md#box-1-mc-def-residual)</span>. Augmenting $\vet{x}$ along a path $P$ of $G(\vet{x})$ from $s$ to $t$ by $\delta \le r(P)=\min_{(i,j) \in P}r_{ij}$ is defined as for cycles: the bounds still hold, $e_s$ decreases by $\delta$, $e_t$ increases by $\delta$, and the cost grows by $\delta\, c(P)$, where $c(P)=\sum_{(i,j) \in P} c^x_{ij}$.

- The idea is to keep potentials with non-negative reduced costs on $G(\vet{x})$, the condition of <span style="color:#1971c2">[Theorem 6.9](optimality-conditions-with-potentials.md#box-12-mc-th-potentials)</span>, while the imbalances go to zero. With $\vet{x}=\vet{0}$, $\vet{\pi}= \vet{0}$ and costs $c_{ij} \ge 0$ the condition holds at the start.

<a id="box-22-mc-lem-ssp"></a>

!!! teorema "Lemma 6.16: shortest paths keep the reduced costs non-negative"

    Let $\vet{x}$ be a pseudoflow and $\vet{\pi}$ potentials with $\bar{c}^{\pi}_{ij}=c^x_{ij}-\pi_i+\pi_j \ge 0$ on every arc of $G(\vet{x})$. Let $d(i)$ be the distances from a node $s$ in $G(\vet{x})$ with the lengths $\bar{c}^{\pi}$ ($d(i)=+\infty$ if $i$ is not reachable), $t$ a node with $d(t)<+\infty$, $P$ a shortest path from $s$ to $t$, and

    $$
    \pi'_i=\pi_i-\min\{d(i),d(t)\}, \qquad \forall i \in N .
    $$

    - **(a)** $c^x_{ij}-\pi'_i+\pi'_j \ge 0$ on every arc of $G(\vet{x})$.

    - **(b)** $c^x_{ij}-\pi'_i+\pi'_j=0$ on every arc of $P$.

    - **(c)** If $\vet{x}'$ is $\vet{x}$ augmented along $P$ by $\delta \le r(P)$, then $c^{x'}_{ij}-\pi'_i+\pi'_j \ge 0$ on every arc of $G(\vet{x}')$.

??? dimostrazione "Proof"

    Let $\hat{d}(i)=\min\{d(i),d(t)\}$. The reduced cost of $(i,j)$ with $\vet{\pi}'$ is $\bar{c}^{\pi}_{ij}+\hat{d}(i)- \hat{d}(j)$.

    - **(a)** Let $(i,j)$ be an arc of $G(\vet{x})$. If $d(i)<+\infty$, a shortest path to $i$ followed by $(i,j)$ gives $d(j) \le d(i)+\bar{c}^{\pi}_{ij}$, so $\hat{d}(j) \le \min\{d(i)+\bar{c}^{\pi}_{ij},\,d(t)\} \le \hat{d}(i)+ \bar{c}^{\pi}_{ij}$, since $\bar{c}^{\pi}_{ij} \ge 0$. If $d(i)=+\infty$, then $\hat{d}(i)=d(t) \ge \hat{d}(j)$. In both cases the new reduced cost is non-negative.

    - **(b)** Subpaths of $P$ are shortest (Lemma «optimality of subpaths» of Chapter 3), so $d(j)=d(i)+ \bar{c}^{\pi}_{ij}$ on every arc of $P$, and $d(i) \le d(t)$ along $P$ since the lengths are non-negative. Hence $\hat{d}=d$ on $P$, and the new reduced cost is $0$.

    - **(c)** Augmenting along $P$ changes $G(\vet{x})$ only on the arcs of $P$: an arc $(i,j)$ of $P$ may disappear, and the reverse arc $(j,i)$ may appear. The reverse of a residual arc has the opposite cost, hence by (b) reduced cost $0$; the other arcs keep their reduced costs, non-negative by (a).

    <p class="qed-riga"><span class="qed">□</span></p>

- For every path $P$ from $s$ to $t$ the potentials telescope: $\sum_{(i,j) \in P}\bar{c}^{\pi}_{ij}=c(P)-\pi_s+ \pi_t$. A shortest path for the reduced costs is a minimum cost path of $G(\vet{x})$: the flow travels along cheapest paths, hence the name of the algorithm.

!!! algoritmo "Algorithm: Successive shortest path algorithm"

    <div class="pseudocodice" markdown="0"><div class="pc" style="--liv:0"><strong>Input:</strong> a balanced network with <span class="arithmatex">\(\vet{l}=\vet{0}\)</span>, integer <span class="arithmatex">\(b_i\)</span> and <span class="arithmatex">\(u_{ij}\)</span>, costs <span class="arithmatex">\(c_{ij} \ge 0\)</span></div><div class="pc" style="--liv:0"><strong>Output:</strong> an optimal flow <span class="arithmatex">\(\vet{x}\)</span> with its certificate <span class="arithmatex">\(\vet{\pi}\)</span>, or «infeasible»</div><div class="pc" style="--liv:0"><span class="pc-n">1</span><strong>Step 0 (initialization).</strong> Set <span class="arithmatex">\(\vet{x}:=\vet{0}\)</span>, <span class="arithmatex">\(\vet{\pi}:=\vet{0}\)</span> and <span class="arithmatex">\(\vet{e}:=\vet{b}\)</span>.</div><div class="pc" style="--liv:0"><span class="pc-n">2</span><strong>Step 1 (selection).</strong> If <span class="arithmatex">\(\vet{e}=\vet{0}\)</span>, <code>STOP</code>: <span class="arithmatex">\(\vet{x}\)</span> is optimal, with <span class="arithmatex">\(\vet{\pi}\)</span>.</div><div class="pc" style="--liv:0"><span class="pc-n">3</span>  Otherwise let <span class="arithmatex">\(s\)</span> be the node of smallest index with <span class="arithmatex">\(e_s>0\)</span>.</div><div class="pc" style="--liv:0"><span class="pc-n">4</span><strong>Step 2 (shortest paths).</strong> Run Dijkstra from <span class="arithmatex">\(s\)</span> on <span class="arithmatex">\(G(\vet{x})\)</span>, lengths <span class="arithmatex">\(c^x_{ij}-\pi_i+\pi_j\)</span>.</div><div class="pc" style="--liv:0"><span class="pc-n">5</span>  If no node with <span class="arithmatex">\(e_t<0\)</span> is reachable, <code>STOP</code>: infeasible.</div><div class="pc" style="--liv:0"><span class="pc-n">6</span>  Otherwise <span class="arithmatex">\(t\)</span> is the reachable node with <span class="arithmatex">\(e_t<0\)</span> and smallest <span class="arithmatex">\(d(t)\)</span>, and <span class="arithmatex">\(P\)</span> its path.</div><div class="pc" style="--liv:0"><span class="pc-n">7</span><strong>Step 3 (augmentation).</strong> Set <span class="arithmatex">\(\pi_i:=\pi_i-\min\{d(i),d(t)\}\)</span> for every <span class="arithmatex">\(i \in N\)</span>.</div><div class="pc" style="--liv:0"><span class="pc-n">8</span>  Augment <span class="arithmatex">\(\vet{x}\)</span> along <span class="arithmatex">\(P\)</span> by <span class="arithmatex">\(\delta:=\min\{e_s,-e_t,r(P)\}\)</span>, and update <span class="arithmatex">\(e_s\)</span>, <span class="arithmatex">\(e_t\)</span>.</div><div class="pc" style="--liv:0"><span class="pc-n">9</span>  Go to Step 1.</div></div>

- <strong>Rules of this chapter.</strong> Dijkstra's algorithm breaks ties by the smallest index, as in Chapter 3; among the deficit nodes at the same distance, $t$ is the one of smallest index.

<a id="box-23-mc-th-ssp"></a>

!!! teorema "Theorem 6.17: correctness of the successive shortest path algorithm"

    With the input of the algorithm, at the beginning of every iteration $\vet{x}$ is an integer pseudoflow and $c^x_{ij}-\pi_i+\pi_j \ge 0$ on every arc of $G(\vet{x})$. The algorithm stops after at most $D=\sum_{i: b_i>0}b_i$ iterations. If it stops in Step 1, $\vet{x}$ is an optimal flow; if it stops in Step 2, the network has no feasible flow.

??? dimostrazione "Proof"

    We prove the invariant, then the bound and the two stops.

    1. <em>Invariant.</em> At the start $G(\vet{0})$ has the forward arcs only, with costs $c_{ij} \ge 0$, and $\vet{\pi}=\vet{0}$. Dijkstra's algorithm applies, the lengths being non-negative, and <span style="color:#1971c2">[Lemma 6.16](#box-22-mc-lem-ssp)</span>(c) keeps the reduced costs non-negative. The amount $\delta$ is a positive integer, since $e_s$, $-e_t$ and the residual capacities are positive integers (or $+\infty$), so $\vet{x}$ stays integer.

    2. <em>Bound.</em> If $e_s>0$, some node has $e_t<0$, since the imbalances add up to zero. Every iteration lowers $\sum_{i: e_i>0}e_i$ by $\delta \ge 1$, and no imbalance changes sign, since $\delta \le e_s$ and $\delta \le -e_t$. The sum starts at $D$.

    3. <em>Stop in Step 1.</em> $\vet{e}=\vet{0}$, so $\vet{x}$ is a feasible flow, optimal by the invariant and <span style="color:#1971c2">[Theorem 6.9](optimality-conditions-with-potentials.md#box-12-mc-th-potentials)</span>.

    4. <em>Stop in Step 2.</em> Let $S$ be the set of the nodes reachable from $s$. No arc of $G(\vet{x})$ leaves $S$, so $x_{ij}=u_{ij}$ on $\delta^+(S)$ and $x_{ij}=0$ on $\delta^-(S)$. The pseudoflow satisfies conservation with the balances $b_i-e_i$, so by Lemma «flow across a cut» of Chapter 4

        $$
        \sum_{i \in S} b_i=x(\delta^+(S))-x(\delta^-(S))+\sum_{i \in S} e_i=u(\delta^+(S))+\sum_{i \in S}e_i>u(\delta^+(S)),
        $$

        because $e_s>0$ and no node of $S$ has $e_i<0$. The cut condition of Chapter 4 fails for $S$: there is no feasible flow.

    <p class="qed-riga"><span class="qed">□</span></p>

- <strong>Running time.</strong> Each iteration runs Dijkstra's algorithm in $O(n^2)$ time: $O(D\,n^2)$ in total, a pseudo-polynomial bound.

- <strong>Negative costs.</strong> If some arcs with finite capacity have $c_{ij}<0$, start from $x_{ij}=u_{ij}$ on them and $x_{ij}=0$ elsewhere, with $\vet{e}=\vet{b}-\mat{B}\vet{x}$: such an arc gives only its backward arc, of cost $-c_{ij}>0$, and $\vet{\pi}=\vet{0}$ works again.

### 6.7.1 Successive shortest paths on the reference network

<a id="box-24-mc-ex-ssp"></a>

!!! esempio "Example 6.7: successive shortest paths"

    We start from $\vet{x}=\vet{0}$, $\vet{\pi}=\vet{0}$ and $\vet{e}=\vet{b}=(5,2,0,-3,0,-4)$. In the first table each row is an iteration, with the node $s$, the distances of Dijkstra's algorithm and the node $t$; the second table gives the path $P$, its reduced cost $d(t)$ and its cost $c(P)$, the amount $\delta$ and the cost of the new flow.

    <div class="tabella" markdown="0"><table>
    <tr>
    <th>it.</th>
    <th><span class="arithmatex">\(s\)</span></th>
    <th><span class="arithmatex">\(d(1)\)</span></th>
    <th><span class="arithmatex">\(d(2)\)</span></th>
    <th><span class="arithmatex">\(d(3)\)</span></th>
    <th><span class="arithmatex">\(d(4)\)</span></th>
    <th><span class="arithmatex">\(d(5)\)</span></th>
    <th><span class="arithmatex">\(d(6)\)</span></th>
    <th><span class="arithmatex">\(t\)</span></th>
    </tr>
    <tr>
    <td><span class="arithmatex">\(1\)</span></td>
    <td><span class="arithmatex">\(1\)</span></td>
    <td><span class="arithmatex">\(0\)</span></td>
    <td><span class="arithmatex">\(2\)</span></td>
    <td><span class="arithmatex">\(2\)</span></td>
    <td><span class="arithmatex">\(7\)</span></td>
    <td><span class="arithmatex">\(5\)</span></td>
    <td><span class="arithmatex">\(8\)</span></td>
    <td><span class="arithmatex">\(4\)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">\(2\)</span></td>
    <td><span class="arithmatex">\(1\)</span></td>
    <td><span class="arithmatex">\(0\)</span></td>
    <td><span class="arithmatex">\(0\)</span></td>
    <td><span class="arithmatex">\(0\)</span></td>
    <td><span class="arithmatex">\(0\)</span></td>
    <td><span class="arithmatex">\(0\)</span></td>
    <td><span class="arithmatex">\(1\)</span></td>
    <td><span class="arithmatex">\(6\)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">\(3\)</span></td>
    <td><span class="arithmatex">\(2\)</span></td>
    <td><span class="arithmatex">\(0\)</span></td>
    <td><span class="arithmatex">\(0\)</span></td>
    <td><span class="arithmatex">\(0\)</span></td>
    <td><span class="arithmatex">\(0\)</span></td>
    <td><span class="arithmatex">\(0\)</span></td>
    <td><span class="arithmatex">\(4\)</span></td>
    <td><span class="arithmatex">\(6\)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">\(4\)</span></td>
    <td><span class="arithmatex">\(2\)</span></td>
    <td><span class="arithmatex">\(0\)</span></td>
    <td><span class="arithmatex">\(0\)</span></td>
    <td><span class="arithmatex">\(0\)</span></td>
    <td><span class="arithmatex">\(3\)</span></td>
    <td><span class="arithmatex">\(0\)</span></td>
    <td><span class="arithmatex">\(3\)</span></td>
    <td><span class="arithmatex">\(6\)</span></td>
    </tr>
    </table></div>

    <div class="tabella" markdown="0"><table>
    <tr>
    <th>it.</th>
    <th><span class="arithmatex">\(P\)</span></th>
    <th><span class="arithmatex">\(d(t)\)</span></th>
    <th><span class="arithmatex">\(c(P)\)</span></th>
    <th><span class="arithmatex">\(\delta\)</span></th>
    <th>cost</th>
    </tr>
    <tr>
    <td><span class="arithmatex">\(1\)</span></td>
    <td><span class="arithmatex">\(1,2,4\)</span></td>
    <td><span class="arithmatex">\(7\)</span></td>
    <td><span class="arithmatex">\(7\)</span></td>
    <td><span class="arithmatex">\(3\)</span></td>
    <td><span class="arithmatex">\(21\)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">\(2\)</span></td>
    <td><span class="arithmatex">\(1,3,5,6\)</span></td>
    <td><span class="arithmatex">\(1\)</span></td>
    <td><span class="arithmatex">\(8\)</span></td>
    <td><span class="arithmatex">\(2\)</span></td>
    <td><span class="arithmatex">\(37\)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">\(3\)</span></td>
    <td><span class="arithmatex">\(2,4,6\)</span></td>
    <td><span class="arithmatex">\(4\)</span></td>
    <td><span class="arithmatex">\(10\)</span></td>
    <td><span class="arithmatex">\(1\)</span></td>
    <td><span class="arithmatex">\(47\)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">\(4\)</span></td>
    <td><span class="arithmatex">\(2,1,3,5,4,6\)</span></td>
    <td><span class="arithmatex">\(3\)</span></td>
    <td><span class="arithmatex">\(13\)</span></td>
    <td><span class="arithmatex">\(1\)</span></td>
    <td><span class="arithmatex">\(60\)</span></td>
    </tr>
    </table></div>

    The third table gives, after each iteration, the potentials, the imbalances and the flow.

    <div class="tabella" markdown="0"><table>
    <tr>
    <th>it.</th>
    <th><span class="arithmatex">\(\vet{\pi}\)</span></th>
    <th><span class="arithmatex">\(\vet{e}\)</span></th>
    <th><span class="arithmatex">\(\vet{x}\)</span></th>
    </tr>
    <tr>
    <td><span class="arithmatex">\(0\)</span></td>
    <td><span class="arithmatex">\((0,0,0,0,0,0)\)</span></td>
    <td><span class="arithmatex">\((5,2,0,-3,0,-4)\)</span></td>
    <td><span class="arithmatex">\((0,0,0,0,0,0,0,0,0)\)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">\(1\)</span></td>
    <td><span class="arithmatex">\((0,-2,-2,-7,-5,-7)\)</span></td>
    <td><span class="arithmatex">\((2,2,0,0,0,-4)\)</span></td>
    <td><span class="arithmatex">\((3,0,3,0,0,0,0,0,0)\)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">\(2\)</span></td>
    <td><span class="arithmatex">\((0,-2,-2,-7,-5,-8)\)</span></td>
    <td><span class="arithmatex">\((0,2,0,0,0,-2)\)</span></td>
    <td><span class="arithmatex">\((3,2,3,0,2,0,0,0,2)\)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">\(3\)</span></td>
    <td><span class="arithmatex">\((0,-2,-2,-7,-5,-12)\)</span></td>
    <td><span class="arithmatex">\((0,1,0,0,0,-1)\)</span></td>
    <td><span class="arithmatex">\((3,2,4,0,2,0,1,0,2)\)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">\(4\)</span></td>
    <td><span class="arithmatex">\((0,-2,-2,-10,-5,-15)\)</span></td>
    <td><span class="arithmatex">\((0,0,0,0,0,0)\)</span></td>
    <td><span class="arithmatex">\((2,3,4,0,3,0,2,1,2)\)</span></td>
    </tr>
    </table></div>

    The reduced costs $\bar{c}_{ij}=c_{ij}-\pi_i+\pi_j$ of the arcs of $A$, before each iteration, are (the forward arc has $\bar{c}_{ij}$ if $x_{ij}<u_{ij}$, the backward arc $-\bar{c}_{ij}$ if $x_{ij}>0$):

    <div class="tabella" markdown="0"><table>
    <tr>
    <th>it.</th>
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
    <td><span class="arithmatex">\(1\)</span></td>
    <td><span class="arithmatex">\(2\)</span></td>
    <td><span class="arithmatex">\(2\)</span></td>
    <td><span class="arithmatex">\(5\)</span></td>
    <td><span class="arithmatex">\(2\)</span></td>
    <td><span class="arithmatex">\(3\)</span></td>
    <td><span class="arithmatex">\(3\)</span></td>
    <td><span class="arithmatex">\(5\)</span></td>
    <td><span class="arithmatex">\(5\)</span></td>
    <td><span class="arithmatex">\(3\)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">\(2\)</span></td>
    <td><span class="arithmatex">\(0\)</span></td>
    <td><span class="arithmatex">\(0\)</span></td>
    <td><span class="arithmatex">\(0\)</span></td>
    <td><span class="arithmatex">\(2\)</span></td>
    <td><span class="arithmatex">\(0\)</span></td>
    <td><span class="arithmatex">\(8\)</span></td>
    <td><span class="arithmatex">\(5\)</span></td>
    <td><span class="arithmatex">\(3\)</span></td>
    <td><span class="arithmatex">\(1\)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">\(3\)</span></td>
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
    <tr>
    <td><span class="arithmatex">\(4\)</span></td>
    <td><span class="arithmatex">\(0\)</span></td>
    <td><span class="arithmatex">\(0\)</span></td>
    <td><span class="arithmatex">\(0\)</span></td>
    <td><span class="arithmatex">\(2\)</span></td>
    <td><span class="arithmatex">\(0\)</span></td>
    <td><span class="arithmatex">\(8\)</span></td>
    <td><span class="arithmatex">\(0\)</span></td>
    <td><span class="arithmatex">\(3\)</span></td>
    <td><span class="arithmatex">\(-4\)</span></td>
    </tr>
    </table></div>

    - <em>Iteration $1$.</em> The reduced costs are the costs. The deficit nodes $4$ and $6$ are at distance $7$ and $8$: $t=4$, and $\delta=\min\{5,3,4,4\}=3$. Node $6$ is farther than $t$ and its potential decreases by $7$, not $8$.

    - <em>Iteration $2$.</em> The arcs $(1,2)$, $(2,4)$ of the first path now have reduced cost $0$, and so do their backward arcs. The path $1,3,5,6$ has reduced cost $1$ and cost $8$; $\delta=\min\{2,4,4,4,2\}=2$ is set by $e_1$ and by $u_{56}$.

    - <em>Iteration $3$.</em> $s=2$, and $d(1)=0$ through the backward arc $(2,1)$. The path $2,4,6$ uses the last unit of $(2,4)$.

    - <em>Iteration $4$.</em> The path $2,1,3,5,4,6$ uses the backward arc $(2,1)$: one unit that went from $1$ to $2$ is rerouted from $1$ through $3$, $5$ and $4$. The figure shows $G(\vet{x})$ with $r_{ij}$ and the reduced cost on each arc, and the path in blue.

    ![Figure 3](../../img/min-cost-flow/fig03.svg){ .fig loading=lazy  }

    After iteration $4$ the imbalances are zero and $\vet{x}=\tilde{\vet{x}}$, of cost $60$. Shifted by $15$, the potentials become $(15,13,13,5,10,0)$: the potentials of Chapter 4.

- Here the costs $7,8,10,13$ of the paths grow from one iteration to the next: later units travel along more expensive paths, and the total cost is $3 \cdot 7+2 \cdot 8+10+13=60$.

- Four iterations are enough here, while the bound of <span style="color:#1971c2">[Theorem 6.17](#box-23-mc-th-ssp)</span> is $D=7$.

!!! attenzione "Dijkstra needs the reduced costs"

    In iteration $4$ the arcs $(2,1)$, $(3,1)$, $(4,2)$, $(5,3)$, $(6,4)$, $(6,5)$ of $G(\vet{x})$ are backward arcs with negative costs $c^x_{ij}$, and Dijkstra's algorithm with negative lengths can fail ([Chapter 3](https://fabiofurini.github.io/network-optimization/trees-and-paths/shortest-paths/dijkstra-s-algorithm/)). The potentials make all the lengths non-negative without changing the shortest paths.

!!! chiave ""

    The successive shortest path algorithm sends flow from an excess node to a deficit node along a shortest path of $G(\vet{x})$, found by Dijkstra's algorithm on the reduced costs. The update $\pi_i:=\pi_i-\min\{d(i),d(t)\}$ keeps the reduced costs non-negative, so the final flow is optimal and the potentials certify it.

## 6.8 Typical mistakes

!!! attenzione "Warning"

    - <strong>Giving the backward arc the cost $+c_{ij}$.</strong> A backward arc decreases $x_{ij}$, so it saves $c_{ij}$ per unit: its cost is $-c_{ij}$, and its residual capacity is $x_{ij}-l_{ij}$.

    - <strong>Augmenting by more than $r(W)$.</strong> Some arc of the cycle would leave its bounds; $\theta=r(W)$ is the largest step.

    - <strong>Running Bellman–Ford from a single node.</strong> A negative cycle that is not reachable from that node is missed; the labels start at $0$ on every node.

    - <strong>Taking the walk for the cycle.</strong> The walk with $n$ arcs read from the table contains a negative cycle, but it is not a cycle itself: the cycle is the piece between two occurrences of the same node.

    - <strong>Running Dijkstra's algorithm on the costs $c^x_{ij}$.</strong> Backward arcs can have negative costs; the lengths are the reduced costs $c^x_{ij}-\pi_i+\pi_j$.

    - <strong>Updating the potentials with the wrong sign.</strong> With $\bar{c}_{ij}=c_{ij}-\pi_i+\pi_j$ the update is $\pi_i:=\pi_i-\min\{d(i),d(t)\}$; the nodes farther than $t$ decrease by $d(t)$ only.

    - <strong>Taking the maximum flow of Step 0 as optimal.</strong> The auxiliary network has no costs: its maximum flow is feasible, and optimal only by chance.

## 6.9 In summary

!!! chiave "In summary"

    - The residual network $G(\vet{x})$ has a forward arc $(i,j)$ with $r_{ij}=u_{ij}-x_{ij}$ and cost $c_{ij}$, and a backward arc $(j,i)$ with $r_{ji}=x_{ij}-l_{ij}$ and cost $-c_{ij}$; augmenting along a cycle $W$ changes the cost by $\theta\,c(W)$.

    - A circulation decomposes into cycles; the difference of two feasible flows is a circulation on $G(\vet{x})$.

    - A feasible flow is optimal if and only if $G(\vet{x})$ has no negative cycle, if and only if some potentials give non-negative reduced costs on $G(\vet{x})$; on the arcs of $A$: $\bar{c}_{ij}>0 \Rightarrow x_{ij}=l_{ij}$, $\bar{c}_{ij}<0 \Rightarrow x_{ij}=u_{ij}$.

    - A maximum flow from a super source to a super sink finds a feasible flow or proves that there is none.

    - Cycle canceling: Bellman–Ford from labels $0$ finds a negative cycle, augmenting by $r(W)$ cancels it; at most $\vet{c}'\vet{x}^0-z(\mathrm{MCF})$ iterations with integer data.

    - Successive shortest paths: Dijkstra on the reduced costs from an excess node to the nearest deficit node, $\pi_i:=\pi_i-\min\{d(i),d(t)\}$; at most $D$ iterations.

    <strong>The reference network at a glance.</strong>

    <div class="tabella" markdown="0"><table>
    <tr>
    <td>most expensive flow</td>
    <td><span class="arithmatex">\(\vet{x}^0=(1,4,4,1,4,1,3,3,1)\)</span>, cost <span class="arithmatex">\(80\)</span></td>
    </tr>
    <tr>
    <td>cycle canceling from <span class="arithmatex">\(\vet{x}^0\)</span></td>
    <td>cycles <span class="arithmatex">\(4,5,3,4\)</span>; <span class="arithmatex">\(6,4,5,6\)</span>; <span class="arithmatex">\(3,1,2,3\)</span>: costs <span class="arithmatex">\(80,69,62,60\)</span></td>
    </tr>
    <tr>
    <td>successive shortest paths</td>
    <td>paths <span class="arithmatex">\(1,2,4\)</span>; <span class="arithmatex">\(1,3,5,6\)</span>; <span class="arithmatex">\(2,4,6\)</span>; <span class="arithmatex">\(2,1,3,5,4,6\)</span>: costs <span class="arithmatex">\(21,37,47,60\)</span></td>
    </tr>
    <tr>
    <td>first feasible flow</td>
    <td>maximum flow of value <span class="arithmatex">\(7\)</span>; on <span class="arithmatex">\(A\)</span> it is <span class="arithmatex">\(\tilde{\vet{x}}\)</span></td>
    </tr>
    <tr>
    <td>optimal flow</td>
    <td><span class="arithmatex">\(\tilde{\vet{x}}=(2,3,4,0,3,0,2,1,2)\)</span>, <span class="arithmatex">\(z(\mathrm{MCF})=60\)</span></td>
    </tr>
    <tr>
    <td>potentials (<span class="arithmatex">\(\pi_6=0\)</span>)</td>
    <td><span class="arithmatex">\(\vet{\pi}=(15,13,13,5,10,0)\)</span></td>
    </tr>
    </table></div>

---

**Exercises on this chapter:** [:material-pencil: Minimum cost flow](../../exercises/min-cost-flow.md)


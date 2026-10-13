---
title: "The cycle-canceling algorithm"
---

# 6.6 The cycle-canceling algorithm { #sez-sec-mc-cycle-canceling }

<div class="info-capitolo" markdown>

**Part 3 · Flows · Chapter 6** · [:material-book-open-variant: Chapter 6: Minimum cost flow](index.md) · [:material-file-pdf-box: Lecture notes, volume 3 (PDF)](../../pdf/lecture-notes-3-flows.pdf) · [:material-pencil: Exercises: Minimum cost flow](../../exercises/min-cost-flow.md)

</div>

- <span style="color:#1971c2">[Theorem 6.7](negative-cycle-optimality-conditions.md#box-9-mc-th-negcycle)</span> suggests an algorithm due to Klein: while $G(\vet{x})$ has a negative cycle, augment along it. Augmenting by $r(W)$ saturates an arc of $W$, which leaves $G(\vet{x})$: the cycle is <strong>canceled</strong>.

## 6.6.1 Finding a negative cycle

- A negative cycle of $G(\vet{x})$ need not be reachable from a given node. We run the Bellman–Ford algorithm of [Chapter 3](https://fabiofurini.github.io/network-optimization/trees-and-paths/shortest-paths/the-bellman-ford-algorithm/) from a new node $r$ joined to every node by an arc of cost $0$; its first pass gives label $0$ to every node, and we write the table from there.

<a id="box-18-mc-prop-bf"></a>

!!! teorema "Proposition 6.13: Bellman–Ford on the residual network"

    Let $d^0(j)=0$ for every $j \in N$ and, for $k \ge 1$,

    $$
    d^k(j)=\min\Big\{\, d^{k-1}(j),\; \min_{(i,j) \in A(\vet{x})} \big(d^{k-1}(i)+c^x_{ij}\big) \Big\},
    \qquad \forall j \in N .
    $$

    - **(a)** $d^k(j)$ is the minimum cost of a walk of $G(\vet{x})$ with at most $k$ arcs that ends at $j$, the walk without arcs having cost $0$.

    - **(b)** $G(\vet{x})$ has a negative cycle if and only if $d^n \neq d^{n-1}$. In that case, if $d^n(j)<d^{n-1}(j)$, the predecessors read backwards from $j$, one row per pass from row $n$ to row $1$, give a walk of $G(\vet{x})$ with $n$ arcs, ending at $j$, that contains a negative cycle.

    - **(c)** If $d^k=d^{k-1}$ for some $k \le n$, the potentials $\pi_i=-d^k(i)$ satisfy $c^x_{ij}-\pi_i+\pi_j \ge 0$ on every arc of $G(\vet{x})$.

??? dimostrazione "Proof"

    Let $H$ be $G(\vet{x})$ plus the node $r$ and the arcs $(r,i)$ of cost $0$, and let $D^k$ be the labels of Bellman–Ford from $r$ in $H$: $D^1(i)=0$ for every $i \in N$, and $D^k(r)=0$ for every $k$.

    1. By induction on $k$, $D^{k+1}(j)=d^k(j)$ for $j \in N$: the recursions coincide, and the arc $(r,j)$ offers $D^k(r)+0=0$, which never lowers the minimum since $d^{k-1}(j) \le d^0(j)=0$. A walk from $r$ with $k+1$ arcs is an arc $(r,i)$ followed by a walk of $G(\vet{x})$ with $k$ arcs from $i$: this proves (a).

    2. In $H$ every node is reachable from $r$, and the cycles are those of $G(\vet{x})$. By Theorem «detection of a negative cycle» of Chapter 3, applied to the $n+1$ nodes of $H$, a negative cycle exists if and only if $D^{n+1} \neq D^{n}$, that is $d^n \neq d^{n-1}$. The walk from $r$ with $n+1$ arcs read in rows $n+1,\dots,2$ of $H$, which are our rows $n,\dots,1$, contains a negative cycle; without its first arc $(r,\cdot)$ it is a walk of $G(\vet{x})$ with $n$ arcs, and the cycle does not contain $r$. This proves (b).

    3. If $d^k=d^{k-1}$, the next pass repeats the labels: $d^k(j) \le d^k(i)+c^x_{ij}$ for every arc $(i,j)$ of $G(\vet{x})$, which is (c) with $\pi=-d^k$. <span class="qed">□</span>

- <strong>Rules of this chapter.</strong> The arcs of $G(\vet{x})$ are scanned in lexicographic order; as in Chapter 3, ties in the minimum go to the smallest tail and a predecessor changes only when the label strictly decreases. If $d^n \neq d^{n-1}$, $j$ is the smallest node with $d^n(j)<d^{n-1}(j)$, and the cycle is the piece of the walk between the two occurrences of the first node met twice, reading the walk from its first node.

- At the stop the potentials $\pi_i=-d^k(i)$ are shifted so that $\pi_n=0$.

## 6.6.2 The algorithm

!!! algoritmo "Algorithm: Cycle-canceling algorithm"

    <div class="pseudocodice" markdown="0"><div class="pc" style="--liv:0"><strong>Input:</strong> a balanced network with <span class="arithmatex">\(\vet{l}=\vet{0}\)</span>, capacities <span class="arithmatex">\(u_{ij}\)</span>, costs <span class="arithmatex">\(c_{ij}\)</span></div><div class="pc" style="--liv:0"><strong>Output:</strong> an optimal flow <span class="arithmatex">\(\vet{x}\)</span> with its certificate <span class="arithmatex">\(\vet{\pi}\)</span>, or «infeasible», or «unbounded»</div><div class="pc" style="--liv:0"><span class="pc-n">1</span><strong>Step 0 (start).</strong> If a cycle of arcs with <span class="arithmatex">\(u_{ij}=+\infty\)</span> has negative cost, <code>STOP</code>: unbounded.</div><div class="pc" style="--liv:0"><span class="pc-n">2</span>  Find a feasible flow <span class="arithmatex">\(\vet{x}\)</span> with a maximum flow of the auxiliary network.</div><div class="pc" style="--liv:0"><span class="pc-n">3</span>  If its value is less than <span class="arithmatex">\(D\)</span>, <code>STOP</code>: infeasible.</div><div class="pc" style="--liv:0"><span class="pc-n">4</span><strong>Step 1 (negative cycle).</strong> Run Bellman–Ford on <span class="arithmatex">\(G(\vet{x})\)</span> from <span class="arithmatex">\(d^0=\vet{0}\)</span>.</div><div class="pc" style="--liv:0"><span class="pc-n">5</span>  If <span class="arithmatex">\(d^k=d^{k-1}\)</span> for some <span class="arithmatex">\(k \le n\)</span>, <code>STOP</code>: <span class="arithmatex">\(\vet{x}\)</span> is optimal, with <span class="arithmatex">\(\vet{\pi}=-d^k\)</span>.</div><div class="pc" style="--liv:0"><span class="pc-n">6</span>  Otherwise read a negative cycle <span class="arithmatex">\(W\)</span> from the table.</div><div class="pc" style="--liv:0"><span class="pc-n">7</span><strong>Step 2 (cancel).</strong> Augment <span class="arithmatex">\(\vet{x}\)</span> along <span class="arithmatex">\(W\)</span> by <span class="arithmatex">\(\theta=r(W)\)</span> and go to Step 1.</div></div>

- The test of Step 0 is <span style="color:#1971c2">[Proposition 6.13](#box-18-mc-prop-bf)</span> applied to the graph of the arcs with $u_{ij}=+\infty$ and their costs. When it fails, every negative cycle of $G(\vet{x})$ has an arc of finite residual capacity (proof of <span style="color:#1971c2">[Proposition 6.8](negative-cycle-optimality-conditions.md#box-10-mc-prop-unbounded)</span>), so $r(W)<+\infty$ in Step 2.

- Any feasible flow can be used in Step 0; the maximum flow is one way to find it.

<a id="box-19-mc-th-cc"></a>

!!! teorema "Theorem 6.14: correctness of cycle canceling"

    Let the balances, the capacities and the costs be integer, with capacities possibly $+\infty$, and let the algorithm pass Step 0 with an integer feasible flow $\vet{x}^0$. Then every flow of the algorithm is integer and feasible, every iteration lowers the cost by at least $1$, and the algorithm stops after at most $\vet{c}'\vet{x}^0-z(\mathrm{MCF})$ iterations with an optimal flow.

??? dimostrazione "Proof"

    By <span style="color:#1971c2">[Proposition 6.8](negative-cycle-optimality-conditions.md#box-10-mc-prop-unbounded)</span> the model is bounded, so it has an optimal value $z(\mathrm{MCF})$.

    1. If $\vet{x}$ is integer, the residual capacities are positive integers or $+\infty$, and $r(W)$ is a positive integer, since $r(W)<+\infty$. By <span style="color:#1971c2">[Proposition 6.3](the-residual-network-with-costs.md#box-3-mc-prop-augment)</span> the new flow is feasible and integer.

    2. The cost changes by $r(W)\,c(W)$, where $r(W) \ge 1$ and $c(W) \le -1$ are integers: it decreases by at least $1$.

    3. The cost starts at $\vet{c}'\vet{x}^0$ and never goes below $z(\mathrm{MCF})$, so there are at most $\vet{c}'\vet{x}^0-z(\mathrm{MCF})$ iterations. At the stop $G(\vet{x})$ has no negative cycle (<span style="color:#1971c2">[Proposition 6.13](#box-18-mc-prop-bf)</span>), and $\vet{x}$ is optimal by <span style="color:#1971c2">[Theorem 6.7](negative-cycle-optimality-conditions.md#box-9-mc-th-negcycle)</span>. <span class="qed">□</span>

- <strong>Running time.</strong> $G(\vet{x})$ has at most $2m$ arcs, so Step 1 takes $O(n\,m)$ time. With finite capacities, $U=\max u_{ij}$ and $K=\max |c_{ij}|$, every flow costs between $-mKU$ and $mKU$: at most $2mKU$ iterations, and $O(n\,m^2 K U)$ time.

- The bound depends on the size of the numbers $K$ and $U$, not only on $n$ and $m$: it is a <strong>pseudo-polynomial</strong> bound.

## 6.6.3 Cycle canceling on the reference network

- On the reference network Step 0 returns $\tilde{\vet{x}}$ (<span style="color:#1971c2">[Example 6.5](a-first-feasible-flow.md#box-17-mc-ex-feasible)</span>), and the algorithm stops at the first Bellman–Ford run. To see it at work, we start from the most expensive flow $\vet{x}^0$ of <span style="color:#1971c2">[Example 6.1](the-residual-network-with-costs.md#box-4-mc-ex-residual)</span>, of cost $80$.

- In the tables each row is a pass $k$; next to a label that decreased, its new predecessor in brackets. The entries read backwards to find the walk are in bold.

<a id="box-20-mc-ex-cc"></a>

!!! esempio "Example 6.6: cycle canceling from the most expensive flow"

    <strong>Iteration 1</strong><br> $G(\vet{x}^0)$ is the residual network of <span style="color:#1971c2">[Example 6.1](the-residual-network-with-costs.md#box-4-mc-ex-residual)</span>. Bellman–Ford gives:

    $$
    \begin{array}{c|cccccc}
    \hline {k} & {d^k(1)} & {d^k(2)} & {d^k(3)} & {d^k(4)} & {d^k(5)} & {d^k(6)} \\
    \hline {0} & {0} & {0} & {0} & {0} & {0} & {0} \\
    {1} & {-2} ({2}) & {-5} ({4}) & {-3} ({5}) & {\mathbf{-5}} ({\mathbf{6}}) & {-5} ({4}) & {0} \\
    {2} & {-7} ({2}) & {-10} ({4}) & {-8} ({5}) & {-6} ({3}) & {\mathbf{-10}} ({\mathbf{4}}) & {-2} ({5}) \\
    {3} & {-12} ({2}) & {-11} ({4}) & {\mathbf{-13}} ({\mathbf{5}}) & {-11} ({3}) & {-11} ({4}) & {-7} ({5}) \\
    {4} & {-15} ({3}) & {-16} ({4}) & {-14} ({5}) & {\mathbf{-16}} ({\mathbf{3}}) & {-16} ({4}) & {-8} ({5}) \\
    {5} & {-18} ({2}) & {\mathbf{-21}} ({\mathbf{4}}) & {-19} ({5}) & {-17} ({3}) & {-21} ({4}) & {-13} ({5}) \\
    {6} & {\mathbf{-23}} ({\mathbf{2}}) & {-22} ({4}) & {-24} ({5}) & {-22} ({3}) & {-22} ({4}) & {-18} ({5}) \\
    \hline
    \end{array}
    $$

    All the labels decrease in pass $6$, so $j=1$. Reading backwards: row $6$ gives $2$, row $5$ for node $2$ gives $4$, then $3$, $5$, $4$, $6$. The walk $6,4,5,3,4,2,1$ meets node $4$ twice: $W=4,5,3,4$, with $c(W)=-11$ and $r(W)=1$. The new flow is $\vet{x}^1=(1,4,4,1,3,0,3,2,1)$, of cost $69$.

    <strong>Iteration 2</strong><br> The arcs of $W$ change: $(4,5)$ and $(5,3)$ lose one unit, $(3,4)$ disappears, and the forward arcs $(3,5)$, $(5,4)$ appear. $G(\vet{x}^1)$ is:

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
    <td><span class="arithmatex">\(x^1_{ij}\)</span></td>
    <td><span class="arithmatex">\(1\)</span></td>
    <td><span class="arithmatex">\(4\)</span></td>
    <td><span class="arithmatex">\(4\)</span></td>
    <td><span class="arithmatex">\(1\)</span></td>
    <td><span class="arithmatex">\(3\)</span></td>
    <td><span class="arithmatex">\(0\)</span></td>
    <td><span class="arithmatex">\(3\)</span></td>
    <td><span class="arithmatex">\(2\)</span></td>
    <td><span class="arithmatex">\(1\)</span></td>
    </tr>
    <tr>
    <td>forward <span class="arithmatex">\((i,j)\)</span>: <span class="arithmatex">\(r,c\)</span></td>
    <td><span class="arithmatex">\(3,2\)</span></td>
    <td>–</td>
    <td>–</td>
    <td><span class="arithmatex">\(1,2\)</span></td>
    <td><span class="arithmatex">\(1,3\)</span></td>
    <td><span class="arithmatex">\(3,3\)</span></td>
    <td><span class="arithmatex">\(2,5\)</span></td>
    <td><span class="arithmatex">\(1,5\)</span></td>
    <td><span class="arithmatex">\(1,3\)</span></td>
    </tr>
    <tr>
    <td>backward <span class="arithmatex">\((j,i)\)</span>: <span class="arithmatex">\(r,c\)</span></td>
    <td><span class="arithmatex">\(1,-2\)</span></td>
    <td><span class="arithmatex">\(4,-2\)</span></td>
    <td><span class="arithmatex">\(4,-5\)</span></td>
    <td><span class="arithmatex">\(1,-2\)</span></td>
    <td><span class="arithmatex">\(3,-3\)</span></td>
    <td>–</td>
    <td><span class="arithmatex">\(3,-5\)</span></td>
    <td><span class="arithmatex">\(2,-5\)</span></td>
    <td><span class="arithmatex">\(1,-3\)</span></td>
    </tr>
    </table></div>

    $$
    \begin{array}{c|cccccc}
    \hline {k} & {d^k(1)} & {d^k(2)} & {d^k(3)} & {d^k(4)} & {d^k(5)} & {d^k(6)} \\
    \hline {0} & {0} & {0} & {0} & {0} & {0} & {0} \\
    {1} & {-2} ({2}) & {-5} ({4}) & {-3} ({5}) & {\mathbf{-5}} ({\mathbf{6}}) & {-5} ({4}) & {0} \\
    {2} & {-7} ({2}) & {-10} ({4}) & {-8} ({5}) & {-5} & {\mathbf{-10}} ({\mathbf{4}}) & {-2} ({5}) \\
    {3} & {-12} ({2}) & {-10} & {-13} ({5}) & {-7} ({6}) & {-10} & {\mathbf{-7}} ({\mathbf{5}}) \\
    {4} & {-15} ({3}) & {-12} ({4}) & {-13} & {\mathbf{-12}} ({\mathbf{6}}) & {-12} ({4}) & {-7} \\
    {5} & {-15} & {\mathbf{-17}} ({\mathbf{4}}) & {-15} ({5}) & {-12} & {-17} ({4}) & {-9} ({5}) \\
    {6} & {\mathbf{-19}} ({\mathbf{2}}) & {-17} & {-20} ({5}) & {-14} ({6}) & {-17} & {-14} ({5}) \\
    \hline
    \end{array}
    $$

    Again $j=1$, and the walk is $6,4,5,6,4,2,1$: $W=6,4,5,6$, made of the backward arcs of $(4,6)$ and $(5,4)$ and of the forward arc $(5,6)$, with $c(W)=-5-5+3=-7$ and $r(W)=\min\{3,2,1\}=1$. The new flow is $\vet{x}^2=(1,4,4,1,3,0,2,1,2)$, of cost $62$.

    <strong>Iteration 3</strong><br> In $G(\vet{x}^2)$ the arc $(5,6)$ is saturated: only its backward arc $(6,5)$ remains, with $r=2$, and the arcs $(6,4)$, $(4,5)$ have residual capacities $2$ and $1$, the forward arcs $(4,6)$, $(5,4)$ residual capacities $3$ and $2$. Bellman–Ford gives:

    $$
    \begin{array}{c|cccccc}
    \hline {k} & {d^k(1)} & {d^k(2)} & {d^k(3)} & {d^k(4)} & {d^k(5)} & {d^k(6)} \\
    \hline {0} & {0} & {0} & {0} & {0} & {0} & {0} \\
    {1} & {-2} ({2}) & {-5} ({4}) & {-3} ({5}) & {\mathbf{-5}} ({\mathbf{6}}) & {-5} ({4}) & {0} \\
    {2} & {-7} ({2}) & {-10} ({4}) & {-8} ({5}) & {-5} & {\mathbf{-10}} ({\mathbf{4}}) & {0} \\
    {3} & {-12} ({2}) & {-10} & {\mathbf{-13}} ({\mathbf{5}}) & {-5} & {-10} & {0} \\
    {4} & {\mathbf{-15}} ({\mathbf{3}}) & {-11} ({3}) & {-13} & {-5} & {-10} & {0} \\
    {5} & {-15} & {\mathbf{-13}} ({\mathbf{1}}) & {-13} & {-5} & {-10} & {0} \\
    {6} & {-15} & {-13} & {\mathbf{-15}} ({\mathbf{2}}) & {-5} & {-10} & {0} \\
    \hline
    \end{array}
    $$

    Only node $3$ decreases in pass $6$: $j=3$, and the walk is $6,4,5,3,1,2,3$. Node $3$ is met twice: $W=3,1,2,3$, made of the backward arc of $(1,3)$, the forward arc $(1,2)$ and the backward arc of $(3,2)$, with $c(W)=-2+2-2=-2$ and $r(W)=\min\{4,3,1\}=1$. The new flow is $\vet{x}^3=(2,3,4,0,3,0,2,1,2)=\tilde{\vet{x}}$, of cost $60$.

    <strong>Iteration 4</strong><br> Bellman–Ford on $G(\tilde{\vet{x}})$ repeats the rows $0$–$5$ of iteration $3$, and in pass $6$ no label decreases: $d^6=d^5=(-15,-13,-13,-5,-10,0)$. The algorithm stops with $\tilde{\vet{x}}$, certified by $\vet{\pi}=-d^6=(15,13,13,5,10,0)$, already normalized with $\pi_6=0$: the potentials of Chapter 4.

- In summary:

    <div class="tabella" markdown="0"><table>
    <tr>
    <th>iteration</th>
    <th>cost of <span class="arithmatex">\(\vet{x}\)</span></th>
    <th><span class="arithmatex">\(j\)</span></th>
    <th>cycle <span class="arithmatex">\(W\)</span></th>
    <th><span class="arithmatex">\(c(W)\)</span></th>
    <th><span class="arithmatex">\(r(W)\)</span></th>
    </tr>
    <tr>
    <td><span class="arithmatex">\(1\)</span></td>
    <td><span class="arithmatex">\(80\)</span></td>
    <td><span class="arithmatex">\(1\)</span></td>
    <td><span class="arithmatex">\(4,5,3,4\)</span></td>
    <td><span class="arithmatex">\(-11\)</span></td>
    <td><span class="arithmatex">\(1\)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">\(2\)</span></td>
    <td><span class="arithmatex">\(69\)</span></td>
    <td><span class="arithmatex">\(1\)</span></td>
    <td><span class="arithmatex">\(6,4,5,6\)</span></td>
    <td><span class="arithmatex">\(-7\)</span></td>
    <td><span class="arithmatex">\(1\)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">\(3\)</span></td>
    <td><span class="arithmatex">\(62\)</span></td>
    <td><span class="arithmatex">\(3\)</span></td>
    <td><span class="arithmatex">\(3,1,2,3\)</span></td>
    <td><span class="arithmatex">\(-2\)</span></td>
    <td><span class="arithmatex">\(1\)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">\(4\)</span></td>
    <td><span class="arithmatex">\(60\)</span></td>
    <td>–</td>
    <td>no negative cycle</td>
    <td>–</td>
    <td>–</td>
    </tr>
    </table></div>

- The bound of <span style="color:#1971c2">[Theorem 6.14](#box-19-mc-th-cc)</span> allows $80-60=20$ iterations; three are enough. The three cycles are the cycles of the decomposition of <span style="color:#1971c2">[Example 6.2](circulations-and-their-decomposition.md#box-8-mc-ex-decomp)</span>, found in a different order.

!!! chiave ""

    The cycle-canceling algorithm starts from a feasible flow and cancels negative cycles of $G(\vet{x})$, found by Bellman–Ford from labels all equal to $0$. With integer data every cancellation lowers the cost by at least $1$; at the stop the labels give the potentials that certify the optimal flow.

---

**Next:** [6.7 The successive shortest path algorithm](the-successive-shortest-path-algorithm.md)

---
title: "Dijkstra's algorithm"
---

# 3.6 Dijkstra's algorithm

<div class="info-capitolo" markdown>

**Part 2 · Trees and paths · Chapter 3** · [:material-book-open-variant: Chapter 3: Shortest paths](index.md) · [:material-file-pdf-box: Lecture notes, volume 2 (PDF)](../../pdf/lecture-notes-2-trees-and-paths.pdf) · [:material-pencil: Exercises: Shortest paths](../../exercises/shortest-paths.md) · [:material-gesture-tap: App: Shortest paths: Dijkstra, Bellman–Ford, acyclic graphs](../../lab/shortest-paths-dijkstra-bellman-ford.md)

</div>

<a id="sez-sec-sp-dijkstra"></a>
- In this section all lengths are non-negative: $d_{ij} \ge 0$ for every arc. Then every cycle has length $\ge 0$, and (A2) holds.

- The nodes are <strong>permanent</strong>, when their label is final, or <strong>temporary</strong>. At every iteration the temporary node with the smallest label becomes permanent.

!!! algoritmo "Algorithm: Dijkstra's algorithm"

    <div class="pseudocodice" markdown="0"><div class="pc" style="--liv:0"><strong>Input:</strong> a directed graph <span class="arithmatex">\(G=(N,A)\)</span> with lengths <span class="arithmatex">\(d_{ij} \ge 0\)</span>, a source <span class="arithmatex">\(s \in N\)</span></div><div class="pc" style="--liv:0"><strong>Output:</strong> the distances <span class="arithmatex">\(d(j)=\tilde{d}(j)\)</span> and the predecessors <span class="arithmatex">\(\mathit{pred}(j)\)</span></div><div class="pc" style="--liv:0"><span class="pc-n">1</span><strong>Step 0 (initialization).</strong> Set <span class="arithmatex">\(d(s):=0\)</span>, <span class="arithmatex">\(d(j):=+\infty\)</span> for <span class="arithmatex">\(j \neq s\)</span>; all nodes are temporary.</div><div class="pc" style="--liv:0"><span class="pc-n">2</span><strong>Step 1 (selection).</strong> If no temporary node has a finite label, <code>STOP</code>.</div><div class="pc" style="--liv:0"><span class="pc-n">3</span>  Otherwise make permanent the temporary node <span class="arithmatex">\(i\)</span> with the smallest <span class="arithmatex">\(d(i)\)</span> (the smallest index, if more than
    one).</div><div class="pc" style="--liv:0"><span class="pc-n">4</span><strong>Step 2 (update).</strong> For each arc <span class="arithmatex">\((i,j) \in \delta^+(i)\)</span> with <span class="arithmatex">\(j\)</span> temporary: if <span class="arithmatex">\(d(i)+d_{ij}<d(j)\)</span>, set
    <span class="arithmatex">\(d(j):=d(i)+d_{ij}\)</span> and <span class="arithmatex">\(\mathit{pred}(j):=i\)</span>.</div><div class="pc" style="--liv:0"><span class="pc-n">5</span>  Go to Step 1.</div></div>

<a id="box-30-sp-th-dijkstra"></a>

!!! teorema "Theorem 3.22: correctness of Dijkstra's algorithm"

    If $d_{ij} \ge 0$ for every arc, at every iteration of Dijkstra's algorithm:

    - **(a)** every permanent node $i$ has $d(i)=\tilde{d}(i)$;

    - **(b)** every temporary node $j$ has as $d(j)$ the minimum length of a path from $s$ to $j$ whose nodes other than $j$ are all permanent ($+\infty$ if there is none).

    At the stop, $d(j)=\tilde{d}(j)$ for every $j \in N$.

??? dimostrazione "Proof"

    Both properties hold after Step 0, with no permanent node. Let $i$ be the node selected in Step 1.

    1. <em>$d(i)=\tilde{d}(i)$.</em> Let $P$ be any path from $s$ to $i$, and let $h$ be its first temporary node. The part of $P$ up to $h$ has length $\ge d(h)$ by (b), and the rest has length $\ge 0$, since $d \ge 0$. Hence $d(P) \ge d(h) \ge d(i)$, and by (b) the value $d(i)$ is the length of a path: $d(i)=\tilde{d}(i)$.

    2. <em>(b) after Step 2.</em> Let $j$ be temporary and $Q$ a path to $j$ whose other nodes are permanent, with $h$ the node before $j$. If $h=i$, then $d(Q) \ge \tilde{d}(i)+d_{ij}=d(i)+d_{ij}$, the value tested in Step 2.

    3. If $h \neq i$, then $h$ became permanent before $i$, through a path of permanent nodes of length $\tilde{d}(h)$; when $h$ was selected, Step 2 gave $d(j) \le \tilde{d}(h)+d_{hj} \le d(Q)$.

    Hence the new minimum is $\min\{d(j),\,d(i)+d_{ij}\}$, attained by a path, which is the label left by Step 2. At the stop, the temporary nodes have $d(j)=+\infty$: by (b) no arc leaves the permanent set towards them, so they are not reachable and $\tilde{d}(j)=+\infty$. <span class="qed">□</span>

- For the $s$–$t$ problem the algorithm can stop as soon as $t$ is permanent, by (a).

- The arcs $(\mathit{pred}(j),j)$ form a shortest path tree: $\mathit{pred}(j)$ is permanent before $j$, and when it is last set $d(j)=d(\mathit{pred}(j))+d_{\mathit{pred}(j)\,j}$ with both labels final.

<a id="box-31-sp-th-dijkstra-time"></a>

!!! teorema "Theorem 3.23: running time of Dijkstra's algorithm"

    With the labels in an array, Dijkstra's algorithm runs in $O(n^2)$ time.

??? dimostrazione "Proof"

    There are at most $n$ iterations, and Step 1 scans the temporary labels in $O(n)$ time. Step 2 scans the forward star of the selected node, and each node is selected once, so all the updates take $O(m)$ time. The total is $O(n^2+m)=O(n^2)$, since $m \le n(n-1)$. <span class="qed">□</span>

- With the temporary labels in a binary heap, Step 1 and each decrease of a label take $O(\log n)$ time: the total is $O((n+m)\log n)$, better than $O(n^2)$ on sparse graphs.

### 3.6.1 Dijkstra's algorithm on the reference graph

<a id="box-32-sp-ex-dijkstra"></a>

!!! esempio "Example 3.9: Dijkstra from node $1$"

    We run the algorithm with the lengths of <span style="color:#1971c2">[Example 3.1](shortest-path-problems.md#box-2-sp-ex-ref)</span>. Each row is an iteration: the selected node becomes permanent (bold label), and a label that decreased has the new predecessor in brackets.

    <div class="tabella" markdown="0"><table>
    <tr>
    <th>iteration</th>
    <th>selected <span class="arithmatex">\(i\)</span></th>
    <th><span class="arithmatex">\(d(1)\)</span></th>
    <th><span class="arithmatex">\(d(2)\)</span></th>
    <th><span class="arithmatex">\(d(3)\)</span></th>
    <th><span class="arithmatex">\(d(4)\)</span></th>
    <th><span class="arithmatex">\(d(5)\)</span></th>
    <th><span class="arithmatex">\(d(6)\)</span></th>
    </tr>
    <tr>
    <td><span class="arithmatex">\(1\)</span></td>
    <td><span class="arithmatex">\(1\)</span></td>
    <td><span class="arithmatex">\(\mathbf{0}\)</span></td>
    <td><span class="arithmatex">\(7\)</span> (<span class="arithmatex">\(1\)</span>)</td>
    <td><span class="arithmatex">\(2\)</span> (<span class="arithmatex">\(1\)</span>)</td>
    <td><span class="arithmatex">\(\infty\)</span></td>
    <td><span class="arithmatex">\(\infty\)</span></td>
    <td><span class="arithmatex">\(\infty\)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">\(2\)</span></td>
    <td><span class="arithmatex">\(3\)</span></td>
    <td><span class="arithmatex">\(\mathbf{0}\)</span></td>
    <td><span class="arithmatex">\(5\)</span> (<span class="arithmatex">\(3\)</span>)</td>
    <td><span class="arithmatex">\(\mathbf{2}\)</span></td>
    <td><span class="arithmatex">\(\infty\)</span></td>
    <td><span class="arithmatex">\(10\)</span> (<span class="arithmatex">\(3\)</span>)</td>
    <td><span class="arithmatex">\(\infty\)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">\(3\)</span></td>
    <td><span class="arithmatex">\(2\)</span></td>
    <td><span class="arithmatex">\(\mathbf{0}\)</span></td>
    <td><span class="arithmatex">\(\mathbf{5}\)</span></td>
    <td><span class="arithmatex">\(\mathbf{2}\)</span></td>
    <td><span class="arithmatex">\(8\)</span> (<span class="arithmatex">\(2\)</span>)</td>
    <td><span class="arithmatex">\(10\)</span></td>
    <td><span class="arithmatex">\(\infty\)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">\(4\)</span></td>
    <td><span class="arithmatex">\(4\)</span></td>
    <td><span class="arithmatex">\(\mathbf{0}\)</span></td>
    <td><span class="arithmatex">\(\mathbf{5}\)</span></td>
    <td><span class="arithmatex">\(\mathbf{2}\)</span></td>
    <td><span class="arithmatex">\(\mathbf{8}\)</span></td>
    <td><span class="arithmatex">\(10\)</span></td>
    <td><span class="arithmatex">\(13\)</span> (<span class="arithmatex">\(4\)</span>)</td>
    </tr>
    <tr>
    <td><span class="arithmatex">\(5\)</span></td>
    <td><span class="arithmatex">\(5\)</span></td>
    <td><span class="arithmatex">\(\mathbf{0}\)</span></td>
    <td><span class="arithmatex">\(\mathbf{5}\)</span></td>
    <td><span class="arithmatex">\(\mathbf{2}\)</span></td>
    <td><span class="arithmatex">\(\mathbf{8}\)</span></td>
    <td><span class="arithmatex">\(\mathbf{10}\)</span></td>
    <td><span class="arithmatex">\(13\)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">\(6\)</span></td>
    <td><span class="arithmatex">\(6\)</span></td>
    <td><span class="arithmatex">\(\mathbf{0}\)</span></td>
    <td><span class="arithmatex">\(\mathbf{5}\)</span></td>
    <td><span class="arithmatex">\(\mathbf{2}\)</span></td>
    <td><span class="arithmatex">\(\mathbf{8}\)</span></td>
    <td><span class="arithmatex">\(\mathbf{10}\)</span></td>
    <td><span class="arithmatex">\(\mathbf{13}\)</span></td>
    </tr>
    </table></div>

    - In iteration $2$ the label of node $2$ drops from $7$ to $2+3=5$; in iteration $5$ the arc $(5,6)$ offers $10+7=17>13$, and the arc $(5,4)$ ends in a permanent node.

    - The nodes become permanent in the order $1,3,2,4,5,6$, with $\tilde{d}=(0,5,2,8,10,13)$; the predecessors give the shortest path tree of <span style="color:#1971c2">[Example 3.3](shortest-path-problems.md#box-9-sp-ex-bellman)</span>.

### 3.6.2 Negative lengths

<a id="box-33-sp-ex-counter"></a>

!!! esempio "Example 3.10: a negative arc breaks Dijkstra's algorithm"

    In the graph below, with $s=1$, the algorithm makes node $2$ permanent with $d(2)=2$, then node $3$ with $d(3)=3$; the arc $(3,2)$ ends in a permanent node and is ignored. The path $1,3,2$ has length $3-2=1<2$.

    ![Figure 6](../../img/shortest-paths/fig06.svg){ .fig loading=lazy  }

    On the reference graph with the lengths $d'$ of <span style="color:#1971c2">[Example 3.7](the-bellman-ford-algorithm.md#box-28-sp-ex-bf)</span> ($d'_{54}=-3$), Dijkstra's algorithm makes the nodes permanent in the order $1,3,2,4,5,6$ and returns $d(4)=8$ and $d(6)=13$: node $4$ is permanent before node $5$, so the shorter path $1,3,5,4$ of length $7$ is missed, and with it the path to $6$ of length $12$.

- The proof of <span style="color:#1971c2">[Theorem 3.22](#box-30-sp-th-dijkstra)</span> uses $d \ge 0$ in one point: the rest of $P$ after its first temporary node has length $\ge 0$. A negative arc breaks exactly this step.

!!! chiave ""

    With non-negative lengths, Dijkstra's algorithm makes permanent, at every iteration, the temporary node with the smallest label, whose label is then final; it runs in $O(n^2)$ time. With a negative arc it can fail, and the Bellman–Ford algorithm is used instead.

## 3.7 Typical mistakes

!!! attenzione "Warning"

    - <strong>Running Dijkstra's algorithm with a negative arc.</strong> Its labels can be wrong, as with $d'_{54}=-3$ on the reference graph; use Bellman–Ford, or the topological order if the graph is acyclic.

    - <strong>Adding a constant to every length.</strong> It makes the lengths non-negative but changes the shortest paths: a path with $k$ arcs grows by $k$ times the constant.

    - <strong>Swapping the sign of the potentials.</strong> With $+1$ in the tail of $\mat{B}$ the dual constraints are $\pi_i-\pi_j \le d_{ij}$ and the optimal potentials are $\pi_i=-\tilde{d}(i)$.

    - <strong>Skipping the test of pass $n$.</strong> After $n-1$ passes the labels are the distances only without negative cycles; a change in pass $n$ reveals one.

    - <strong>Expecting Bellman–Ford to see every negative cycle.</strong> It detects only the cycles reachable from $s$, while a negative cycle anywhere in $G$ makes the LP model unbounded.

    - <strong>Updating a permanent node in Dijkstra's algorithm.</strong> Its label is final; only temporary nodes are updated.

    - <strong>Looking for a topological order in a graph with cycles.</strong> It exists only in acyclic graphs: the reference graph has none.

## 3.8 In summary

!!! chiave "In summary"

    - The distance $\tilde{d}(j)$ is the length of a shortest path from $s$ to $j$; it is well defined when no negative cycle is reachable from $s$ (A2).

    - Subpaths of shortest paths are shortest; the distances satisfy Bellman's equations, and a shortest path tree exists.

    - Feasible potentials, $\bar{c}_{ij}=d_{ij}-\pi_i+\pi_j \ge 0$, and a path of tight arcs certify optimality.

    - The LP model is a unit flow, $\mat{B}\vet{x}=\vet{b}$, $\vet{x} \ge \vet{0}$; its dual is $\max\{\pi_s-\pi_t : \pi_i-\pi_j \le d_{ij}\}$, optimal at $\pi_i=-\tilde{d}(i)$.

    - Acyclic graphs: topological order, $O(n+m)$, any lengths. Bellman–Ford: $O(n\,m)$, any lengths, detects negative cycles. Dijkstra: $O(n^2)$, non-negative lengths.

    <strong>The reference graph at a glance.</strong>

    <div class="tabella" markdown="0"><table>
    <tr>
    <td>lengths <span class="arithmatex">\(d\)</span> (Dijkstra)</td>
    <td><span class="arithmatex">\(\tilde{d}=(0,5,2,8,10,13)\)</span>, order <span class="arithmatex">\(1,3,2,4,5,6\)</span></td>
    </tr>
    <tr>
    <td>LP models</td>
    <td><span class="arithmatex">\(z(\mathrm{SP}(1,6))=13\)</span>, <span class="arithmatex">\(z(\mathrm{SP}(1))=38\)</span></td>
    </tr>
    <tr>
    <td>lengths <span class="arithmatex">\(d'\)</span>, <span class="arithmatex">\(d'_{54}=-3\)</span> (Bellman–Ford)</td>
    <td><span class="arithmatex">\(\tilde{d}=(0,5,2,7,10,12)\)</span>, <span class="arithmatex">\(5\)</span> passes</td>
    </tr>
    <tr>
    <td>lengths <span class="arithmatex">\(d''\)</span>, <span class="arithmatex">\(d''_{54}=-10\)</span></td>
    <td>negative cycle <span class="arithmatex">\(3,5,4,3\)</span> of length <span class="arithmatex">\(-1\)</span></td>
    </tr>
    <tr>
    <td>acyclic graph, arc <span class="arithmatex">\((3,4)\)</span></td>
    <td>order <span class="arithmatex">\(1,3,2,5,4,6\)</span>; <span class="arithmatex">\(\tilde{d}=(0,5,2,3,10,8)\)</span></td>
    </tr>
    </table></div>

---

**Exercises on this chapter:** [:material-pencil: Shortest paths](../../exercises/shortest-paths.md)


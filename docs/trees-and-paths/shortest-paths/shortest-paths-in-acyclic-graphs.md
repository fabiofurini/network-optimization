---
title: "Shortest paths in acyclic graphs"
---

# 3.4 Shortest paths in acyclic graphs { #sez-sec-sp-dag }

<div class="info-capitolo" markdown>

**Part 2 · Trees and paths · Chapter 3** · [:material-book-open-variant: Chapter 3: Shortest paths](index.md) · [:material-file-pdf-box: Lecture notes, volume 2 (PDF)](../../pdf/lecture-notes-2-trees-and-paths.pdf) · [:material-pencil: Exercises: Shortest paths](../../exercises/shortest-paths.md) · [:material-gesture-tap: App: Shortest paths: Dijkstra, Bellman–Ford, acyclic graphs](../../lab/shortest-paths-dijkstra-bellman-ford.md)

</div>

<a id="box-18-sp-def-topo"></a>

!!! definizione "Definition 3.13: acyclic graph and topological order"

    A directed graph without directed cycles is a <strong>directed acyclic graph</strong> (DAG). A <strong>topological order</strong> of $G=(N,A)$ is an ordering $v_1,v_2,\dots,v_n$ of its nodes such that every arc goes forward:

    $$
    (v_a,v_b) \in A \quad \Longrightarrow \quad a<b .
    $$

<a id="box-19-sp-prop-topo"></a>

!!! teorema "Proposition 3.14: topological orders"

    A directed graph has a topological order if and only if it is acyclic.

??? dimostrazione "Proof"

    If $G$ has a topological order, a cycle $i_0,i_1,\dots,i_k=i_0$ would go forward on every arc and come back to its first node: impossible. Conversely, let $G$ be acyclic; we argue by induction on $n$.

    1. $G$ has a node with no entering arc: otherwise, walking backwards along entering arcs from any node, after $n$ steps a node repeats, and the walk contains a cycle.

    2. Put such a node $v_1$ first. The graph without $v_1$ is acyclic, and by induction it has a topological order $v_2,\dots,v_n$; no arc enters $v_1$, so $v_1,v_2,\dots,v_n$ is a topological order of $G$. <span class="qed">□</span>

!!! algoritmo "Algorithm: Shortest paths in an acyclic graph"

    <div class="pseudocodice" markdown="0"><div class="pc" style="--liv:0"><strong>Input:</strong> an acyclic graph <span class="arithmatex">\(G=(N,A)\)</span> with lengths <span class="arithmatex">\(d_{ij}\)</span> of any sign, a source <span class="arithmatex">\(s \in N\)</span></div><div class="pc" style="--liv:0"><strong>Output:</strong> the distances <span class="arithmatex">\(d(j)=\tilde{d}(j)\)</span> and the predecessors <span class="arithmatex">\(\mathit{pred}(j)\)</span></div><div class="pc" style="--liv:0"><span class="pc-n">1</span><strong>Step 0 (order).</strong> Find a topological order: repeatedly remove a node without entering arcs (the smallest
    index, if more than one).</div><div class="pc" style="--liv:0"><span class="pc-n">2</span>  Set <span class="arithmatex">\(d(s):=0\)</span> and <span class="arithmatex">\(d(j):=+\infty\)</span> for <span class="arithmatex">\(j \neq s\)</span>.</div><div class="pc" style="--liv:0"><span class="pc-n">3</span><strong>Step 1 (labels).</strong> For each node <span class="arithmatex">\(i\)</span> in topological order with <span class="arithmatex">\(d(i)<+\infty\)</span>, and each arc <span class="arithmatex">\((i,j) \in \delta^+(i)\)</span>:</div><div class="pc" style="--liv:0"><span class="pc-n">4</span>  if <span class="arithmatex">\(d(i)+d_{ij}<d(j)\)</span>, set <span class="arithmatex">\(d(j):=d(i)+d_{ij}\)</span> and <span class="arithmatex">\(\mathit{pred}(j):=i\)</span>.</div><div class="pc" style="--liv:0"><span class="pc-n">5</span>  <code>STOP</code>.</div></div>

<a id="box-20-sp-th-dag"></a>

!!! teorema "Theorem 3.15: correctness and running time on acyclic graphs"

    On an acyclic graph with lengths of any sign, the algorithm «Shortest paths in an acyclic graph» ends with $d(j)=\tilde{d}(j)$ for every $j \in N$, and it runs in $O(n+m)$ time.

??? dimostrazione "Proof"

    An acyclic graph has no cycle at all, so (A2) holds. Every finite label is the length of a walk from $s$, so $d(j) \ge \tilde{d}(j)$ by <span style="color:#1971c2">[Lemma 3.3](shortest-path-problems.md#box-4-sp-lem-walk)</span>; labels only decrease.

    1. Let $j$ be reachable and $s=i_0,i_1,\dots,i_k=j$ a shortest path; its nodes appear in this order in the topological order, since every arc goes forward.

    2. By induction on $t$, after $i_t$ is processed $d(i_t) \le \tilde{d}(i_t)$: the path to $i_{t-1}$ is shortest (<span style="color:#1971c2">[Lemma 3.4](shortest-path-problems.md#box-6-sp-lem-subpath)</span>), and processing $i_{t-1}$ gives $d(i_t) \le \tilde{d}(i_{t-1})+d_{i_{t-1}i_t}=\tilde{d}(i_t)$.

    3. Nodes not reachable from $s$ keep $d(j)=+\infty=\tilde{d}(j)$.

    <em>Time.</em> The topological order takes $O(n+m)$ time with a counter of the entering arcs of every node, decreased when a tail is removed; Step 1 scans every arc once. <span class="qed">□</span>

- The smallest-index rule fixes one order for the examples; any node without entering arcs can be removed.

- With the lengths $-d_{ij}$ the algorithm computes <strong>longest paths</strong>, since an acyclic graph has no cycle to repeat. Longest paths in acyclic graphs are the core of [Chapter 9 «Project management»](https://fabiofurini.github.io/network-optimization/project-management/project-management/).

<a id="box-21-sp-ex-dag"></a>

!!! esempio "Example 3.6: an acyclic instance"

    Reversing the arc $(4,3)$ of the reference graph into $(3,4)$, with $d_{34}=1$, gives an acyclic graph. We give it the lengths of <span style="color:#1971c2">[Example 3.1](shortest-path-problems.md#box-2-sp-ex-ref)</span> except $d_{54}=-3$ (red).

    ![Figure 3](../../img/shortest-paths/fig03.svg){ .fig loading=lazy  }

    Step 0 gives the topological order $1,3,2,5,4,6$: after $1$, only $3$ has no entering arc; then $2$ and $5$ are free, and $2$ goes first. Each row of the table processes one node and shows the labels after it:

    <div class="tabella" markdown="0"><table>
    <tr>
    <th>step</th>
    <th>node <span class="arithmatex">\(i\)</span></th>
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
    <td><span class="arithmatex">\(0\)</span></td>
    <td><span class="arithmatex">\(7\)</span></td>
    <td><span class="arithmatex">\(2\)</span></td>
    <td><span class="arithmatex">\(\infty\)</span></td>
    <td><span class="arithmatex">\(\infty\)</span></td>
    <td><span class="arithmatex">\(\infty\)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">\(2\)</span></td>
    <td><span class="arithmatex">\(3\)</span></td>
    <td><span class="arithmatex">\(0\)</span></td>
    <td><span class="arithmatex">\(5\)</span></td>
    <td><span class="arithmatex">\(2\)</span></td>
    <td><span class="arithmatex">\(3\)</span></td>
    <td><span class="arithmatex">\(10\)</span></td>
    <td><span class="arithmatex">\(\infty\)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">\(3\)</span></td>
    <td><span class="arithmatex">\(2\)</span></td>
    <td><span class="arithmatex">\(0\)</span></td>
    <td><span class="arithmatex">\(5\)</span></td>
    <td><span class="arithmatex">\(2\)</span></td>
    <td><span class="arithmatex">\(3\)</span></td>
    <td><span class="arithmatex">\(10\)</span></td>
    <td><span class="arithmatex">\(\infty\)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">\(4\)</span></td>
    <td><span class="arithmatex">\(5\)</span></td>
    <td><span class="arithmatex">\(0\)</span></td>
    <td><span class="arithmatex">\(5\)</span></td>
    <td><span class="arithmatex">\(2\)</span></td>
    <td><span class="arithmatex">\(3\)</span></td>
    <td><span class="arithmatex">\(10\)</span></td>
    <td><span class="arithmatex">\(17\)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">\(5\)</span></td>
    <td><span class="arithmatex">\(4\)</span></td>
    <td><span class="arithmatex">\(0\)</span></td>
    <td><span class="arithmatex">\(5\)</span></td>
    <td><span class="arithmatex">\(2\)</span></td>
    <td><span class="arithmatex">\(3\)</span></td>
    <td><span class="arithmatex">\(10\)</span></td>
    <td><span class="arithmatex">\(8\)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">\(6\)</span></td>
    <td><span class="arithmatex">\(6\)</span></td>
    <td><span class="arithmatex">\(0\)</span></td>
    <td><span class="arithmatex">\(5\)</span></td>
    <td><span class="arithmatex">\(2\)</span></td>
    <td><span class="arithmatex">\(3\)</span></td>
    <td><span class="arithmatex">\(10\)</span></td>
    <td><span class="arithmatex">\(8\)</span></td>
    </tr>
    </table></div>

    The predecessors give the tree $(1,3)$, $(3,2)$, $(3,4)$, $(3,5)$, $(4,6)$ (blue). The negative arc $(5,4)$ is not used: $d(5)-3=7>3=d(4)$. With the lengths $-d_{ij}$ the longest path lengths from $1$ are $(0,7,2,10,10,17)$.

!!! chiave ""

    A graph is acyclic if and only if it has a topological order. Scanning the nodes in that order, each label is final when its node is processed: shortest paths in $O(n+m)$ time, with lengths of any sign.

---

**Next:** [3.5 The Bellman–Ford algorithm](the-bellman-ford-algorithm.md)

---
title: "Kruskal's algorithm"
---

# 2.5 Kruskal's algorithm { #sez-sec-mst-kruskal }

<div class="info-capitolo" markdown>

**Part 2 · Trees and paths · Chapter 2** · [:material-book-open-variant: Chapter 2: Spanning trees](index.md) · [:material-file-pdf-box: Lecture notes, volume 2 (PDF)](../../pdf/lecture-notes-2-trees-and-paths.pdf) · [:material-pencil: Exercises: Spanning trees](../../exercises/minimum-spanning-trees.md) · [:material-gesture-tap: App: Minimum spanning trees: Kruskal and Prim](../../lab/minimum-spanning-tree-kruskal-prim.md)

</div>

!!! algoritmo "Algorithm: Kruskal's algorithm"

    <div class="pseudocodice" markdown="0"><div class="pc" style="--liv:0"><strong>Input:</strong> a connected undirected graph <span class="arithmatex">\(G=(V,E)\)</span> with weights <span class="arithmatex">\(w_e\)</span></div><div class="pc" style="--liv:0"><strong>Output:</strong> a minimum spanning tree <span class="arithmatex">\(F\)</span></div><div class="pc" style="--liv:0"><span class="pc-n">1</span><strong>Step 0 (initialization).</strong> Sort the edges by non-decreasing weight, <span class="arithmatex">\(w_{e_1} \le w_{e_2} \le \dots \le w_{e_m}\)</span>, and set <span class="arithmatex">\(F:=\emptyset\)</span>.</div><div class="pc" style="--liv:0"><span class="pc-n">2</span><strong>Step 1 (scan).</strong> For <span class="arithmatex">\(k=1,2,\dots,m\)</span>: if the endpoints of <span class="arithmatex">\(e_k\)</span> are in different components of <span class="arithmatex">\((V,F)\)</span>, set
    <span class="arithmatex">\(F:=F \cup \{e_k\}\)</span>; otherwise reject <span class="arithmatex">\(e_k\)</span>.</div><div class="pc" style="--liv:0"><span class="pc-n">3</span>  If <span class="arithmatex">\(|F|=n-1\)</span>, <code>STOP</code>.</div></div>

- An edge is <strong>accepted</strong> if it joins two different components of $(V,F)$, and <strong>rejected</strong> if it would close a cycle. The components of $(V,F)$ start as the $n$ single vertices and merge at every acceptance.

- In this module, edges of equal weight are scanned in lexicographic order of $\{u,v\}$, with $u<v$.

<a id="box-16-mst-th-kruskal"></a>

!!! teorema "Theorem 2.10: correctness of Kruskal's algorithm"

    Kruskal's algorithm stops with $|F|=n-1$, and $F$ is a minimum spanning tree.

??? dimostrazione "Proof"

    We show that every accepted edge $e_k=\{u,v\}$ is a choice of Step 2 of the generic greedy algorithm. Let $S$ be the component of $(V,F)$ that contains $u$, just before $e_k$ is accepted: $v \notin S$, and no edge of $F$ crosses $\delta(S)$.

    1. Let $e_h \in \delta(S)$ with $h<k$. When $e_h$ was scanned it was not accepted, since $F \cap \delta(S)=\emptyset$; so its endpoints were in the same component then, and they still are, because components only merge. This contradicts $e_h \in \delta(S)$.

    2. Hence every edge of $\delta(S)$ is some $e_h$ with $h \ge k$, and $w_{e_h} \ge w_{e_k}$: $e_k$ has minimum weight in $\delta(S)$.

    3. If the scan ended with $|F|<n-1$, the forest $(V,F)$ would have two components joined by an edge of $G$, and that edge would have been accepted when scanned, by the argument of point 1.

    By <span style="color:#1971c2">[Theorem 2.9](the-generic-greedy-algorithm.md#box-15-mst-th-greedy)</span>, $F$ is a minimum spanning tree. <span class="qed">□</span>

## 2.5.1 Implementation and running time

- The components of $(V,F)$ are kept in a <strong>union–find</strong> structure: every vertex $v$ stores the label $\mathit{comp}(v)$ of its component, and every component stores the list of its vertices and its size.

- Testing whether $u$ and $v$ are in different components is the comparison $\mathit{comp}(u) \neq \mathit{comp}(v)$, in $O(1)$ time. Merging two components relabels the vertices of the <em>smaller</em> one (<strong>union by size</strong>).

<a id="box-17-mst-th-kruskal-time"></a>

!!! teorema "Theorem 2.11: running time of Kruskal's algorithm"

    With the union–find structure by labels and union by size, Kruskal's algorithm runs in $O(m\log n)$ time.

??? dimostrazione "Proof"

    1. Sorting the edges takes $O(m\log m)$ time; since $m \le n^2$, $\log m \le 2\log n$ and this is $O(m\log n)$.

    2. The scan performs $m$ tests, each in $O(1)$ time.

    3. When a vertex is relabelled, its component merges with one at least as large, so the size of its component at least doubles. The size never exceeds $n$, so each vertex is relabelled at most $\log_2 n$ times: all the merges take $O(n\log n)$ time.

    $G$ is connected, so $n-1 \le m$, and the total is $O(m\log n+n\log n)=O(m\log n)$. <span class="qed">□</span>

- The running time is dominated by the sorting. With the union–find structure by trees, with union by rank and path compression, the scan takes almost linear time; the bound stays $O(m\log n)$ because of the sorting.

- The algorithm uses only comparisons between weights: any increasing transformation of the weights gives the same tree.

## 2.5.2 Kruskal's algorithm on the reference graph

<a id="box-18-mst-ex-kruskal"></a>

!!! esempio "Example 2.7: Kruskal's algorithm"

    We run Kruskal's algorithm on the weighted reference graph. The edges in order of weight are $\{1,3\},\{4,5\},\{2,3\},\{1,2\},\{3,4\},\{2,4\},\{5,6\},\{3,5\},\{4,6\}$. Each row is one scanned edge, with the components of $(V,F)$ after the step:

    <div class="tabella" markdown="0"><table>
    <tr>
    <th><span class="arithmatex">\(k\)</span></th>
    <th>edge <span class="arithmatex">\(e_k\)</span></th>
    <th><span class="arithmatex">\(w_{e_k}\)</span></th>
    <th>decision and components of <span class="arithmatex">\((V,F)\)</span></th>
    </tr>
    <tr>
    <td><span class="arithmatex">\(1\)</span></td>
    <td><span class="arithmatex">\(\{1,3\}\)</span></td>
    <td><span class="arithmatex">\(1\)</span></td>
    <td>accept: <span class="arithmatex">\(\{1,3\},\{2\},\{4\},\{5\},\{6\}\)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">\(2\)</span></td>
    <td><span class="arithmatex">\(\{4,5\}\)</span></td>
    <td><span class="arithmatex">\(2\)</span></td>
    <td>accept: <span class="arithmatex">\(\{1,3\},\{2\},\{4,5\},\{6\}\)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">\(3\)</span></td>
    <td><span class="arithmatex">\(\{2,3\}\)</span></td>
    <td><span class="arithmatex">\(3\)</span></td>
    <td>accept: <span class="arithmatex">\(\{1,2,3\},\{4,5\},\{6\}\)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">\(4\)</span></td>
    <td><span class="arithmatex">\(\{1,2\}\)</span></td>
    <td><span class="arithmatex">\(4\)</span></td>
    <td>reject (<span class="arithmatex">\(1\)</span> and <span class="arithmatex">\(2\)</span> are both in <span class="arithmatex">\(\{1,2,3\}\)</span>)</td>
    </tr>
    <tr>
    <td><span class="arithmatex">\(5\)</span></td>
    <td><span class="arithmatex">\(\{3,4\}\)</span></td>
    <td><span class="arithmatex">\(5\)</span></td>
    <td>accept: <span class="arithmatex">\(\{1,2,3,4,5\},\{6\}\)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">\(6\)</span></td>
    <td><span class="arithmatex">\(\{2,4\}\)</span></td>
    <td><span class="arithmatex">\(6\)</span></td>
    <td>reject (<span class="arithmatex">\(2\)</span> and <span class="arithmatex">\(4\)</span> are both in <span class="arithmatex">\(\{1,2,3,4,5\}\)</span>)</td>
    </tr>
    <tr>
    <td><span class="arithmatex">\(7\)</span></td>
    <td><span class="arithmatex">\(\{5,6\}\)</span></td>
    <td><span class="arithmatex">\(7\)</span></td>
    <td>accept: <span class="arithmatex">\(\{1,2,3,4,5,6\}\)</span>; <span class="arithmatex">\(|F|=5\)</span>, <code>STOP</code></td>
    </tr>
    </table></div>

    The algorithm stops after $7$ of the $9$ edges, with $F=\{\{1,3\},\{4,5\},\{2,3\},\{3,4\},\{5,6\}\}$ of weight $18$: the tree $\tilde{F}$ of <span style="color:#1971c2">[Example 2.2](the-minimum-spanning-tree-problem.md#box-3-mst-ex-opt)</span>. The figure shows, on each tree edge, its weight and in brackets the step $k$ of its acceptance.

    ![Figure 4](../../img/minimum-spanning-trees/fig04.svg){ .fig loading=lazy  }

- The rejected edges $\{1,2\}$ and $\{2,4\}$ are the heaviest edges of the cycles $1,2,3$ and $2,3,4$, as the cycle property predicts; the edges $\{3,5\}$ and $\{4,6\}$ are never scanned.

!!! chiave ""

    Kruskal's algorithm scans the edges by non-decreasing weight and accepts those that join two components; with union–find it runs in $O(m\log n)$ time, dominated by the sorting.

---

**Next:** [2.6 Prim's algorithm](prim-s-algorithm.md)

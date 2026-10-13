---
title: "Prim's algorithm"
---

# 2.6 Prim's algorithm { #sez-sec-mst-prim }

<div class="info-capitolo" markdown>

**Part 2 · Trees and paths · Chapter 2** · [:material-book-open-variant: Chapter 2: Spanning trees](index.md) · [:material-file-pdf-box: Lecture notes, volume 2 (PDF)](../../pdf/lecture-notes-2-trees-and-paths.pdf) · [:material-pencil: Exercises: Spanning trees](../../exercises/minimum-spanning-trees.md) · [:material-gesture-tap: App: Minimum spanning trees: Kruskal and Prim](../../lab/minimum-spanning-tree-kruskal-prim.md)

</div>

- Prim's algorithm grows a single tree from a start vertex $s$: the set $S$ of the vertices of the tree defines the cut $\delta(S)$ of Step 2, and the lightest edge of the cut is found through a <strong>label</strong> $d(v)$ for every vertex $v \notin S$.

!!! algoritmo "Algorithm: Prim's algorithm"

    <div class="pseudocodice" markdown="0"><div class="pc" style="--liv:0"><strong>Input:</strong> a connected undirected graph <span class="arithmatex">\(G=(V,E)\)</span> with weights <span class="arithmatex">\(w_e\)</span>, given by its adjacency lists; a start vertex
    <span class="arithmatex">\(s \in V\)</span></div><div class="pc" style="--liv:0"><strong>Output:</strong> a minimum spanning tree <span class="arithmatex">\(F\)</span></div><div class="pc" style="--liv:0"><span class="pc-n">1</span><strong>Step 0 (initialization).</strong> Set <span class="arithmatex">\(S:=\{s\}\)</span> and <span class="arithmatex">\(F:=\emptyset\)</span>. For every <span class="arithmatex">\(v \neq s\)</span>: if <span class="arithmatex">\(\{s,v\} \in E\)</span>, set
    <span class="arithmatex">\(d(v):=w_{sv}\)</span> and <span class="arithmatex">\(\mathit{pred}(v):=s\)</span>; otherwise set <span class="arithmatex">\(d(v):=+\infty\)</span>.</div><div class="pc" style="--liv:0"><span class="pc-n">2</span><strong>Step 1 (selection).</strong> If <span class="arithmatex">\(S=V\)</span>, <code>STOP</code>. Otherwise select <span class="arithmatex">\(v \notin S\)</span> with minimum <span class="arithmatex">\(d(v)\)</span>, and set
    <span class="arithmatex">\(S:=S \cup \{v\}\)</span>, <span class="arithmatex">\(F:=F \cup \{\{\mathit{pred}(v),v\}\}\)</span>.</div><div class="pc" style="--liv:0"><span class="pc-n">3</span><strong>Step 2 (update).</strong> For every <span class="arithmatex">\(u \notin S\)</span> adjacent to <span class="arithmatex">\(v\)</span> with <span class="arithmatex">\(w_{vu}<d(u)\)</span>, set <span class="arithmatex">\(d(u):=w_{vu}\)</span> and
    <span class="arithmatex">\(\mathit{pred}(u):=v\)</span>. Go to Step 1.</div></div>

- In this module the start vertex is $s=1$, and ties in Step 1 are broken by the smallest index.

<a id="box-19-mst-lem-labels"></a>

!!! teorema "Lemma 2.12: meaning of the labels"

    At every execution of Step 1 of Prim's algorithm, for every $v \notin S$,

    $$
    d(v)=\min\big\{\, w_{uv} : u \in S,~ \{u,v\} \in E \,\big\}
    $$

    ($+\infty$ if $v$ has no neighbour in $S$), and when $d(v)<+\infty$ the minimum is attained by $u=\mathit{pred}(v)$.

??? dimostrazione "Proof"

    By induction. At the first execution $S=\{s\}$, and Step 0 sets exactly $d(v)=w_{sv}$, or $+\infty$. Assume the claim before the insertion of a vertex $v$ into $S$. For $u \notin S \cup \{v\}$, the new set $S \cup \{v\}$ adds the candidate $w_{vu}$ when $\{v,u\} \in E$, and Step 2 replaces $d(u)$ and $\mathit{pred}(u)$ exactly when this candidate is smaller. The other labels and predecessors are unchanged. <span class="qed">□</span>

<a id="box-20-mst-th-prim"></a>

!!! teorema "Theorem 2.13: correctness of Prim's algorithm"

    Prim's algorithm stops with $|F|=n-1$, and $F$ is a minimum spanning tree.

??? dimostrazione "Proof"

    All the edges of $F$ have both endpoints in $S$, so $F \cap \delta(S)=\emptyset$.

    1. By <span style="color:#1971c2">[Lemma 2.12](#box-19-mst-lem-labels)</span>, $\min_{v \notin S} d(v)$ is the minimum weight of an edge of $\delta(S)$, attained by $\{\mathit{pred}(v),v\}$ for the selected $v$; it is finite because $G$ is connected.

    2. Hence every iteration is a choice of Step 2 of the generic greedy algorithm, with the cut $\delta(S)$.

    3. Each iteration adds one vertex to $S$ and one edge to $F$, so the algorithm stops after $n-1$ iterations with $|F|=n-1$; <span style="color:#1971c2">[Theorem 2.9](the-generic-greedy-algorithm.md#box-15-mst-th-greedy)</span> concludes. <span class="qed">□</span>

<a id="box-21-mst-th-prim-time"></a>

!!! teorema "Theorem 2.14: running time of Prim's algorithm"

    With the labels stored in an array, Prim's algorithm runs in $O(n^2)$ time.

??? dimostrazione "Proof"

    There are $n-1$ selections, and each scans the labels of at most $n$ vertices: $O(n^2)$ in total. The update after the insertion of $v$ scans the adjacency list of $v$ in $O(\deg(v))$ time, and $\sum_{v \in V} \deg(v)=2m$. The total is $O(n^2+m)=O(n^2)$, since $m \le n^2$. <span class="qed">□</span>

- On dense graphs, with $m$ of the order of $n^2$, the bound $O(n^2)$ is linear in the size of the graph.

- With the labels in a binary heap, each selection and each update take $O(\log n)$ time, for $O(m\log n)$ in total: better on sparse graphs.

## 2.6.1 Prim's algorithm on the reference graph

<a id="box-22-mst-ex-prim"></a>

!!! esempio "Example 2.8: Prim's algorithm from vertex $1$"

    We run Prim's algorithm on the weighted reference graph from $s=1$. Each row shows the selected vertex, the edge added to $F$ and the labels $d(v)$ of the vertices outside $S$ after the update, with $\mathit{pred}(v)$ in brackets; a dash marks the vertices already in $S$.

    <div class="tabella" markdown="0"><table>
    <tr>
    <th>iteration</th>
    <th>selected</th>
    <th>added edge</th>
    <th><span class="arithmatex">\(d(2)\)</span></th>
    <th><span class="arithmatex">\(d(3)\)</span></th>
    <th><span class="arithmatex">\(d(4)\)</span></th>
    <th><span class="arithmatex">\(d(5)\)</span></th>
    <th><span class="arithmatex">\(d(6)\)</span></th>
    </tr>
    <tr>
    <td><span class="arithmatex">\(0\)</span></td>
    <td><span class="arithmatex">\(1\)</span></td>
    <td>–</td>
    <td><span class="arithmatex">\(4~(1)\)</span></td>
    <td><span class="arithmatex">\(1~(1)\)</span></td>
    <td><span class="arithmatex">\(\infty\)</span></td>
    <td><span class="arithmatex">\(\infty\)</span></td>
    <td><span class="arithmatex">\(\infty\)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">\(1\)</span></td>
    <td><span class="arithmatex">\(3\)</span></td>
    <td><span class="arithmatex">\(\{1,3\}\)</span></td>
    <td><span class="arithmatex">\(3~(3)\)</span></td>
    <td>–</td>
    <td><span class="arithmatex">\(5~(3)\)</span></td>
    <td><span class="arithmatex">\(8~(3)\)</span></td>
    <td><span class="arithmatex">\(\infty\)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">\(2\)</span></td>
    <td><span class="arithmatex">\(2\)</span></td>
    <td><span class="arithmatex">\(\{2,3\}\)</span></td>
    <td>–</td>
    <td>–</td>
    <td><span class="arithmatex">\(5~(3)\)</span></td>
    <td><span class="arithmatex">\(8~(3)\)</span></td>
    <td><span class="arithmatex">\(\infty\)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">\(3\)</span></td>
    <td><span class="arithmatex">\(4\)</span></td>
    <td><span class="arithmatex">\(\{3,4\}\)</span></td>
    <td>–</td>
    <td>–</td>
    <td>–</td>
    <td><span class="arithmatex">\(2~(4)\)</span></td>
    <td><span class="arithmatex">\(9~(4)\)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">\(4\)</span></td>
    <td><span class="arithmatex">\(5\)</span></td>
    <td><span class="arithmatex">\(\{4,5\}\)</span></td>
    <td>–</td>
    <td>–</td>
    <td>–</td>
    <td>–</td>
    <td><span class="arithmatex">\(7~(5)\)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">\(5\)</span></td>
    <td><span class="arithmatex">\(6\)</span></td>
    <td><span class="arithmatex">\(\{5,6\}\)</span></td>
    <td>–</td>
    <td>–</td>
    <td>–</td>
    <td>–</td>
    <td>–</td>
    </tr>
    </table></div>

    At iteration $1$ the label of $2$ drops from $4$ to $3$, because $w_{32}=3<4$; at iteration $3$ the label of $5$ drops from $8$ to $2$. The figure shows the state after iteration $2$: the cut $\delta(\{1,2,3\})$ is crossed by $\{2,4\}$, $\{3,4\}$, $\{3,5\}$, and the next edge is $\{3,4\}$, with $d(4)=5$.

    ![Figure 5](../../img/minimum-spanning-trees/fig05.svg){ .fig loading=lazy  }

    The final tree is $\{1,3\},\{2,3\},\{3,4\},\{4,5\},\{5,6\}$, of weight $18$: the same tree as Kruskal's algorithm, with the edges added in a different order.

- Kruskal's algorithm adds $\{4,5\}$ second, while Prim's algorithm adds it fourth: Kruskal grows a forest, Prim a single tree containing $s$.

!!! chiave ""

    Prim's algorithm grows one tree from $s$ and adds the lightest edge leaving it; the labels $d(v)$ give that edge in $O(n)$ time, for $O(n^2)$ in total.

---

**Next:** [2.7 Uniqueness of the minimum spanning tree](uniqueness-of-the-minimum-spanning-tree.md)

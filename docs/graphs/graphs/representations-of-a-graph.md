---
title: "Representations of a graph"
---

# 1.2 Representations of a graph { #sez-sec-gr-representations }

<div class="info-capitolo" markdown>

**Part 1 · Graphs · Chapter 1** · [:material-book-open-variant: Chapter 1: Graphs](index.md) · [:material-file-pdf-box: Lecture notes, volume 1 (PDF)](../../pdf/lecture-notes-1-graphs.pdf) · [:material-presentation: Slides](../../pdf/slides-graphs.pdf) · [:material-pencil: Exercises: Graphs](../../exercises/graphs.md) · [:material-gesture-tap: App: Graph search: BFS and DFS](../../lab/graph-search-bfs-dfs.md)

</div>

<a id="box-10-gr-def-adjmatrix"></a>

!!! definizione "Definition 1.7: adjacency matrix"

    The <strong>adjacency matrix</strong> of a directed graph $G=(N,A)$ is the $n \times n$ matrix $\mat{M}$ with entries

    $$
    m_{ij}=\begin{cases} 1 & \text{if } (i,j) \in A,\\ 0 & \text{otherwise,}\end{cases}
    \qquad \forall i,j \in \{1,2,\dots,n\}.
    $$

    The adjacency matrix of an undirected graph has $m_{uv}=m_{vu}=1$ for every edge $\{u,v\}$: it is symmetric.

<a id="box-11-gr-def-incidence"></a>

!!! definizione "Definition 1.8: node–arc incidence matrix"

    Let $G=(N,A)$ be a directed graph with arcs $a_1,a_2,\dots,a_m$. The <strong>node–arc incidence matrix</strong> is the $n \times m$ matrix $\mat{B}$ with one row per node and one column per arc, whose entries are

    $$
    b_{ik}=\begin{cases} +1 & \text{if } i \text{ is the tail of } a_k,\\ -1 & \text{if } i \text{ is the head of }
    a_k,\\ 0 & \text{otherwise,}\end{cases}
    \qquad \forall i \in \{1,2,\dots,n\},~ \forall k \in \{1,2,\dots,m\}.
    $$

- Every column of $\mat{B}$ has exactly one $+1$ (the tail) and one $-1$ (the head), so the sum of the rows of $\mat{B}$ is the zero vector.

- Row $i$ has a $+1$ for every arc of $\delta^+(i)$ and a $-1$ for every arc of $\delta^-(i)$: it has $\deg^+(i)+\deg^-(i)$ nonzero entries.

- The <strong>vertex–edge incidence matrix</strong> of an undirected graph has a $1$ in both endpoints of every edge.

<a id="box-12-gr-ex-matrices"></a>

!!! esempio "Example 1.4: the matrices of the reference graph"

    The adjacency matrix $\mat{M}$ and the node–arc incidence matrix $\mat{B}$ of the reference graph of <span style="color:#1971c2">[Example 1.2](undirected-and-directed-graphs.md#box-5-gr-ex-ref)</span> are shown with the index of each row (a node) and of each column (a node in $\mat{M}$, an arc in $\mat{B}$):

    $$
    \mat{M}:\quad
    \begin{array}{c|rrrrrr}
    & 1 & 2 & 3 & 4 & 5 & 6\\ \hline
    1 & 0 & 1 & 1 & 0 & 0 & 0\\
    2 & 0 & 0 & 0 & 1 & 0 & 0\\
    3 & 0 & 1 & 0 & 0 & 1 & 0\\
    4 & 0 & 0 & 1 & 0 & 0 & 1\\
    5 & 0 & 0 & 0 & 1 & 0 & 1\\
    6 & 0 & 0 & 0 & 0 & 0 & 0\\
    \end{array}
    $$

    $$
    \mat{B}:\quad
    \begin{array}{c|rrrrrrrrr}
    & a_1 & a_2 & a_3 & a_4 & a_5 & a_6 & a_7 & a_8 & a_9\\ \hline
    1 & 1 & 1 & 0 & 0 & 0 & 0 & 0 & 0 & 0\\
    2 & -1 & 0 & 1 & -1 & 0 & 0 & 0 & 0 & 0\\
    3 & 0 & -1 & 0 & 1 & 1 & -1 & 0 & 0 & 0\\
    4 & 0 & 0 & -1 & 0 & 0 & 1 & 1 & -1 & 0\\
    5 & 0 & 0 & 0 & 0 & -1 & 0 & 0 & 1 & 1\\
    6 & 0 & 0 & 0 & 0 & 0 & 0 & -1 & 0 & -1\\
    \end{array}
    $$

    For example, the column of $a_6=(4,3)$ has $+1$ in row $4$ (the tail) and $-1$ in row $3$ (the head). Row $6$ of $\mat{M}$ is zero, because node $6$ has no successors.

<a id="box-13-gr-def-lists"></a>

!!! definizione "Definition 1.9: adjacency lists and arc list"

    Let $G=(N,A)$ be a directed graph.

    - The <strong>adjacency lists</strong> store, for every node $i$, the list $L(i)$ of its successors, that is, the heads of the arcs of $\delta^+(i)$. In this module every list is sorted by increasing index.

    - The <strong>arc list</strong> stores two arrays of length $m$, with the tail and the head of every arc.

    For an undirected graph the list $L(v)$ contains the neighbourhood $N(v)$, and every edge appears in two lists.

<a id="box-14-gr-ex-lists"></a>

!!! esempio "Example 1.5: the lists of the reference graph"

    The adjacency lists and the arc list of the reference graph are:

    <div class="tabella" markdown="0"><table>
    <tr>
    <th><span class="arithmatex">\(i\)</span></th>
    <th><span class="arithmatex">\(L(i)\)</span></th>
    </tr>
    <tr>
    <td><span class="arithmatex">\(1\)</span></td>
    <td><span class="arithmatex">\(2,~3\)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">\(2\)</span></td>
    <td><span class="arithmatex">\(4\)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">\(3\)</span></td>
    <td><span class="arithmatex">\(2,~5\)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">\(4\)</span></td>
    <td><span class="arithmatex">\(3,~6\)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">\(5\)</span></td>
    <td><span class="arithmatex">\(4,~6\)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">\(6\)</span></td>
    <td>(empty)</td>
    </tr>
    </table></div>

    <div class="tabella" markdown="0"><table>
    <tr>
    <th>arc</th>
    <th><span class="arithmatex">\(a_1\)</span></th>
    <th><span class="arithmatex">\(a_2\)</span></th>
    <th><span class="arithmatex">\(a_3\)</span></th>
    <th><span class="arithmatex">\(a_4\)</span></th>
    <th><span class="arithmatex">\(a_5\)</span></th>
    <th><span class="arithmatex">\(a_6\)</span></th>
    <th><span class="arithmatex">\(a_7\)</span></th>
    <th><span class="arithmatex">\(a_8\)</span></th>
    <th><span class="arithmatex">\(a_9\)</span></th>
    </tr>
    <tr>
    <td>tail</td>
    <td><span class="arithmatex">\(1\)</span></td>
    <td><span class="arithmatex">\(1\)</span></td>
    <td><span class="arithmatex">\(2\)</span></td>
    <td><span class="arithmatex">\(3\)</span></td>
    <td><span class="arithmatex">\(3\)</span></td>
    <td><span class="arithmatex">\(4\)</span></td>
    <td><span class="arithmatex">\(4\)</span></td>
    <td><span class="arithmatex">\(5\)</span></td>
    <td><span class="arithmatex">\(5\)</span></td>
    </tr>
    <tr>
    <td>head</td>
    <td><span class="arithmatex">\(2\)</span></td>
    <td><span class="arithmatex">\(3\)</span></td>
    <td><span class="arithmatex">\(4\)</span></td>
    <td><span class="arithmatex">\(2\)</span></td>
    <td><span class="arithmatex">\(5\)</span></td>
    <td><span class="arithmatex">\(3\)</span></td>
    <td><span class="arithmatex">\(6\)</span></td>
    <td><span class="arithmatex">\(4\)</span></td>
    <td><span class="arithmatex">\(6\)</span></td>
    </tr>
    </table></div>

    The lists of the underlying undirected graph are $L(1)=\{2,3\}$, $L(2)=\{1,3,4\}$, $L(3)=\{1,2,4,5\}$, $L(4)=\{2,3,5,6\}$, $L(5)=\{3,4,6\}$ and $L(6)=\{4,5\}$.

## 1.2.1 Space and access time

- The table compares the four representations of a directed graph. The space is the number of stored entries; the two operations are the test of an arc and the scan of the successors of a node.

<div class="tabella" markdown="0"><table>
<tr>
<th>representation</th>
<th>space</th>
<th>is <span class="arithmatex">\((i,j) \in A\)</span>?</th>
<th>successors of <span class="arithmatex">\(i\)</span></th>
</tr>
<tr>
<td>adjacency matrix</td>
<td><span class="arithmatex">\(n^2\)</span></td>
<td><span class="arithmatex">\(O(1)\)</span></td>
<td><span class="arithmatex">\(O(n)\)</span></td>
</tr>
<tr>
<td>node–arc incidence matrix</td>
<td><span class="arithmatex">\(n\,m\)</span></td>
<td><span class="arithmatex">\(O(m)\)</span></td>
<td><span class="arithmatex">\(O(m)\)</span></td>
</tr>
<tr>
<td>arc list</td>
<td><span class="arithmatex">\(2\,m\)</span></td>
<td><span class="arithmatex">\(O(m)\)</span></td>
<td><span class="arithmatex">\(O(m)\)</span></td>
</tr>
<tr>
<td>adjacency lists</td>
<td><span class="arithmatex">\(n+m\)</span></td>
<td><span class="arithmatex">\(O(\deg^+(i))\)</span></td>
<td><span class="arithmatex">\(O(\deg^+(i))\)</span></td>
</tr>
</table></div>

- For the reference graph the four representations store $36$, $54$, $18$ and $15$ entries.

- A simple directed graph has $m \le n(n-1)$. In the networks of the applications $m$ is much smaller than $n^2$ (the graph is <strong>sparse</strong>), and the adjacency lists are the representation of choice for the algorithms.

## 1.2.2 The incidence matrix and flow conservation

- Given a value $x_{ij}$ for every arc, row $i$ of $\mat{B}\vet{x}$ is what leaves node $i$ minus what enters it:

    $$
    (\mat{B}\vet{x})_i=\sum_{(i,j) \in \delta^+(i)} x_{ij} \;-\; \sum_{(j,i) \in \delta^-(i)} x_{ji},
    \qquad \forall i \in N.
    $$

- With $x_{ij}=1$ for every arc of the reference graph, $\mat{B}\vet{x}$ is the vector of the differences $\deg^+(i)-\deg^-(i)$:

    $$
    \mat{B}\vet{x}=(2,\,-1,\,0,\,0,\,1,\,-2)' .
    $$

!!! chiave ""

    The node–arc incidence matrix has $+1$ in the tail and $-1$ in the head of every arc; the adjacency lists store a graph in $n+m$ space and give the successors of a node in $O(\deg^+(i))$ time.

---

**Next:** [1.3 Connectivity](connectivity.md)

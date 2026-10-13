---
title: "Uniqueness of the minimum spanning tree"
---

# 2.7 Uniqueness of the minimum spanning tree

<div class="info-capitolo" markdown>

**Part 2 · Trees and paths · Chapter 2** · [:material-book-open-variant: Chapter 2: Spanning trees](index.md) · [:material-file-pdf-box: Lecture notes, volume 2 (PDF)](../../pdf/lecture-notes-2-trees-and-paths.pdf) · [:material-pencil: Exercises: Spanning trees](../../exercises/minimum-spanning-trees.md) · [:material-gesture-tap: App: Minimum spanning trees: Kruskal and Prim](../../lab/minimum-spanning-tree-kruskal-prim.md)

</div>

<a id="sez-sec-mst-uniqueness"></a>
<a id="box-23-mst-th-unique"></a>

!!! teorema "Theorem 2.15: distinct weights"

    If the weights $w_e$, $e \in E$, are pairwise distinct, the connected graph $G=(V,E)$ has exactly one minimum spanning tree.

??? dimostrazione "Proof"

    Assume that $T_1 \neq T_2$ are minimum spanning trees. They have the same number of edges, so the symmetric difference $(T_1 \setminus T_2) \cup (T_2 \setminus T_1)$ is nonempty; let $e$ be its lightest edge, and say $e \in T_1 \setminus T_2$.

    1. The cycle $C(T_2,e)$ is not contained in the acyclic $T_1$, so it has an edge $f \notin T_1$; $f \neq e$, and $f \in T_2$, so $f \in T_2 \setminus T_1$.

    2. $f$ is in the symmetric difference and $f \neq e$, so $w_f>w_e$, the weights being distinct.

    3. $T_2 \cup \{e\} \setminus \{f\}$ is a spanning tree (<span style="color:#1971c2">[Lemma 2.5](cuts-and-cycles.md#box-7-mst-lem-exchange)</span>) of weight $w(T_2)+w_e-w_f<w(T_2)$: a contradiction. <span class="qed">□</span>

- With distinct weights, Kruskal's algorithm, Prim's algorithm from any start vertex and every execution of the generic greedy algorithm return the same tree.

- On the reference graph, Prim's algorithm from $s=6$ adds $\{5,6\},\{4,5\},\{3,4\},\{1,3\},\{2,3\}$: once more the tree $\tilde{F}$.

### 2.7.1 Weights with ties

<a id="box-24-mst-prop-ties"></a>

!!! teorema "Proposition 2.16: edges in every or in no minimum spanning tree"

    Let $T$ be a minimum spanning tree of $G=(V,E)$.

    - **(a)** An edge $e \in T$ belongs to every minimum spanning tree if and only if $w_e<w_f$ for every $f \neq e$ in the fundamental cut of $e$.

    - **(b)** An edge $e \notin T$ belongs to no minimum spanning tree if and only if $w_e>w_f$ for every $f \neq e$ in $C(T,e)$.

    In particular, $T$ is the unique minimum spanning tree if and only if every edge outside $T$ is strictly heavier than the other edges of its fundamental cycle.

??? dimostrazione "Proof"

    - **(a)** If the inequalities hold, $e$ is in every minimum spanning tree by the cut property (<span style="color:#1971c2">[Theorem 2.6](the-cut-property-and-the-cycle-property.md#box-9-mst-th-cut)</span>(b)). Otherwise some $f \neq e$ in the fundamental cut has $w_f \le w_e$, and $w_f \ge w_e$ by the cut condition (<span style="color:#1971c2">[Theorem 2.8](the-cut-property-and-the-cycle-property.md#box-12-mst-th-optimality)</span>): so $w_f=w_e$, and $T \cup \{f\} \setminus \{e\}$ is a spanning tree (<span style="color:#1971c2">[Lemma 2.5](cuts-and-cycles.md#box-7-mst-lem-exchange)</span>(2)) of the same weight, without $e$.

    - **(b)** If the inequalities hold, $e$ is in no minimum spanning tree by the cycle property (<span style="color:#1971c2">[Theorem 2.7](the-cut-property-and-the-cycle-property.md#box-10-mst-th-cycle)</span>(b)). Otherwise some $f \neq e$ in $C(T,e)$ has $w_f=w_e$, by the cycle condition, and $T \cup \{e\} \setminus \{f\}$ is a minimum spanning tree containing $e$.

    For the last claim: $T$ is unique if and only if no edge outside $T$ belongs to a minimum spanning tree, that is, (b) holds for every $e \notin T$. <span class="qed">□</span>

<a id="box-25-mst-ex-ties"></a>

!!! esempio "Example 2.9: ties on the reference graph"

    - Let $w_{12}=3$ instead of $4$, so that $w_{12}=w_{23}=3$. The fundamental cycle of $\{1,2\}$ in $\tilde{F}$ is $1,3,2,1$, with $w_{23}=w_{12}$: by <span style="color:#1971c2">[Proposition 2.16](#box-24-mst-prop-ties)</span>(b), the tree $\{1,2\},\{1,3\},\{3,4\},\{4,5\},\{5,6\}$ is also optimal, with weight $18$.

    - Enumeration confirms that these are the only two minimum spanning trees. Kruskal's algorithm, scanning $\{1,2\}$ before $\{2,3\}$, returns the one with $\{1,2\}$.

    - Ties do not always create several optimal trees: with $w_{35}=w_{46}=9$ the tree $\tilde{F}$ is still the unique minimum spanning tree, because each of the four edges outside it remains strictly the heaviest of its cycle.

!!! chiave ""

    With distinct weights the minimum spanning tree is unique. With ties, a tree is the unique optimum if and only if every edge outside it is strictly the heaviest of its fundamental cycle.

## 2.8 Typical mistakes

!!! attenzione "Warning"

    - <strong>Using the cut property with a cut crossed by $F$.</strong> The lightest edge of $\delta(S)$ is safe only if no edge already chosen crosses $\delta(S)$.

    - <strong>Accepting an edge in Kruskal's algorithm because it touches a new vertex.</strong> The test is whether the two endpoints are in different components: $\{3,4\}$ is accepted although both $3$ and $4$ are already covered.

    - <strong>Updating the labels in Prim's algorithm with path lengths.</strong> The new label is the weight $w_{vu}$ of a single edge, not $d(v)+w_{vu}$: that is Dijkstra's algorithm for shortest paths.

    - <strong>Forgetting that the labels can only decrease.</strong> In Prim's algorithm $d(u)$ changes only when $w_{vu}<d(u)$.

    - <strong>Claiming uniqueness from the algorithm.</strong> Kruskal and Prim return one tree; with ties other optimal trees may exist, and they are found through the equalities in the fundamental cycles.

    - <strong>Applying the algorithms to directed graphs.</strong> A minimum spanning tree is defined on undirected graphs; in a directed graph the orientation of the arcs is ignored.

## 2.9 In summary

!!! chiave "In summary"

    - A minimum spanning tree is a spanning tree of minimum total weight of a connected weighted graph; it has $n-1$ edges.

    - Cut property: the lightest edge of a cut not crossed by $F$ extends $F$ within some minimum spanning tree. Cycle property: the heaviest edge of a cycle can be left out, and if it is strictly the heaviest it is in no optimum.

    - A spanning tree is optimal if and only if every edge outside it is the heaviest of its fundamental cycle, or equivalently every tree edge is the lightest of its fundamental cut.

    - Kruskal's algorithm sorts the edges and accepts those joining two components, in $O(m\log n)$ time; Prim's algorithm grows one tree with the labels $d(v)$, in $O(n^2)$ time.

    - With distinct weights the minimum spanning tree is unique.

    <strong>The weighted reference graph at a glance.</strong>

    <div class="tabella" markdown="0"><table>
    <tr>
    <td>vertices, edges, spanning trees</td>
    <td><span class="arithmatex">\(n=6\)</span>, <span class="arithmatex">\(m=9\)</span>, <span class="arithmatex">\(55\)</span></td>
    </tr>
    <tr>
    <td>minimum spanning tree</td>
    <td><span class="arithmatex">\(\{1,3\},\{2,3\},\{3,4\},\{4,5\},\{5,6\}\)</span>, weight <span class="arithmatex">\(18\)</span> (unique)</td>
    </tr>
    <tr>
    <td>Kruskal</td>
    <td>accepts <span class="arithmatex">\(\{1,3\},\{4,5\},\{2,3\},\{3,4\},\{5,6\}\)</span>; rejects <span class="arithmatex">\(\{1,2\},\{2,4\}\)</span></td>
    </tr>
    <tr>
    <td>Prim from <span class="arithmatex">\(1\)</span></td>
    <td>selects <span class="arithmatex">\(3,2,4,5,6\)</span></td>
    </tr>
    </table></div>

---

**Exercises on this chapter:** [:material-pencil: Spanning trees](../../exercises/minimum-spanning-trees.md)


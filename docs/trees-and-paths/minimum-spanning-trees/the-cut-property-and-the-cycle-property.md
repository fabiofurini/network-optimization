---
title: "The cut property and the cycle property"
---

# 2.3 The cut property and the cycle property { #sez-sec-mst-properties }

<div class="info-capitolo" markdown>

**Part 2 · Trees and paths · Chapter 2** · [:material-book-open-variant: Chapter 2: Spanning trees](index.md) · [:material-file-pdf-box: Lecture notes, volume 2 (PDF)](../../pdf/lecture-notes-2-trees-and-paths.pdf) · [:material-presentation: Slides](../../pdf/slides-minimum-spanning-trees.pdf) · [:material-pencil: Exercises: Spanning trees](../../exercises/minimum-spanning-trees.md) · [:material-gesture-tap: App: Minimum spanning trees: Kruskal and Prim](../../lab/minimum-spanning-tree-kruskal-prim.md)

</div>

<a id="box-9-mst-th-cut"></a>

!!! teorema "Theorem 2.6: cut property"

    Let $G=(V,E)$ be a connected graph with weights $w_e$, and let $F \subseteq E$ be contained in some minimum spanning tree. Let $\delta(S)$ be a cut with $F \cap \delta(S)=\emptyset$, and let $e$ be an edge of minimum weight in $\delta(S)$.

    - **(a)** $F \cup \{e\}$ is contained in some minimum spanning tree.

    - **(b)** If $w_e<w_f$ for every $f \in \delta(S) \setminus \{e\}$, then $e$ belongs to every minimum spanning tree.

??? dimostrazione "Proof"

    Let $T^\star$ be a minimum spanning tree with $F \subseteq T^\star$; for (b), let $T^\star$ be any minimum spanning tree and $F=\emptyset$. If $e \in T^\star$ there is nothing to prove; let $e \notin T^\star$.

    1. The fundamental cycle $C(T^\star,e)$ contains the edge $e$ of $\delta(S)$, so it contains another edge $f \in \delta(S)$, $f \neq e$ (<span style="color:#1971c2">[Lemma 2.3](cuts-and-cycles.md#box-5-mst-lem-even)</span>). All its edges other than $e$ are in $T^\star$, so $f \in T^\star$; and $f \notin F$, since $F \cap \delta(S)=\emptyset$.

    2. By <span style="color:#1971c2">[Lemma 2.5](cuts-and-cycles.md#box-7-mst-lem-exchange)</span>, $T'=T^\star \cup \{e\} \setminus \{f\}$ is a spanning tree, with $w(T')=w(T^\star)+w_e-w_f$.

    3. (a) $e$ has minimum weight in $\delta(S)$, so $w_e \le w_f$ and $w(T') \le w(T^\star)$: $T'$ is a minimum spanning tree containing $F \cup \{e\}$.

    4. (b) Here $w_e<w_f$ and $w(T')<w(T^\star)$, against the optimality of $T^\star$: hence $e \in T^\star$. <span class="qed">□</span>

<a id="box-10-mst-th-cycle"></a>

!!! teorema "Theorem 2.7: cycle property"

    Let $G=(V,E)$ be a connected graph with weights $w_e$, let $C$ be a cycle of $G$ and $e$ an edge of maximum weight in $C$.

    - **(a)** Some minimum spanning tree does not contain $e$.

    - **(b)** If $w_e>w_f$ for every $f \in C \setminus \{e\}$, then no minimum spanning tree contains $e$.

??? dimostrazione "Proof"

    Let $T^\star$ be a minimum spanning tree with $e \in T^\star$ (if there is none, both claims hold), and let $\delta(S_e)$ be the fundamental cut of $e$ in $T^\star$.

    1. The cycle $C$ contains the edge $e$ of $\delta(S_e)$, so it contains another edge $f \in \delta(S_e)$ (<span style="color:#1971c2">[Lemma 2.3](cuts-and-cycles.md#box-5-mst-lem-even)</span>); $f \notin T^\star$, because $e$ is the only edge of $T^\star$ in its fundamental cut.

    2. By <span style="color:#1971c2">[Lemma 2.5](cuts-and-cycles.md#box-7-mst-lem-exchange)</span>(2), $T'=T^\star \cup \{f\} \setminus \{e\}$ is a spanning tree, with $w(T')=w(T^\star)+w_f-w_e$.

    3. (a) $w_f \le w_e$, so $T'$ is a minimum spanning tree without $e$. (b) $w_f<w_e$ would give $w(T')<w(T^\star)$, a contradiction: no minimum spanning tree contains $e$. <span class="qed">□</span>

<a id="box-11-mst-ex-properties"></a>

!!! esempio "Example 2.4: the two properties on the reference graph"

    - <em>Cut property.</em> The edge $\{3,4\}$, of weight $5$, is the unique lightest edge of $\delta(\{1,2,3\})=\{\{2,4\},\{3,4\},\{3,5\}\}$, with weights $6,5,8$: it belongs to every minimum spanning tree. In the same way, $\{5,6\}$ is the unique lightest edge of $\delta(\{6\})$.

    - <em>Cycle property.</em> The edge $\{1,2\}$ is the unique heaviest edge of the cycle $1,2,3$ (weights $4,3,1$), and $\{3,5\}$ is the unique heaviest edge of the cycle $3,4,5$ (weights $5,2,8$): no minimum spanning tree contains them. The cycles $2,3,4$ and $4,5,6$ exclude $\{2,4\}$ and $\{4,6\}$.

    - The four excluded edges leave exactly the $5$ edges of $\tilde{F}$: the two properties alone prove that $\tilde{F}$ is the unique minimum spanning tree.

## 2.3.1 Optimality conditions

<a id="box-12-mst-th-optimality"></a>

!!! teorema "Theorem 2.8: optimality conditions"

    Let $T$ be a spanning tree of a connected graph $G=(V,E)$ with weights $w_e$. The following statements are equivalent:

    - **(i)** $T$ is a minimum spanning tree;

    - **(ii)** <strong>cycle condition</strong>: for every $e \notin T$, $w_e \ge w_f$ for every edge $f$ of $C(T,e)$;

    - **(iii)** <strong>cut condition</strong>: for every $e \in T$, $w_e \le w_f$ for every edge $f$ of the fundamental cut of $e$.

??? dimostrazione "Proof"

    We prove (i)$\Rightarrow$(iii)$\Rightarrow$(ii)$\Rightarrow$(i).

    - <strong>(i)$\Rightarrow$(iii).</strong> If $f$ crosses the fundamental cut of $e \in T$ with $w_f<w_e$, then $T \cup \{f\} \setminus \{e\}$ is a spanning tree (<span style="color:#1971c2">[Lemma 2.5](cuts-and-cycles.md#box-7-mst-lem-exchange)</span>(2)) lighter than $T$.

    - <strong>(iii)$\Rightarrow$(ii).</strong> Let $e \notin T$ and $f \in C(T,e)$, $f \neq e$. The path of $T$ between the endpoints of $e$ uses $f$, and it is unique, so removing $f$ separates them: $e$ crosses the fundamental cut of $f$, and $w_f \le w_e$ by (iii).

    <strong>(ii)$\Rightarrow$(i).</strong> Among the minimum spanning trees, let $T^\star$ have the largest number of edges in common with $T$, and assume $T^\star \neq T$.

    1. Take $e \in T^\star \setminus T$, and let $\delta(S_e)$ be its fundamental cut in $T^\star$. The cycle $C(T,e)$ contains $e$, so it contains another edge $f \in \delta(S_e)$ (<span style="color:#1971c2">[Lemma 2.3](cuts-and-cycles.md#box-5-mst-lem-even)</span>), with $f \in T$ and $f \notin T^\star$.

    2. By <span style="color:#1971c2">[Lemma 2.5](cuts-and-cycles.md#box-7-mst-lem-exchange)</span>(2), $T'=T^\star \cup \{f\} \setminus \{e\}$ is a spanning tree, and $w_f \le w_e$ by (ii) applied to $e \notin T$. Hence $w(T') \le w(T^\star)$.

    3. $T'$ is a minimum spanning tree with one more edge in common with $T$: a contradiction. So $T=T^\star$. <span class="qed">□</span>

<a id="box-13-mst-ex-certificate"></a>

!!! esempio "Example 2.5: certifying the optimal tree"

    For the tree $\tilde{F}$ of <span style="color:#1971c2">[Example 2.2](the-minimum-spanning-tree-problem.md#box-3-mst-ex-opt)</span>, the four edges outside the tree and their fundamental cycles are:

    <div class="tabella" markdown="0"><table>
    <tr>
    <th>edge <span class="arithmatex">\(e \notin \tilde{F}\)</span></th>
    <th><span class="arithmatex">\(C(\tilde{F},e)\)</span></th>
    <th>weights of the tree edges of the cycle</th>
    </tr>
    <tr>
    <td><span class="arithmatex">\(\{1,2\}\)</span>, <span class="arithmatex">\(w=4\)</span></td>
    <td><span class="arithmatex">\(1,3,2,1\)</span></td>
    <td><span class="arithmatex">\(1,~3\)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">\(\{2,4\}\)</span>, <span class="arithmatex">\(w=6\)</span></td>
    <td><span class="arithmatex">\(2,3,4,2\)</span></td>
    <td><span class="arithmatex">\(3,~5\)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">\(\{3,5\}\)</span>, <span class="arithmatex">\(w=8\)</span></td>
    <td><span class="arithmatex">\(3,4,5,3\)</span></td>
    <td><span class="arithmatex">\(5,~2\)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">\(\{4,6\}\)</span>, <span class="arithmatex">\(w=9\)</span></td>
    <td><span class="arithmatex">\(4,5,6,4\)</span></td>
    <td><span class="arithmatex">\(2,~7\)</span></td>
    </tr>
    </table></div>

    Every edge outside the tree is at least as heavy as the tree edges of its cycle: by <span style="color:#1971c2">[Theorem 2.8](#box-12-mst-th-optimality)</span> the tree is optimal, without enumerating the $55$ spanning trees.

<a id="box-14-mst-ex-improve"></a>

!!! esempio "Example 2.6: improving a tree that is not optimal"

    The BFS tree $T=\{\{1,2\},\{1,3\},\{2,4\},\{3,5\},\{4,6\}\}$, of weight $28$, violates the cycle condition. For $e=\{4,5\}$, of weight $2$, the fundamental cycle $4,2,1,3,5,4$ contains $\{2,4\}$, $\{1,2\}$ and $\{3,5\}$, of weights $6,4,8$.

    - Removing the heaviest of them, $\{3,5\}$, and adding $\{4,5\}$ gives a spanning tree of weight $28+2-8=22$.

    - The proof of <span style="color:#1971c2">[Theorem 2.8](#box-12-mst-th-optimality)</span> turns into an algorithm: repeat the exchange while an edge violates the condition. The algorithms of the next sections are faster.

!!! chiave ""

    The lightest edge of a cut belongs to some minimum spanning tree, and the heaviest edge of a cycle can be left out. A spanning tree is optimal if and only if every edge outside it is the heaviest of its fundamental cycle.

---

**Next:** [2.4 The generic greedy algorithm](the-generic-greedy-algorithm.md)

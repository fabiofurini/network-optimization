---
title: "The generic greedy algorithm"
---

# 2.4 The generic greedy algorithm { #sez-sec-mst-greedy }

<div class="info-capitolo" markdown>

**Part 2 · Trees and paths · Chapter 2** · [:material-book-open-variant: Chapter 2: Spanning trees](index.md) · [:material-file-pdf-box: Lecture notes, volume 2 (PDF)](../../pdf/lecture-notes-2-trees-and-paths.pdf) · [:material-presentation: Slides](../../pdf/slides-minimum-spanning-trees.pdf) · [:material-pencil: Exercises: Spanning trees](../../exercises/minimum-spanning-trees.md) · [:material-gesture-tap: App: Minimum spanning trees: Kruskal and Prim](../../lab/minimum-spanning-tree-kruskal-prim.md)

</div>

- The cut property suggests building a minimum spanning tree one edge at a time: the current set $F$ is always contained in some minimum spanning tree, and the next edge is the lightest edge of a cut not crossed by $F$.

!!! algoritmo "Algorithm: Generic greedy algorithm for the MST"

    <div class="pseudocodice" markdown="0"><div class="pc" style="--liv:0"><strong>Input:</strong> a connected undirected graph <span class="arithmatex">\(G=(V,E)\)</span> with weights <span class="arithmatex">\(w_e\)</span></div><div class="pc" style="--liv:0"><strong>Output:</strong> a minimum spanning tree <span class="arithmatex">\(F\)</span></div><div class="pc" style="--liv:0"><span class="pc-n">1</span><strong>Step 0 (initialization).</strong> Set <span class="arithmatex">\(F:=\emptyset\)</span>.</div><div class="pc" style="--liv:0"><span class="pc-n">2</span><strong>Step 1 (stopping test).</strong> If <span class="arithmatex">\(|F|=n-1\)</span>, <code>STOP</code>.</div><div class="pc" style="--liv:0"><span class="pc-n">3</span><strong>Step 2 (augmentation).</strong> Choose a cut <span class="arithmatex">\(\delta(S)\)</span> with <span class="arithmatex">\(F \cap \delta(S)=\emptyset\)</span>, and add to <span class="arithmatex">\(F\)</span> an edge of
    minimum weight in <span class="arithmatex">\(\delta(S)\)</span>. Go to Step 1.</div></div>

<a id="box-15-mst-th-greedy"></a>

!!! teorema "Theorem 2.9: correctness of the generic greedy algorithm"

    At every iteration of the generic greedy algorithm a cut as in Step 2 exists and is nonempty, and $F$ is contained in some minimum spanning tree. At the end, $F$ is a minimum spanning tree.

??? dimostrazione "Proof"

    By induction on the iterations; $F=\emptyset$ is contained in every minimum spanning tree.

    1. If $|F|<n-1$, the graph $(V,F)$ is a forest (a subset of a tree) with $n-|F| \ge 2$ components. Let $S$ be one of them: no edge of $F$ crosses $\delta(S)$, and $\delta(S) \neq \emptyset$ because $G$ is connected.

    2. By the cut property (<span style="color:#1971c2">[Theorem 2.6](the-cut-property-and-the-cycle-property.md#box-9-mst-th-cut)</span>(a)), the new set $F \cup \{e\}$ is still contained in some minimum spanning tree.

    3. When $|F|=n-1$, $F$ is contained in a minimum spanning tree $T^\star$ with $n-1$ edges, so $F=T^\star$. <span class="qed">□</span>

- The added edge $e=\{u,v\}$ has $u \in S$ and $v \notin S$, and no edge of $F$ crosses $\delta(S)$: $u$ and $v$ are in different components of $(V,F)$, so $e$ does not close a cycle.

- The algorithms of Kruskal and of Prim are two ways of choosing the cut in Step 2.

!!! chiave ""

    Adding, $n-1$ times, the lightest edge of a cut not crossed by the current edges builds a minimum spanning tree.

---

**Next:** [2.5 Kruskal's algorithm](kruskal-s-algorithm.md)

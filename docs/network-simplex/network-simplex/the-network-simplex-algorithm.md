---
title: "The network simplex algorithm"
---

# 8.5 The network simplex algorithm { #sez-sec-ns-algorithm }

<div class="info-capitolo" markdown>

**Part 4 · The network simplex · Chapter 8** · [:material-book-open-variant: Chapter 8: Network simplex](index.md) · [:material-file-pdf-box: Lecture notes, volume 4 (PDF)](../../pdf/lecture-notes-4-network-simplex.pdf) · [:material-presentation: Slides](../../pdf/slides-network-simplex.pdf) · [:material-pencil: Exercises: Network simplex](../../exercises/network-simplex.md) · [:material-gesture-tap: App: The network simplex, pivot by pivot](../../lab/network-simplex.md)

</div>

!!! algoritmo "Algorithm: Network simplex algorithm"

    <div class="pseudocodice" markdown="0"><div class="pc" style="--liv:0"><strong>Input:</strong> a network <span class="arithmatex">\(G=(N,A)\)</span> with a feasible tree structure <span class="arithmatex">\((T,L,U)\)</span></div><div class="pc" style="--liv:0"><strong>Output:</strong> an optimal tree solution, or a cycle that proves that the problem is unbounded</div><div class="pc" style="--liv:0"><span class="pc-n">1</span><strong>Step 0 (initialization).</strong> Compute the tree solution <span class="arithmatex">\(\vet{x}\)</span> from the leaves,</div><div class="pc" style="--liv:0"><span class="pc-n">2</span>  and the potentials <span class="arithmatex">\(\vet{\pi}\)</span> from the root <span class="arithmatex">\(n\)</span>, with <span class="arithmatex">\(\pi_n=0\)</span>.</div><div class="pc" style="--liv:0"><span class="pc-n">3</span><strong>Step 1 (optimality check).</strong> Compute the reduced costs <span class="arithmatex">\(\bar{c}_{ij}=c_{ij}-\pi_i+\pi_j\)</span>.</div><div class="pc" style="--liv:0"><span class="pc-n">4</span>  If <span class="arithmatex">\(\bar{c}_{ij} \ge 0\)</span> on <span class="arithmatex">\(L\)</span> and <span class="arithmatex">\(\bar{c}_{ij} \le 0\)</span> on <span class="arithmatex">\(U\)</span>, <code>STOP</code>: <span class="arithmatex">\(\vet{x}\)</span> is optimal.</div><div class="pc" style="--liv:0"><span class="pc-n">5</span><strong>Step 2 (entering arc).</strong> Choose the eligible arc <span class="arithmatex">\(e\)</span> with the largest <span class="arithmatex">\(|\bar{c}_{ij}|\)</span>.</div><div class="pc" style="--liv:0"><span class="pc-n">6</span>  Orient its cycle <span class="arithmatex">\(C\)</span> as <span class="arithmatex">\(e\)</span> if <span class="arithmatex">\(e \in L\)</span>, and against <span class="arithmatex">\(e\)</span> if <span class="arithmatex">\(e \in U\)</span>.</div><div class="pc" style="--liv:0"><span class="pc-n">7</span><strong>Step 3 (ratio test).</strong> Compute <span class="arithmatex">\(\theta\)</span>, the minimum residual capacity along <span class="arithmatex">\(C\)</span>.</div><div class="pc" style="--liv:0"><span class="pc-n">8</span>  If <span class="arithmatex">\(\theta=+\infty\)</span>, <code>STOP</code>: the problem is unbounded.</div><div class="pc" style="--liv:0"><span class="pc-n">9</span>  Otherwise the leaving arc <span class="arithmatex">\(f\)</span> is the last blocking arc along <span class="arithmatex">\(C\)</span> from the apex.</div><div class="pc" style="--liv:0"><span class="pc-n">10</span><strong>Step 4 (update).</strong> Send <span class="arithmatex">\(\theta\)</span> units along <span class="arithmatex">\(C\)</span>, and set <span class="arithmatex">\(T:=T \cup \{e\} \setminus \{f\}\)</span>.</div><div class="pc" style="--liv:0"><span class="pc-n">11</span>  The arc <span class="arithmatex">\(f\)</span> goes to <span class="arithmatex">\(U\)</span> or to <span class="arithmatex">\(L\)</span>.</div><div class="pc" style="--liv:0"><span class="pc-n">12</span>  Update the potentials of the subtree cut off by <span class="arithmatex">\(f\)</span>, and go to Step 1.</div></div>

- Ties in Step 2 are broken by the lexicographic order of the arcs. Step 0 uses the procedure of <span style="color:#1971c2">[Proposition 8.6](bases-and-spanning-trees.md#box-7-ns-prop-leaves)</span>, Step 4 the updates of <span style="color:#1971c2">[Proposition 8.12](the-pivot.md#box-15-ns-prop-pivot)</span> and <span style="color:#1971c2">[Proposition 8.13](the-pivot.md#box-16-ns-prop-update)</span>.

- The stop in Step 1 is correct by <span style="color:#1971c2">[Theorem 8.10](potentials-and-optimality.md#box-12-ns-th-optimality)</span>, the stop in Step 3 by <span style="color:#1971c2">[Proposition 8.14](the-pivot.md#box-17-ns-prop-unbounded)</span>.

- Every structure met is feasible by <span style="color:#1971c2">[Proposition 8.12](the-pivot.md#box-15-ns-prop-pivot)</span>. With integer balances and capacities all the flows are integer (<span style="color:#1971c2">[Corollary 8.4](bases-and-spanning-trees.md#box-5-ns-cor-integer)</span>), and with integer costs all the potentials are integer.

<a id="box-19-ns-prop-finite"></a>

!!! teorema "Proposition 8.15: termination without degenerate pivots"

    If every pivot of the algorithm has $\theta>0$, the algorithm stops after a finite number of pivots.

??? dimostrazione "Proof"

    A tree structure determines its tree solution, hence its cost. By <span style="color:#1971c2">[Proposition 8.12](the-pivot.md#box-15-ns-prop-pivot)</span> every pivot with $\theta>0$ decreases the cost by $\theta|\bar{c}_{kl}|>0$, so no tree structure is met twice. There are finitely many tree structures: at most $\binom{m}{n-1}$ trees, each with at most $2^{m-n+1}$ bound statuses. <span class="qed">□</span>

## 8.5.1 The algebra of the pivot

- In the language of [Chapter 11 «Revised simplex algorithm»](https://fabiofurini.github.io/linear-programming/advanced-methods/11-revised-simplex/), the potentials solve the first system $\vet{\pi}'\mat{M}_T=\vet{c}_T'$.

- The second system $\mat{M}_T\vet{d}=\mat{M}_e$ is solved by the tree path from $k$ to $l$: by [Chapter 1, Lemma «columns of a cycle»](https://fabiofurini.github.io/network-optimization/graphs/graphs/the-rank-of-the-incidence-matrix/), $d_a=+1$ on the arcs of the path traversed from tail to head, $d_a=-1$ on the others, and $d_a=0$ off the path. Increasing $x_e$ by $t$ changes the basic variables by $-t\,\vet{d}$: this is the flow sent around the fundamental cycle.

- The potential method for the transportation problem in [Chapter 7 «Transportation and assignment»](https://fabiofurini.github.io/network-optimization/flows/transportation-and-assignment/) is the network simplex algorithm on the bipartite graph of origins and destinations: the basic cells form a spanning tree, and the potentials and reduced costs are those of this chapter.

!!! chiave ""

    The network simplex algorithm moves from tree to tree: potentials from the root, reduced costs, entering arc, cycle, step, leaving arc. Without degenerate pivots the cost decreases at every pivot, and the algorithm stops.

---

**Next:** [8.6 An uncapacitated example](an-uncapacitated-example.md)

---
title: "Optimality conditions and potentials"
---

# 3.2 Optimality conditions and potentials { #sez-sec-sp-potentials }

<div class="info-capitolo" markdown>

**Part 2 · Trees and paths · Chapter 3** · [:material-book-open-variant: Chapter 3: Shortest paths](index.md) · [:material-file-pdf-box: Lecture notes, volume 2 (PDF)](../../pdf/lecture-notes-2-trees-and-paths.pdf) · [:material-presentation: Slides](../../pdf/slides-shortest-paths.pdf) · [:material-pencil: Exercises: Shortest paths](../../exercises/shortest-paths.md) · [:material-gesture-tap: App: Shortest paths: Dijkstra, Bellman–Ford, acyclic graphs](../../lab/shortest-paths-dijkstra-bellman-ford.md)

</div>

<a id="box-10-sp-def-potentials"></a>

!!! definizione "Definition 3.7: potentials and reduced costs"

    A vector $\vet{\pi} \in \R^n$ gives a <strong>potential</strong> $\pi_i$ to every node $i \in N$. The <strong>reduced cost</strong> of the arc $(i,j)$ with respect to $\vet{\pi}$ is

    $$
    \bar{c}_{ij}=d_{ij}-\pi_i+\pi_j .
    $$

    The potentials are <strong>feasible</strong> if $\bar{c}_{ij} \ge 0$ for every arc $(i,j) \in A$, and an arc with $\bar{c}_{ij}=0$ is <strong>tight</strong>.

- Given <strong>labels</strong> $d(j)$, lengths of walks from $s$ to $j$, we use the potentials $\pi_i=-d(i)$. Then $\bar{c}_{ij}=d_{ij}+d(i)-d(j)$, and the potentials are feasible if and only if $d(j) \le d(i)+d_{ij}$ for every arc.

- Along a walk $W=i_0,i_1,\dots,i_k$ the potentials telescope:

    $$
    d(W)=\sum_{t=1}^{k} \bar{c}_{i_{t-1}i_t} \;+\; \pi_{i_0}-\pi_{i_k} .
    $$

<a id="box-11-sp-th-certificate"></a>

!!! teorema "Theorem 3.8: potentials as optimality certificate"

    Let $\vet{\pi}$ be feasible potentials, and let $P$ be a path from $s$ to $t$ whose arcs are all tight. Then $P$ is a shortest path from $s$ to $t$, and $d(P)=\pi_s-\pi_t$. Moreover, $G$ has no negative cycle.

??? dimostrazione "Proof"

    We use the telescoping formula above.

    1. The arcs of $P$ have $\bar{c}_{ij}=0$, so $d(P)=\pi_s-\pi_t$.

    2. For every path $Q$ from $s$ to $t$, $d(Q)=\sum_{(i,j) \in Q}\bar{c}_{ij}+\pi_s-\pi_t \ge \pi_s-\pi_t=d(P)$.

    3. For every cycle $C$ the first and the last node coincide, so $d(C)=\sum_{(i,j) \in C}\bar{c}_{ij} \ge 0$. <span class="qed">□</span>

<a id="box-12-sp-cor-conditions"></a>

!!! teorema "Corollary 3.9: optimality conditions for labels"

    Let the labels $d(j)$, $j \in N$, be finite with $d(s)=0$, and assume that

    - **(i)** $d(j) \le d(i)+d_{ij}$ for every arc $(i,j) \in A$;

    - **(ii)** for every $j \neq s$ there is a path from $s$ to $j$ of length $d(j)$.

    Then $d(j)=\tilde{d}(j)$ for every $j \in N$.

??? dimostrazione "Proof"

    By (i) the potentials $\pi_i=-d(i)$ are feasible, so every path $Q$ from $s$ to $j$ has $d(Q) \ge \pi_s-\pi_j=d(j)$ by the argument of <span style="color:#1971c2">[Theorem 3.8](#box-11-sp-th-certificate)</span>. By (ii) the value $d(j)$ is attained by a path, so $d(j)=\tilde{d}(j)$. <span class="qed">□</span>

<a id="box-13-sp-ex-certificate"></a>

!!! esempio "Example 3.4: a certificate on the reference graph"

    With the distances of <span style="color:#1971c2">[Example 3.1](shortest-path-problems.md#box-2-sp-ex-ref)</span> the potentials are $\vet{\pi}=-\tilde{\vet{d}}=(0,-5,-2,-8,-10, -13)$, and the reduced costs $\bar{c}_{ij}=d_{ij}-\pi_i+\pi_j$ are:

    <div class="tabella" markdown="0"><table>
    <tr>
    <th>arc</th>
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
    <td><span class="arithmatex">\(d_{ij}\)</span></td>
    <td><span class="arithmatex">\(7\)</span></td>
    <td><span class="arithmatex">\(2\)</span></td>
    <td><span class="arithmatex">\(3\)</span></td>
    <td><span class="arithmatex">\(3\)</span></td>
    <td><span class="arithmatex">\(8\)</span></td>
    <td><span class="arithmatex">\(1\)</span></td>
    <td><span class="arithmatex">\(5\)</span></td>
    <td><span class="arithmatex">\(2\)</span></td>
    <td><span class="arithmatex">\(7\)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">\(\bar{c}_{ij}\)</span></td>
    <td><span class="arithmatex">\(2\)</span></td>
    <td><span class="arithmatex">\(0\)</span></td>
    <td><span class="arithmatex">\(0\)</span></td>
    <td><span class="arithmatex">\(0\)</span></td>
    <td><span class="arithmatex">\(0\)</span></td>
    <td><span class="arithmatex">\(7\)</span></td>
    <td><span class="arithmatex">\(0\)</span></td>
    <td><span class="arithmatex">\(4\)</span></td>
    <td><span class="arithmatex">\(4\)</span></td>
    </tr>
    </table></div>

    - All reduced costs are non-negative, and the tight arcs are the arcs of the shortest path tree. The path $1,3,2,4,6$ is tight, so it is shortest, with length $\pi_1-\pi_6=13$.

    - The tree of the breadth-first search, $(1,2)$, $(1,3)$, $(2,4)$, $(3,5)$, $(4,6)$, gives the labels $(0,7,2,10,10,15)$. With their potentials, $\bar{c}_{32}=3-(-2)+(-7)=-2<0$: the potentials are not feasible, and entering node $2$ through $(3,2)$ shortens its path by $2$.

!!! chiave ""

    Feasible potentials ($\bar{c}_{ij}=d_{ij}-\pi_i+\pi_j \ge 0$ on every arc) and a path made of tight arcs prove that the path is shortest. With labels, $\pi_i=-d(i)$, and feasibility reads $d(j) \le d(i)+d_{ij}$.

---

**Next:** [3.3 The linear programming formulation](the-linear-programming-formulation.md)

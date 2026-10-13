---
title: "The max-flow min-cut theorem"
---

# 5.4 The max-flow min-cut theorem { #sez-sec-mf-theorem }

<div class="info-capitolo" markdown>

**Part 3 · Flows · Chapter 5** · [:material-book-open-variant: Chapter 5: Maximum flow](index.md) · [:material-file-pdf-box: Lecture notes, volume 3 (PDF)](../../pdf/lecture-notes-3-flows.pdf) · [:material-pencil: Exercises: Maximum flow](../../exercises/maximum-flow.md) · [:material-gesture-tap: App: Maximum flow: Ford–Fulkerson and Edmonds–Karp](../../lab/maximum-flow-ford-fulkerson-edmonds-karp.md)

</div>

<a id="box-12-mf-th-mfmc"></a>

!!! teorema "Theorem 5.8: max-flow min-cut"

    Let $\vet{x}$ be a feasible flow of value $v$. The following statements are equivalent:

    - **(a)** $\vet{x}$ is a maximum flow;

    - **(b)** the residual network $G(\vet{x})$ has no augmenting path;

    - **(c)** $v=u(S,N \setminus S)$ for some $s$–$t$ cut $(S,N \setminus S)$.

    Moreover, a maximum flow exists, and the maximum value of a flow equals the minimum capacity of an $s$–$t$ cut:

    $$
    \tilde{v}=\min \big\{\, u(S,N \setminus S) \;:\; S \subseteq N,~ s \in S,~ t \notin S \,\big\}.
    $$

??? dimostrazione "Proof"

    <em>(a) implies (b).</em> An augmenting path would give, by <span style="color:#1971c2">[Lemma 5.7](the-residual-network.md#box-9-mf-lem-aug)</span>, a feasible flow of value $v+\delta>v$.

    <em>(b) implies (c).</em> Let $S$ be the set of the nodes reachable from $s$ in $G(\vet{x})$; then $s \in S$ and, by (b), $t \notin S$.

    1. If an arc $(i,j) \in \delta^+(S)$ had $x_{ij}<u_{ij}$, the forward arc $(i,j)$ would be in $G(\vet{x})$, and $j$ would be reachable: hence $x_{ij}=u_{ij}$.

    2. If an arc $(i,j) \in \delta^-(S)$ had $x_{ij}>0$, the backward arc $(j,i)$, with $j \in S$, would be in $G(\vet{x})$, and $i$ would be reachable: hence $x_{ij}=0$.

    3. By <span style="color:#1971c2">[Corollary 5.4](cuts.md#box-5-mf-cor-weak)</span>, $v=u(S,N \setminus S)$.

    <em>(c) implies (a).</em> By <span style="color:#1971c2">[Corollary 5.4](cuts.md#box-5-mf-cor-weak)</span>.

    <em>Existence and equality.</em> The feasible region of the $\mathrm{MF}$ model is nonempty ($\vet{x}=\vet{0}$, $v=0$) and bounded ($0 \le x_{ij} \le u_{ij}$ and $|v| \le \sum_{(i,j) \in A} u_{ij}$), so the model has an optimal solution ([Chapter 15 «The geometry of Linear Programming»](https://fabiofurini.github.io/linear-programming/advanced-methods/15-geometry/)). For a maximum flow, (a) implies (c): some cut has capacity $\tilde{v}$, and by <span style="color:#1971c2">[Corollary 5.4](cuts.md#box-5-mf-cor-weak)</span> no cut has a smaller capacity. <span class="qed">□</span>

- The proof of (b) implies (c) is constructive: at a maximum flow, the nodes reachable from $s$ in the residual network form a minimum cut.

- A flow and a cut with $v=u(S,N \setminus S)$ certify each other: the cut proves that no flow is better, and the flow proves that no cut is smaller.

<a id="box-13-mf-ex-maxflow"></a>

!!! esempio "Example 5.5: the maximum flow of the reference network"

    On the reference network of <span style="color:#1971c2">[Example 5.1](the-maximum-flow-problem.md#box-2-mf-ex-ref)</span> the flow

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
    <td><span class="arithmatex">\(\tilde{x}_{ij}\)</span></td>
    <td><span class="arithmatex">\(3\)</span></td>
    <td><span class="arithmatex">\(4\)</span></td>
    <td><span class="arithmatex">\(3\)</span></td>
    <td><span class="arithmatex">\(0\)</span></td>
    <td><span class="arithmatex">\(4\)</span></td>
    <td><span class="arithmatex">\(0\)</span></td>
    <td><span class="arithmatex">\(4\)</span></td>
    <td><span class="arithmatex">\(1\)</span></td>
    <td><span class="arithmatex">\(3\)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">\(u_{ij}\)</span></td>
    <td><span class="arithmatex">\(5\)</span></td>
    <td><span class="arithmatex">\(4\)</span></td>
    <td><span class="arithmatex">\(3\)</span></td>
    <td><span class="arithmatex">\(2\)</span></td>
    <td><span class="arithmatex">\(4\)</span></td>
    <td><span class="arithmatex">\(2\)</span></td>
    <td><span class="arithmatex">\(4\)</span></td>
    <td><span class="arithmatex">\(2\)</span></td>
    <td><span class="arithmatex">\(3\)</span></td>
    </tr>
    </table></div>

    is feasible, with value $\tilde{x}_{12}+\tilde{x}_{13}=7$. For $S=\{1,2\}$ the forward arcs $(1,3)$, $(2,4)$ are saturated and the backward arc $(3,2)$ is empty, so

    $$
    u(S,N \setminus S)=u_{13}+u_{24}=4+3=7=v .
    $$

    By <span style="color:#1971c2">[Theorem 5.8](#box-12-mf-th-mfmc)</span>, $\tilde{\vet{x}}$ is a maximum flow, $\tilde{v}=7$, and $(\{1,2\},\{3,4,5,6\})$ is a minimum cut. In $G(\tilde{\vet{x}})$ the nodes reachable from $1$ are exactly $1$ and $2$. In the figure, $S$ is shaded and the forward arcs of the cut are green.

    ![Figure 4](../../img/maximum-flow/fig04.svg){ .fig loading=lazy  }

- <strong>Uniqueness.</strong> By <span style="color:#1971c2">[Corollary 5.4](cuts.md#box-5-mf-cor-weak)</span>, every maximum flow saturates the forward arcs and empties the backward arcs of each of the three minimum cuts of <span style="color:#1971c2">[Example 5.2](cuts.md#box-6-mf-ex-cuts)</span>:

    $$
    \begin{aligned}
    S=\{1,2\}: &\quad x_{13}=4,~ x_{24}=3,~ x_{32}=0,\\
    S=\{1,2,3\}: &\quad x_{35}=4,~ x_{43}=0,\\
    S=\{1,2,3,4,5\}: &\quad x_{46}=4,~ x_{56}=3.
    \end{aligned}
    $$

    Conservation at nodes $1$ and $4$ then gives $x_{12}=7-x_{13}=3$ and $x_{54}=x_{43}+x_{46}-x_{24}=1$: $\tilde{\vet{x}}$ is the unique maximum flow, while the minimum cut is not unique.

!!! attenzione "Saturated arcs and cuts"

    The saturated arcs of a maximum flow do not form a cut in general. Under $\tilde{\vet{x}}$ the saturated arcs are $(1,3)$, $(2,4)$, $(3,5)$, $(4,6)$, $(5,6)$, with total capacity $18$. A minimum cut is read from the nodes reachable from $s$ in the residual network.

!!! chiave ""

    A flow is maximum if and only if its residual network has no augmenting path, if and only if its value equals the capacity of a cut. The maximum value equals the minimum cut capacity, and the nodes reachable from $s$ in the residual network of a maximum flow form a minimum cut.

---

**Next:** [5.5 The Ford–Fulkerson algorithm](the-ford-fulkerson-algorithm.md)

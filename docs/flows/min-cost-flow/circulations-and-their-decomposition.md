---
title: "Circulations and their decomposition"
---

# 6.2 Circulations and their decomposition { #sez-sec-mc-decomposition }

<div class="info-capitolo" markdown>

**Part 3 · Flows · Chapter 6** · [:material-book-open-variant: Chapter 6: Minimum cost flow](index.md) · [:material-file-pdf-box: Lecture notes, volume 3 (PDF)](../../pdf/lecture-notes-3-flows.pdf) · [:material-pencil: Exercises: Minimum cost flow](../../exercises/min-cost-flow.md)

</div>

<a id="box-5-mc-def-circ"></a>

!!! definizione "Definition 6.4: circulation"

    Let $H=(N,F)$ be a directed graph. A <strong>circulation</strong> on $H$ is a vector $\vet{y} \in \R^{F}$ with $\vet{y} \ge \vet{0}$ such that every node has outflow equal to inflow:

    $$
    \sum_{(i,j) \in \delta^+(i)} y_{ij}=\sum_{(j,i) \in \delta^-(i)} y_{ji}, \qquad \forall i \in N .
    $$

    The <strong>incidence vector</strong> $\vet{\chi}^W$ of a directed cycle $W$ of $H$, with $\chi^W_a=1$ on the arcs of $W$ and $\chi^W_a=0$ elsewhere, is a circulation.

<a id="box-6-mc-lem-decomp"></a>

!!! teorema "Lemma 6.5: decomposition into cycles"

    Let $\vet{y} \neq \vet{0}$ be a circulation on $H=(N,F)$, with $p$ arcs where $y_a>0$. Then there are directed cycles $W_1,W_2,\dots,W_k$ of $H$, with $k \le p$, made of arcs with $y_a>0$, and numbers $\theta_1,\theta_2,\dots, \theta_k>0$ such that

    $$
    \vet{y}=\sum_{h=1}^{k} \theta_h\, \vet{\chi}^{W_h} .
    $$

    If $\vet{y}$ is integer, the numbers $\theta_h$ are integers.

??? dimostrazione "Proof"

    By induction on $p$.

    1. <em>A cycle.</em> Let $(i_0,i_1)$ be an arc with $y_{i_0i_1}>0$. Node $i_1$ receives a positive inflow, so by the balance some arc $(i_1,i_2)$ has $y_{i_1i_2}>0$. Going on in the same way we build a directed walk of arcs with $y>0$. Since $N$ is finite a node repeats, and the piece of the walk between its two occurrences is a directed cycle $W_1$.

    2. <em>Removing it.</em> Let $\theta_1=\min_{a \in W_1} y_a>0$. The vector $\vet{y}'=\vet{y}-\theta_1 \vet{\chi}^{W_1}$ is non-negative, it is balanced as a difference of balanced vectors, and it has at most $p-1$ positive arcs, since $y'_a=0$ on an arc of $W_1$ that attains the minimum.

    3. <em>Induction.</em> If $\vet{y}'=\vet{0}$, then $\vet{y}=\theta_1\vet{\chi}^{W_1}$. Otherwise the induction gives $\vet{y}'=\sum_{h=2}^{k}\theta_h\vet{\chi}^{W_h}$ with $k-1 \le p-1$ cycles of arcs with $y'_a>0$, hence $y_a>0$.

    If $\vet{y}$ is integer, $\theta_1$ is one of its entries and $\vet{y}'$ is integer, so all the $\theta_h$ are integers. <span class="qed">□</span>

<a id="box-7-mc-lem-diff"></a>

!!! teorema "Lemma 6.6: the difference of two feasible flows"

    Let $\vet{x}$ and $\vet{x}'$ be feasible flows. Define $\vet{y}$ on the arcs of $G(\vet{x})$: for every $(i,j) \in A$,

    $$
    \begin{aligned}
    y_{ij}&=x'_{ij}-x_{ij} && \text{on the forward arc } (i,j), \text{ if } x'_{ij}>x_{ij},\\
    y_{ji}&=x_{ij}-x'_{ij} && \text{on the backward arc } (j,i), \text{ if } x'_{ij}<x_{ij},
    \end{aligned}
    $$

    and $y=0$ on the other arcs of $G(\vet{x})$. Then $\vet{y}$ is a circulation on $G(\vet{x})$ with $y_{ij} \le r_{ij}$, and

    $$
    \vet{c}'\vet{x}'-\vet{c}'\vet{x}=\sum_{(i,j) \in A(\vet{x})} c^x_{ij}\, y_{ij}=\sum_{h=1}^{k}\theta_h\, c(W_h)
    $$

    for every decomposition $\vet{y}=\sum_{h=1}^{k}\theta_h\vet{\chi}^{W_h}$ into cycles of $G(\vet{x})$.

??? dimostrazione "Proof"

    We check that $\vet{y}$ lives on $G(\vet{x})$, that it is balanced, and its cost.

    1. If $x'_{ij}>x_{ij}$, then $x_{ij}<x'_{ij} \le u_{ij}$: the forward arc exists and $y_{ij} \le u_{ij}-x_{ij}= r_{ij}$. If $x'_{ij}<x_{ij}$, then $x_{ij}>x'_{ij} \ge l_{ij}$: the backward arc exists and $y_{ji} \le x_{ij}-l_{ij} =r_{ji}$.

    2. As in the proof of <span style="color:#1971c2">[Proposition 6.3](the-residual-network-with-costs.md#box-3-mc-prop-augment)</span>, $y$ on an arc $(i,k)$ of $G(\vet{x})$ adds $y$ to the outflow minus inflow of $i$ and subtracts it from that of $k$, exactly as the change from $\vet{x}$ to $\vet{x}'$ does on the corresponding arc of $A$. Hence the outflow minus inflow of $\vet{y}$ at node $i$ is $(\mat{B}\vet{x}')_i-(\mat{B}\vet{x})_i=b_i-b_i=0$.

    3. A forward arc contributes $c_{ij}(x'_{ij}-x_{ij})$, a backward arc $-c_{ij}(x_{ij}-x'_{ij})=c_{ij}(x'_{ij}- x_{ij})$: the total is $\vet{c}'(\vet{x}'-\vet{x})$. With the decomposition, $\sum c^x_{ij}y_{ij}=\sum_h \theta_h \sum_{(i,j) \in W_h} c^x_{ij}=\sum_h \theta_h\, c(W_h)$. <span class="qed">□</span>

- By <span style="color:#1971c2">[Lemma 6.5](#box-6-mc-lem-decomp)</span> such a decomposition exists: $\vet{x}'$ is $\vet{x}$ augmented along the cycles $W_1,W_2,\dots,W_k$ of $G(\vet{x})$ by $\theta_1,\theta_2,\dots,\theta_k$. Since $\vet{y}$ is positive on at most one arc of $G(\vet{x})$ per arc of $A$, $k \le m$.

<a id="box-8-mc-ex-decomp"></a>

!!! esempio "Example 6.2: from the most expensive flow to the optimal flow"

    We compare $\vet{x}^0$ of <span style="color:#1971c2">[Example 6.1](the-residual-network-with-costs.md#box-4-mc-ex-residual)</span>, of cost $80$, with the optimal flow $\tilde{\vet{x}}=(2,3,4,0,3,0,2,1,2)$ of Chapter 4, of cost $60$. The difference is

    $$
    \tilde{\vet{x}}-\vet{x}^0=(1,\,-1,\,0,\,-1,\,-1,\,-1,\,-1,\,-2,\,1),
    $$

    so $\vet{y}$ is positive on eight arcs of $G(\vet{x}^0)$: the forward arcs $(1,2)$ and $(5,6)$, with $y=1$, and the backward arcs

    $$
    y_{31}=1, \qquad y_{23}=1, \qquad y_{53}=1, \qquad y_{34}=1, \qquad y_{64}=1, \qquad y_{45}=2 .
    $$

    We follow the proof of <span style="color:#1971c2">[Lemma 6.5](#box-6-mc-lem-decomp)</span>, starting each time from the first arc with $y>0$ in lexicographic order and leaving every node along its arc with $y>0$ of smallest head:

    <div class="tabella" markdown="0"><table>
    <tr>
    <th><span class="arithmatex">\(h\)</span></th>
    <th>cycle <span class="arithmatex">\(W_h\)</span></th>
    <th><span class="arithmatex">\(\theta_h\)</span></th>
    <th><span class="arithmatex">\(c(W_h)\)</span></th>
    </tr>
    <tr>
    <td><span class="arithmatex">\(1\)</span></td>
    <td><span class="arithmatex">\(1,2,3,1\)</span></td>
    <td><span class="arithmatex">\(1\)</span></td>
    <td><span class="arithmatex">\(2-2-2=-2\)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">\(2\)</span></td>
    <td><span class="arithmatex">\(3,4,5,3\)</span></td>
    <td><span class="arithmatex">\(1\)</span></td>
    <td><span class="arithmatex">\(-3-5-3=-11\)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">\(3\)</span></td>
    <td><span class="arithmatex">\(4,5,6,4\)</span></td>
    <td><span class="arithmatex">\(1\)</span></td>
    <td><span class="arithmatex">\(-5+3-5=-7\)</span></td>
    </tr>
    </table></div>

    By <span style="color:#1971c2">[Lemma 6.6](#box-7-mc-lem-diff)</span>, $\vet{c}'\tilde{\vet{x}}-\vet{c}'\vet{x}^0=-2-11-7=-20=60-80$. All three cycles are negative, and $W_2$ is the cycle $4,5,3,4$ of <span style="color:#1971c2">[Example 6.1](the-residual-network-with-costs.md#box-4-mc-ex-residual)</span>, written from node $3$.

!!! chiave ""

    A circulation is a sum of positive multiples of directed cycles. The difference of two feasible flows is a circulation on $G(\vet{x})$: every feasible flow is reached from $\vet{x}$ along cycles of $G(\vet{x})$, and the cost changes by $\sum_h \theta_h\, c(W_h)$.

---

**Next:** [6.3 Negative cycle optimality conditions](negative-cycle-optimality-conditions.md)

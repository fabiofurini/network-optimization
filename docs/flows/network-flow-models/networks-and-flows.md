---
title: "Networks and flows"
---

# 4.1 Networks and flows { #sez-sec-nf-networks }

<div class="info-capitolo" markdown>

**Part 3 · Flows · Chapter 4** · [:material-book-open-variant: Chapter 4: Flow models](index.md) · [:material-file-pdf-box: Lecture notes, volume 3 (PDF)](../../pdf/lecture-notes-3-flows.pdf) · [:material-presentation: Slides](../../pdf/slides-network-flow-models.pdf) · [:material-pencil: Exercises: Flow models](../../exercises/network-flow-models.md)

</div>

<a id="box-1-nf-def-network"></a>

!!! definizione "Definition 4.1: network"

    A <strong>network</strong> is a directed graph $G=(N,A)$, with $n=|N|$ nodes and $m=|A|$ arcs, together with the following data.

    - Every node $i \in N$ has a <strong>balance</strong> $b_i \in \R$. The node is a <strong>supply node</strong> if $b_i>0$, a <strong>demand node</strong> if $b_i<0$, and a <strong>transshipment node</strong> if $b_i=0$.

    - Every arc $(i,j) \in A$ has a <strong>lower bound</strong> $l_{ij}$ and a <strong>capacity</strong> $u_{ij}$, with $0 \le l_{ij} \le u_{ij} \le +\infty$, and a <strong>cost</strong> $c_{ij} \in \R$ per unit of flow.

    When the lower bounds are not given, $l_{ij}=0$ for every arc.

<a id="box-2-nf-def-flow"></a>

!!! definizione "Definition 4.2: flow"

    Let $G=(N,A)$ be a network. A <strong>flow</strong> is a vector $\vet{x} \in \R^m$ with one entry $x_{ij}$, the amount sent along the arc, for every $(i,j) \in A$.

    - The flow satisfies the <strong>flow conservation</strong> constraint of node $i$ if what leaves $i$ minus what enters $i$ equals the balance:

        $$
        \sum_{(i,j) \in \delta^+(i)} x_{ij} \;-\; \sum_{(j,i) \in \delta^-(i)} x_{ji} = b_i .
        $$

    - The flow is <strong>feasible</strong> if it satisfies flow conservation at every node and $l_{ij} \le x_{ij} \le u_{ij}$ for every arc. Its <strong>cost</strong> is $\sum_{(i,j) \in A} c_{ij}\, x_{ij}$.

- A supply node sends out $b_i$ units more than it receives, a demand node receives $-b_i$ units more than it sends, and a transshipment node passes on everything it receives.

- With the node–arc incidence matrix $\mat{B}$ of [Chapter 1 «Graphs»](https://fabiofurini.github.io/network-optimization/graphs/graphs/), flow conservation at all the nodes reads $\mat{B}\vet{x}=\vet{b}$: row $i$ of $\mat{B}\vet{x}$ is the outflow minus the inflow of $i$.

<a id="box-3-nf-ex-ref"></a>

!!! esempio "Example 4.1: the reference network"

    We add data to the reference graph of [Chapter 1 «Graphs»](https://fabiofurini.github.io/network-optimization/graphs/graphs/), with the arcs numbered $a_1,a_2,\dots,a_9$ in lexicographic order. The balances are

    $$
    b_1=5,\qquad b_2=2,\qquad b_3=0,\qquad b_4=-3,\qquad b_5=0,\qquad b_6=-4,
    $$

    so nodes $1$ and $2$ supply $7$ units, nodes $4$ and $6$ demand them, and nodes $3$ and $5$ are transshipment nodes. The lower bounds are zero, and the costs and capacities are:

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
    <td><span class="arithmatex">\(c_{ij}\)</span></td>
    <td><span class="arithmatex">\(2\)</span></td>
    <td><span class="arithmatex">\(2\)</span></td>
    <td><span class="arithmatex">\(5\)</span></td>
    <td><span class="arithmatex">\(2\)</span></td>
    <td><span class="arithmatex">\(3\)</span></td>
    <td><span class="arithmatex">\(3\)</span></td>
    <td><span class="arithmatex">\(5\)</span></td>
    <td><span class="arithmatex">\(5\)</span></td>
    <td><span class="arithmatex">\(3\)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">\(u_{ij}\)</span></td>
    <td><span class="arithmatex">\(4\)</span></td>
    <td><span class="arithmatex">\(4\)</span></td>
    <td><span class="arithmatex">\(4\)</span></td>
    <td><span class="arithmatex">\(2\)</span></td>
    <td><span class="arithmatex">\(4\)</span></td>
    <td><span class="arithmatex">\(3\)</span></td>
    <td><span class="arithmatex">\(5\)</span></td>
    <td><span class="arithmatex">\(3\)</span></td>
    <td><span class="arithmatex">\(2\)</span></td>
    </tr>
    </table></div>

    In the figure each arc carries the pair $c_{ij},u_{ij}$, and each node its balance $b_i$ (in blue).

    ![Figure 1](../../img/network-flow-models/fig01.svg){ .fig loading=lazy  }

    The flow $\bar{\vet{x}}$ with

    $$
    \bar{x}_{12}=1,~ \bar{x}_{13}=4,~ \bar{x}_{24}=3,~ \bar{x}_{32}=0,~ \bar{x}_{35}=4,~ \bar{x}_{43}=0,~
    \bar{x}_{46}=2,~ \bar{x}_{54}=2,~ \bar{x}_{56}=2
    $$

    is feasible. For example, at node $4$ the outflow is $\bar{x}_{43}+\bar{x}_{46}=2$, the inflow is $\bar{x}_{24}+\bar{x}_{54}=5$, and $2-5=-3=b_4$. The arcs $(1,3)$, $(3,5)$ and $(5,6)$ are at capacity, and the cost of $\bar{\vet{x}}$ is $63$.

## 4.1.1 Flow across a cut

- For a set of nodes $S \subseteq N$, we denote by $\delta^+(S)$ the arcs with the tail in $S$ and the head outside $S$, by $\delta^-(S)$ the arcs with the head in $S$ and the tail outside $S$, and $x(F)=\sum_{(i,j) \in F} x_{ij}$ for a set of arcs $F$.

<a id="box-4-nf-lem-cut"></a>

!!! teorema "Lemma 4.3: flow across a cut"

    Let $\vet{x}$ satisfy flow conservation at every node of a network $G=(N,A)$. Then, for every $S \subseteq N$,

    $$
    x(\delta^+(S))-x(\delta^-(S))=\sum_{i \in S} b_i .
    $$

??? dimostrazione "Proof"

    Add up the conservation constraints of the nodes of $S$; the right-hand side is $\sum_{i \in S} b_i$.

    - An arc with both endpoints in $S$ appears twice, with $+x_{ij}$ in the row of its tail and $-x_{ij}$ in the row of its head: it cancels.

    - An arc of $\delta^+(S)$ appears only in the row of its tail, with $+x_{ij}$; an arc of $\delta^-(S)$ only in the row of its head, with $-x_{ij}$; the other arcs do not appear.

    <p class="qed-riga"><span class="qed">□</span></p>

- In <span style="color:#1971c2">[Example 4.1](#box-3-nf-ex-ref)</span>, the set $S=\{1,2,3\}$ has $\delta^+(S)=\{(2,4),(3,5)\}$ and $\delta^-(S)=\{(4,3)\}$. The flow $\bar{\vet{x}}$ gives $3+4-0=7=b_1+b_2+b_3$.

!!! chiave ""

    A network has balances on the nodes and lower bounds, capacities and costs on the arcs. A feasible flow satisfies $\mat{B}\vet{x}=\vet{b}$ and the bounds; across every cut, the net outflow equals the total balance of the nodes inside.

---

**Next:** [4.2 The minimum cost flow model](the-minimum-cost-flow-model.md)

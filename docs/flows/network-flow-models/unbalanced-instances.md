---
title: "Unbalanced instances"
---

# 4.5 Unbalanced instances { #sez-sec-nf-dummy }

<div class="info-capitolo" markdown>

**Part 3 · Flows · Chapter 4** · [:material-book-open-variant: Chapter 4: Flow models](index.md) · [:material-file-pdf-box: Lecture notes, volume 3 (PDF)](../../pdf/lecture-notes-3-flows.pdf) · [:material-pencil: Exercises: Flow models](../../exercises/network-flow-models.md)

</div>

<a id="box-14-nf-def-unbalanced"></a>

!!! definizione "Definition 4.10: unbalanced instance"

    An instance with $\sum_{i \in N} b_i>0$ is <strong>unbalanced</strong>: the total supply exceeds the total demand. Every demand must be met, and every supply node $i$ sends out <em>at most</em> $b_i$ units:

    $$
    \sum_{(i,j) \in \delta^+(i)} x_{ij} - \sum_{(j,i) \in \delta^-(i)} x_{ji} \;\le\; b_i \quad \forall i \in N:\, b_i>0,
    \qquad\quad = b_i \quad \forall i \in N:\, b_i \le 0,
    $$

    with the bounds $l_{ij} \le x_{ij} \le u_{ij}$ and the objective $\min \sum_{(i,j) \in A} c_{ij}\,x_{ij}$.

<a id="box-15-nf-def-dummy"></a>

!!! definizione "Definition 4.11: dummy node"

    Let $P=\{i \in N : b_i>0\}$ be the supply nodes and $e=\sum_{i \in N} b_i>0$ the excess. The <strong>balanced network</strong> adds a <strong>dummy node</strong> $d$ with balance $b_d=-e$, and an arc $(i,d)$ for every $i \in P$ with $l_{id}=0$, $u_{id}=+\infty$ and $c_{id}=0$.

<a id="box-16-nf-prop-dummy"></a>

!!! teorema "Proposition 4.12: the dummy node"

    The feasible solutions of the unbalanced instance and the feasible flows of the balanced network correspond, with the same cost: a flow of the balanced network restricted to $A$ is feasible for the unbalanced instance, and a solution of the unbalanced instance becomes a feasible flow with $x_{id}=b_i-(\text{outflow}-\text{inflow of } i)$.

??? dimostrazione "Proof"

    For a vector $\vet{x}$ on $A$, let $s_i(\vet{x})$ be the outflow minus the inflow of node $i$ along the arcs of $A$.

    1. Let $(\vet{x},(x_{id})_{i \in P})$ be feasible for the balanced network. At $i \in P$ conservation reads $s_i(\vet{x})+x_{id}=b_i$ with $x_{id} \ge 0$, so $s_i(\vet{x}) \le b_i$; at the other nodes of $N$ it reads $s_i(\vet{x})=b_i$.

    2. Conversely, let $\vet{x}$ be feasible for the unbalanced instance, and set $x_{id}=b_i-s_i(\vet{x}) \ge 0$ for $i \in P$. Conservation holds at every node of $N$, and at $d$ the inflow is

        $$
        \sum_{i \in P} x_{id}=\sum_{i \in P} b_i-\sum_{i \in N} s_i(\vet{x})+\sum_{i \notin P} s_i(\vet{x})
        =\sum_{i \in P} b_i - 0+\sum_{i \notin P} b_i=e,
        $$

        since the values $s_i(\vet{x})$ add up to zero: every arc of $A$ contributes $+x_{ij}$ to its tail and $-x_{ij}$ to its head. Hence $d$ receives exactly $-b_d=e$ units.

    The dummy arcs cost zero, so the two costs coincide. <span class="qed">□</span>

- The flow on $(i,d)$ is the part of the supply of $i$ that is not used.

- If the total demand exceeds the total supply and the demands are upper limits, a dummy node $d$ with balance $b_d=-\sum_{i \in N} b_i$ and arcs $(d,j)$ to the demand nodes balances the network in the same way.

<a id="box-17-nf-ex-dummy"></a>

!!! esempio "Example 4.5: a dummy node on the reference network"

    In the network of <span style="color:#1971c2">[Example 4.1](networks-and-flows.md#box-3-nf-ex-ref)</span> we raise the supply of node $2$ to $b_2=4$. The total supply is $9$, the total demand is $7$, and the excess is $e=2$.

    - The balanced network adds node $7$ with $b_7=-2$, and the arcs $(1,7)$ and $(2,7)$ with cost $0$ and capacity $+\infty$ (dashed in the figure).

    - Its optimal flow, computed with Gurobi, ships all the $4$ units of node $2$ and only $3$ units of node $1$: $x_{17}=2$, $x_{27}=0$, with optimal value $56$.

    ![Figure 2](../../img/network-flow-models/fig02.svg){ .fig loading=lazy  }

!!! chiave ""

    An unbalanced instance becomes a balanced network with a dummy node that absorbs the excess through zero-cost arcs; the flow on a dummy arc is the unused supply of its tail.

---

**Next:** [4.6 Total unimodularity and integrality](total-unimodularity-and-integrality.md)

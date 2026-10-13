---
title: "The minimum cost flow model"
---

# 4.2 The minimum cost flow model { #sez-sec-nf-model }

<div class="info-capitolo" markdown>

**Part 3 · Flows · Chapter 4** · [:material-book-open-variant: Chapter 4: Flow models](index.md) · [:material-file-pdf-box: Lecture notes, volume 3 (PDF)](../../pdf/lecture-notes-3-flows.pdf) · [:material-pencil: Exercises: Flow models](../../exercises/network-flow-models.md)

</div>

<a id="box-5-nf-def-mcf"></a>

!!! definizione "Definition 4.4: minimum cost flow problem"

    Given a network $G=(N,A)$ with balances $b_i$, lower bounds $l_{ij}$, capacities $u_{ij}$ and costs $c_{ij}$, the <strong>minimum cost flow problem</strong> asks for a feasible flow of minimum cost.

- We use one continuous variable $x_{ij}$ for every arc $(i,j) \in A$, the flow on the arc.

!!! chiave ""

    Using these variables, a Linear Programming (LP) model for the minimum cost flow problem reads as follows:

    <a id="eq-nf-MCF"></a>

    \begin{align*}
    &&   \min \;\;{\sum_{(i,j) \in A} c_{ij} \, x_{ij}}                                      \label{nf:obj}  \tag{4.1a}\\[1ex]
    && \text{subject to} \quad  \sum_{(i,j) \in \delta^+(i)} x_{ij} - \sum_{(j,i) \in \delta^-(i)} x_{ji}
    &= b_i, & \forall i \in N,                                                       \label{nf:cons}  \tag{4.1b}\\[1ex]
    && l_{ij} \le x_{ij} &\le u_{ij}, & \forall (i,j) \in A.                          \label{nf:bounds} \tag{4.1c}
    \end{align*}

    This LP model is referred to as the $\mathrm{MCF}$ model.

- Description of the objective function and constraints of the $\mathrm{MCF}$ model:

    - the linear objective function $\eqref{nf:obj}$ minimizes the total cost of the flow;

    - constraints $\eqref{nf:cons}$ are the flow conservation constraints, one for every node;

    - finally, constraints $\eqref{nf:bounds}$ impose the lower bound and the capacity of every arc.

- With the node–arc incidence matrix $\mat{B}$, the vector $\vet{c}$ of the costs and the vectors $\vet{l}$, $\vet{u}$ of the bounds, the $\mathrm{MCF}$ model is

    $$
    \min \;\big\{\, \vet{c}' \vet{x} \;:\; \mat{B}\vet{x}=\vet{b},~ \vet{l} \le \vet{x} \le \vet{u} \,\big\}.
    $$

- The model has $m$ variables and $n$ equations. The column of $x_{ij}$ in $\mat{B}$ has only two nonzero entries, $+1$ in row $i$ and $-1$ in row $j$: this structure gives all the properties of this chapter.

<a id="box-6-nf-ex-model"></a>

!!! esempio "Example 4.2: the $\mathrm{MCF}$ model of the reference network"

    For the network of <span style="color:#1971c2">[Example 4.1](networks-and-flows.md#box-3-nf-ex-ref)</span> the $\mathrm{MCF}$ model has $9$ variables and $6$ equations:

    $\begin{array}{rrrrrrrrrrcr} \min & 2x_{12} & +2x_{13} & +5x_{24} & +2x_{32} & +3x_{35} & +3x_{43} & +5x_{46} & +5x_{54} & +3x_{56} & & \\[1ex] \text{subject to} & x_{12} & +x_{13} & & & & & & & & = & 5\\ & -x_{12} & & +x_{24} & -x_{32} & & & & & & = & 2\\ & & -x_{13} & & +x_{32} & +x_{35} & -x_{43} & & & & = & 0\\ & & & -x_{24} & & & +x_{43} & +x_{46} & -x_{54} & & = & -3\\ & & & & & -x_{35} & & & +x_{54} & +x_{56} & = & 0\\ & & & & & & & -x_{46} & & -x_{56} & = & -4 \end{array}$

    together with $0 \le x_{12} \le 4$, $0 \le x_{13} \le 4$, $0 \le x_{24} \le 4$, $0 \le x_{32} \le 2$, $0 \le x_{35} \le 4$, $0 \le x_{43} \le 3$, $0 \le x_{46} \le 5$, $0 \le x_{54} \le 3$, $0 \le x_{56} \le 2$. The coefficient matrix of the equations is the incidence matrix $\mat{B}$ of the reference graph.

!!! chiave ""

    The minimum cost flow problem is the LP $\min\{\vet{c}'\vet{x} : \mat{B}\vet{x}=\vet{b},~\vet{l} \le \vet{x} \le \vet{u}\}$: one variable per arc, one conservation equation per node.

---

**Next:** [4.3 Feasibility conditions](feasibility-conditions.md)

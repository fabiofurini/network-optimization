---
title: "The linear programming formulation"
---

# 3.3 The linear programming formulation { #sez-sec-sp-lp }

<div class="info-capitolo" markdown>

**Part 2 · Trees and paths · Chapter 3** · [:material-book-open-variant: Chapter 3: Shortest paths](index.md) · [:material-file-pdf-box: Lecture notes, volume 2 (PDF)](../../pdf/lecture-notes-2-trees-and-paths.pdf) · [:material-pencil: Exercises: Shortest paths](../../exercises/shortest-paths.md) · [:material-gesture-tap: App: Shortest paths: Dijkstra, Bellman–Ford, acyclic graphs](../../lab/shortest-paths-dijkstra-bellman-ford.md)

</div>

- A path from $s$ to $t$ sends one unit of flow from $s$ to $t$. We use a variable $x_{ij} \ge 0$ for every arc, the flow on the arc, and the <strong>balances</strong>

    $$
    b_s=1, \qquad b_t=-1, \qquad b_i=0, \quad \forall i \in N \setminus \{s,t\}.
    $$

!!! chiave ""

    Using these variables, an LP model for the $s$–$t$ shortest path problem reads as follows:

    <a id="eq-SP_ST"></a>

    \begin{align*}
    &&   \min \;\;{\sum_{(i,j) \in A} d_{ij} \, x_{ij}}                                     \label{obj_SP}  \tag{3.1a}\\[1ex]
    && \text{subject to} \quad  {\sum_{(i,j) \in \delta^+(i)} x_{ij} \;-\; \sum_{(j,i) \in \delta^-(i)} x_{ji}}
    &= b_i, & \forall i \in N,                                                           \label{cons1_SP}  \tag{3.1b}\\[1ex]
    &&x_{ij}                        &\ge  0, & \forall (i,j) \in A.                    \label{cons2_SP} \tag{3.1c}
    \end{align*}

    This LP model is referred to as the $\mathrm{SP}(s,t)$ model.

- Description of the objective function and constraints of the $\mathrm{SP}(s,t)$ model:

    - the objective function $\eqref{obj_SP}$ minimizes the total length of the flow;

    - constraints $\eqref{cons1_SP}$ are the flow conservation constraints: one unit leaves $s$, one unit enters $t$, and every other node sends out what it receives;

    - finally, constraints $\eqref{cons2_SP}$ define the variables of the LP model.

- In matrix form the model is $\min\{\vet{d}'\vet{x} : \mat{B}\vet{x}=\vet{b},\ \vet{x} \ge \vet{0}\}$, with the node–arc incidence matrix $\mat{B}$ of [Chapter 1](https://fabiofurini.github.io/network-optimization/graphs/graphs/representations-of-a-graph/): $+1$ in the tail and $-1$ in the head of every arc.

- The <strong>incidence vector</strong> $\vet{x}^P$ of a path $P$ from $s$ to $t$, with $x^P_{ij}=1$ on the arcs of $P$ and $0$ elsewhere, is feasible, and its value is $d(P)$.

## 3.3.1 The dual model and the potentials

- The constraint of node $i$ is an equation, so its dual variable $\pi_i$ is free. The column of $x_{ij}$ in $\mat{B}$ has $+1$ in row $i$ and $-1$ in row $j$, so the dual constraint of $x_{ij} \ge 0$ is $\pi_i-\pi_j \le d_{ij}$ ([Linear Programming, Chapter 9 «Duality theory»](https://fabiofurini.github.io/linear-programming/duality/09-duality/)).

!!! chiave ""

    Using a free dual variable $\pi_i$ for each constraint $\eqref{cons1_SP}$, the dual model of the $\mathrm{SP}(s,t)$ model is:

    <a id="eq-DUAL_SP"></a>

    \begin{align*}
    &&   \max \;\; \pi_s-\pi_t                                                    \label{obj_DSP}  \tag{3.2a}\\[2ex]
    && \text{subject to} \quad  \pi_i-\pi_j  &\le d_{ij}, & \forall (i,j) \in A,          \label{cons1_DSP}  \tag{3.2b}\\[2ex]
    &&\pi_i                        &\in \R, & \forall i \in N.                           \label{cons2_DSP} \tag{3.2c}
    \end{align*}

- Constraint $\eqref{cons1_DSP}$ is $\bar{c}_{ij}=d_{ij}-\pi_i+\pi_j \ge 0$: the feasible solutions of the dual are the feasible potentials of <span style="color:#1971c2">[Definition 3.7](optimality-conditions-and-potentials.md#box-10-sp-def-potentials)</span>, and $\bar{c}_{ij}$ is the reduced cost of $x_{ij}$ in the LP sense.

<a id="box-14-sp-th-lp"></a>

!!! teorema "Theorem 3.10: LP and shortest paths"

    Under (A1) and (A2), the $\mathrm{SP}(s,t)$ model has an optimal solution and $z(\mathrm{SP}(s,t))=\tilde{d}(t)$. The incidence vector of a shortest path from $s$ to $t$ is optimal for $\mathrm{SP}(s,t)$, and the potentials $\pi_i=-\tilde{d}(i)$ are optimal for $D(\mathrm{SP}(s,t))$.

??? dimostrazione "Proof"

    Let $P$ be a shortest path from $s$ to $t$, which exists by (A1).

    1. $\vet{x}^P$ is feasible for $\mathrm{SP}(s,t)$, with value $d(P)=\tilde{d}(t)$.

    2. By <span style="color:#1971c2">[Theorem 3.5](shortest-path-problems.md#box-7-sp-th-bellman)</span>, $\tilde{d}(j) \le \tilde{d}(i)+d_{ij}$ for every arc, so $\pi_i=-\tilde{d}(i)$ satisfies $\pi_i-\pi_j \le d_{ij}$; its value is $\pi_s-\pi_t=0+\tilde{d}(t)$.

    3. A feasible primal and a feasible dual solution with the same value are both optimal, by weak duality. <span class="qed">□</span>

<a id="box-15-sp-prop-unbounded"></a>

!!! teorema "Proposition 3.11: a negative cycle makes the model unbounded"

    If $\mathrm{SP}(s,t)$ is feasible and $G$ has a negative cycle $C$, reachable from $s$ or not, then $\mathrm{SP}(s,t)$ is unbounded.

??? dimostrazione "Proof"

    Let $\bar{\vet{x}}$ be feasible and let $\vet{x}^C$ be the incidence vector of $C$. The columns of the arcs of $C$ add up to zero ([Chapter 1, Lemma «columns of a cycle»](https://fabiofurini.github.io/network-optimization/graphs/graphs/the-rank-of-the-incidence-matrix/)), so $\mat{B}\vet{x}^C=\vet{0}$. For every $\lambda \ge 0$ the vector $\bar{\vet{x}}+\lambda\vet{x}^C$ is feasible, with value $\vet{d}'\bar{\vet{x}}+\lambda\, d(C)$, which tends to $-\infty$. <span class="qed">□</span>

!!! attenzione "The sign of the potentials"

    With the incidence matrix of the course ($+1$ in the tail) the dual constraint is $\pi_i-\pi_j \le d_{ij}$, and the optimal potentials are $\pi_i=-\tilde{d}(i)$, up to an additive constant. The form $\pi_j-\pi_i \le d_{ij}$, with $\pi_i=\tilde{d}(i)$, belongs to the opposite sign convention ($-1$ in the tail).

## 3.3.2 The single-source model

- To find a shortest path from $s$ to every node, $s$ sends one unit to each of the other $n-1$ nodes:

    $$
    b_s=n-1, \qquad b_i=-1, \quad \forall i \in N \setminus \{s\}.
    $$

    With these balances the model [(3.1)](#eq-SP_ST) is called $\mathrm{SP}(s)$; its dual maximizes $(n-1)\pi_s-\sum_{i \neq s}\pi_i$ under the same constraints $\eqref{cons1_DSP}$.

<a id="box-16-sp-prop-single"></a>

!!! teorema "Proposition 3.12: the single-source model"

    Under (A1) and (A2), let $T$ be a shortest path tree and, for every $j \neq s$, let $T_j$ be the set of the nodes whose tree path passes through $j$ ($j$ included). The flow with $x_{ij}=|T_j|$ on the arcs $(i,j)$ of $T$ and $0$ elsewhere is optimal for $\mathrm{SP}(s)$, the potentials $\pi_i=-\tilde{d}(i)$ are optimal for its dual, and

    $$
    z(\mathrm{SP}(s))=\sum_{j \in N}\tilde{d}(j).
    $$

??? dimostrazione "Proof"

    1. <em>Feasibility.</em> At a node $j \neq s$ the flow entering on the tree arc is $|T_j|$, and the flow leaving is $\sum |T_h|$ over the tree arcs $(j,h)$, that is $|T_j|-1$: the balance is $-1$. At $s$ the leaving flow covers all the other nodes: $n-1$.

    2. <em>Value.</em> The flow is the sum of the incidence vectors of the $n-1$ tree paths, since the arc $(i,j)$ lies on the tree paths of the $|T_j|$ nodes of $T_j$. Its value is $\sum_{j}\tilde{d}(j)$.

    3. <em>Dual.</em> $\pi_i=-\tilde{d}(i)$ is feasible as in <span style="color:#1971c2">[Theorem 3.10](#box-14-sp-th-lp)</span>, with value $(n-1)\cdot 0+\sum_{i \neq s}\tilde{d}(i)$. By weak duality both solutions are optimal. <span class="qed">□</span>

- In [Chapter 4 «Network flow models»](https://fabiofurini.github.io/network-optimization/flows/network-flow-models/) the vertices of these polyhedra are shown to be integral, by the total unimodularity of $\mat{B}$.

<a id="box-17-sp-ex-lp"></a>

!!! esempio "Example 3.5: the LP models on the reference graph"

    We solve the models with the lengths of <span style="color:#1971c2">[Example 3.1](shortest-path-problems.md#box-2-sp-ex-ref)</span>, $s=1$ and $t=6$ (values checked with Gurobi).

    - $\mathrm{SP}(1,6)$: $z(\mathrm{SP}(1,6))=13$, with $x_{13}=x_{32}=x_{24}=x_{46}=1$ and all other variables $0$: the path $1,3,2,4,6$. The dual value is $\pi_1-\pi_6=13$.

    - $\mathrm{SP}(1)$: $z(\mathrm{SP}(1))=0+5+2+8+10+13=38$, with the flows on the shortest path tree

        $$
        x_{13}=5, \qquad x_{32}=3, \qquad x_{24}=2, \qquad x_{46}=1, \qquad x_{35}=1 .
        $$

        For example $T_3=\{2,3,4,5,6\}$, so $x_{13}=5$; the cost is $2\cdot 5+3\cdot 3+3\cdot 2+5+8=38$. The optimal duals, normalized with $\pi_1=0$, are $\vet{\pi}=(0,-5,-2,-8,-10,-13)$.

    - With the lengths $d''$ of <span style="color:#1971c2">[Example 3.2](shortest-path-problems.md#box-5-sp-ex-negcycle)</span> the model $\mathrm{SP}(1,6)$ is unbounded: each unit of flow around the cycle $3,5,4,3$ lowers the value by $1$.

!!! chiave ""

    A shortest path is a unit flow from $s$ to $t$: $\min \vet{d}'\vet{x}$ with $\mat{B}\vet{x}=\vet{b}$, $\vet{x} \ge \vet{0}$. Its dual has the constraints $\pi_i-\pi_j \le d_{ij}$, and $\pi_i=-\tilde{d}(i)$ is optimal; a negative cycle anywhere in $G$ makes the model unbounded.

---

**Next:** [3.4 Shortest paths in acyclic graphs](shortest-paths-in-acyclic-graphs.md)

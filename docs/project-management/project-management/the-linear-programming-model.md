---
title: "The linear programming model"
---

# 9.7 The linear programming model { #sez-pm-sec-lp }

<div class="info-capitolo" markdown>

**Part 5 · Project management · Chapter 9** · [:material-book-open-variant: Chapter 9: Project management](index.md) · [:material-file-pdf-box: Lecture notes, volume 5 (PDF)](../../pdf/lecture-notes-5-project-management.pdf) · [:material-pencil: Exercises: Project management](../../exercises/project-management.md)

</div>

- The minimum project duration is the optimal value of an LP model whose variables are the start times. We use $n+2$ free variables, one for every node:

    $$
    t_j=\text{start time of node } j, \qquad \forall j \in N .
    $$

!!! chiave ""

    Using these variables, an LP model for the minimum project duration reads as follows:

    <a id="eq-pm-PD"></a>

    \begin{align*}
    &&   \min \;\; t_{n+1}-t_0                                                               \label{pm:obj}  \tag{9.1a}\\[1ex]
    && \text{subject to} \quad  t_j-t_i &\ge d_i, & \forall (i,j) \in A,                 \label{pm:cons}  \tag{9.1b}\\[1ex]
    && t_i &\in \R, & \forall i \in N.                                                  \label{pm:dom} \tag{9.1c}
    \end{align*}

    This LP model is referred to as the $\mathrm{PD}$ model.

- Description of the objective function and constraints of the $\mathrm{PD}$ model:

    - the objective function $\eqref{pm:obj}$ minimizes the time from the start of the project to FINISH;

    - constraints $\eqref{pm:cons}$ make every node start after each of its immediate predecessors is finished;

    - finally, constraints $\eqref{pm:dom}$ define the variables of the LP model, which are free.

- Adding the same constant to all the start times keeps the constraints and the value: the schedules are the feasible solutions with $t_0=0$, and $z(\mathrm{PD})=T$.

## 9.7.1 The dual model: a longest path

- Following the rules of [Chapter 9 «Duality theory»](https://fabiofurini.github.io/linear-programming/duality/09-duality/) of the module Linear Programming, we use a dual variable $x_{ij} \ge 0$ for every constraint $\eqref{pm:cons}$, a $\ge$ constraint of a minimization model. Every free variable $t_i$ gives a dual equation, whose right-hand side is the coefficient of $t_i$ in the objective function.

- The variable $t_i$ has coefficient $+1$ in the constraints of the arcs entering $i$ and $-1$ in those of the arcs leaving $i$. With the balances

    $$
    b_0=1, \qquad b_{n+1}=-1, \qquad b_i=0, \quad \forall i \in N \setminus \{0,n+1\},
    $$

    the equation of $t_i$, multiplied by $-1$, is a flow conservation constraint.

!!! chiave ""

    Using a non-negative dual variable $x_{ij}$ for each constraint $\eqref{pm:cons}$, the dual model of the $\mathrm{PD}$ model is:

    <a id="eq-pm-DPD"></a>

    \begin{align*}
    &&   \max \;\; \sum_{(i,j) \in A} d_i\, x_{ij}                                              \label{pm:dobj}  \tag{9.2a}\\[1ex]
    && \text{subject to} \quad  \sum_{(i,j) \in \delta^+(i)} x_{ij}-\sum_{(j,i) \in \delta^-(i)} x_{ji}
    &= b_i, & \forall i \in N,                                                             \label{pm:dcons}  \tag{9.2b}\\[1ex]
    && x_{ij} &\ge 0, & \forall (i,j) \in A.                                                \label{pm:ddom} \tag{9.2c}
    \end{align*}

    This LP model is referred to as the $D(\mathrm{PD})$ model.

- Description of the dual model:

    - constraints $\eqref{pm:dcons}$ send one unit of flow from START to FINISH;

    - the objective function $\eqref{pm:dobj}$ maximizes the length of the flow, with length $d_i$ on the arc $(i,j)$: the incidence vector of a path $P$ from START to FINISH is feasible, with value $L(P)$.

- With the lengths $-d_i$, the $D(\mathrm{PD})$ model is the model $\mathrm{SP}(0,n+1)$ of [Chapter 3](https://fabiofurini.github.io/network-optimization/trees-and-paths/shortest-paths/the-linear-programming-formulation/) with the objective multiplied by $-1$, and the $\mathrm{PD}$ model is its dual: the start times are the potentials, $\pi_i=t_i$.

- The reduced cost of the arc $(i,j)$ is then $\bar{c}_{ij}=-d_i-t_i+t_j$. With $\vet{t}=\mathit{ES}$ it is $\bar{c}_{ij}=\mathit{ES}_j-\mathit{EF}_i \ge 0$: the tight arcs are the arcs with reduced cost zero, and <span style="color:#1971c2">[Theorem 9.15](slacks-and-critical-activities.md#box-19-pm-th-tight)</span> is the certificate of [Chapter 3](https://fabiofurini.github.io/network-optimization/trees-and-paths/shortest-paths/optimality-conditions-and-potentials/), feasible potentials and a path of arcs with reduced cost zero.

<a id="box-24-pm-th-lp"></a>

!!! teorema "Theorem 9.18: LP models and critical paths"

    $z(\mathrm{PD})=z(D(\mathrm{PD}))=T$. The schedules $\mathit{ES}$ and $\mathit{LS}$ are optimal for the $\mathrm{PD}$ model, and the incidence vector of every critical path is optimal for the $D(\mathrm{PD})$ model. Moreover, every optimal solution of the $\mathrm{PD}$ model satisfies $t_j=t_i+d_i$ on every arc $(i,j)$ of every critical path.

??? dimostrazione "Proof"

    1. $\mathit{ES}$ and $\mathit{LS}$ are feasible for the $\mathrm{PD}$ model, with value $T-0=T$, by <span style="color:#1971c2">[Theorem 9.8](the-forward-pass-earliest-times.md#box-10-pm-th-earliest)</span> and <span style="color:#1971c2">[Theorem 9.11](the-backward-pass-latest-times.md#box-14-pm-th-latest)</span>.

    2. Let $P$ be a critical path and $\vet{x}^P$ its incidence vector, with $x^P_{ij}=1$ on the arcs of $P$ and $0$ elsewhere. One unit leaves START, one unit enters FINISH, and every other node of $P$ has one entering and one leaving arc of $P$: $\vet{x}^P$ is feasible for the $D(\mathrm{PD})$ model, with value $L(P)=T$.

    3. A feasible solution of the $\mathrm{PD}$ model and a feasible solution of its dual with the same value are both optimal, by weak duality.

    4. Let $\vet{t}$ be optimal for the $\mathrm{PD}$ model, and $P=i_0,i_1,\dots,i_k$ a critical path. Adding up the constraints of its arcs,

        $$
        T=t_{n+1}-t_0=\sum_{s=0}^{k-1} \big(t_{i_{s+1}}-t_{i_s}\big) \ge \sum_{s=0}^{k-1} d_{i_s}=L(P)=T,
        $$

        so every constraint of an arc of $P$ holds with equality.

    <p class="qed-riga"><span class="qed">□</span></p>

- In every schedule of minimum duration the critical activities start at their earliest start times, which equal their latest start times.

<a id="box-25-pm-ex-lp"></a>

!!! esempio "Example 9.7: the LP models of the case study"

    For the case study the $\mathrm{PD}$ model has $16$ variables and $19$ constraints; for example, the constraint of the arc $(5,8)$ is $t_8-t_5 \ge 4$. Solved with Gurobi:

    - $z(\mathrm{PD})=z(D(\mathrm{PD}))=44$, and the optimal dual solution returned by Gurobi is the incidence vector of the critical path START$,1,2,3,5,6,10,12,14,$FINISH;

    - the optimal solution of the $\mathrm{PD}$ model is not unique: $\mathit{ES}$ and $\mathit{LS}$ are both optimal, and they differ, for example, on activity $4$, with $\mathit{ES}_4=16$ and $\mathit{LS}_4=20$;

    - with $\vet{t}=\mathit{ES}$ the reduced costs $\bar{c}_{ij}=\mathit{ES}_j-\mathit{EF}_i$ are zero on every arc except $\bar{c}_{58}=9$, $\bar{c}_{9,10}=2$, $\bar{c}_{11,14}=1$ and $\bar{c}_{13,15}=4$. The arcs $(3,4)$, $(4,7)$, $(7,8)$, $(8,13)$ are tight, but the tight arcs from activity $13$ do not reach FINISH, so the chain $4,7,8,13$ is not on a critical path.

!!! chiave ""

    The $\mathrm{PD}$ model minimizes $t_{n+1}-t_0$ subject to $t_j-t_i \ge d_i$ on every arc; its dual sends one unit of flow from START to FINISH along a longest path. Both optimal values are $T$: $\mathit{ES}$ and $\mathit{LS}$ are optimal schedules, and every critical path is an optimal dual solution.

---

**Next:** [9.8 Two critical paths and changes of durations](two-critical-paths-and-changes-of-durations.md)

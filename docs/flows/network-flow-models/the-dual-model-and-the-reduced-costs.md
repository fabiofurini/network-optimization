---
title: "The dual model and the reduced costs"
---

# 4.7 The dual model and the reduced costs { #sez-sec-nf-dual }

<div class="info-capitolo" markdown>

**Part 3 · Flows · Chapter 4** · [:material-book-open-variant: Chapter 4: Flow models](index.md) · [:material-file-pdf-box: Lecture notes, volume 3 (PDF)](../../pdf/lecture-notes-3-flows.pdf) · [:material-pencil: Exercises: Flow models](../../exercises/network-flow-models.md)

</div>

- By <span style="color:#1971c2">[Proposition 4.9](removing-the-lower-bounds.md#box-12-nf-prop-subst)</span> the lower bounds can be removed, so in this section $\vet{l}=\vet{0}$ and every capacity is finite. The constraint $x_{ij} \le u_{ij}$ is written as $-x_{ij} \ge -u_{ij}$.

- Following the rules of [Chapter 9 «Duality theory»](https://fabiofurini.github.io/linear-programming/duality/09-duality/) of the module Linear Programming, we use a free dual variable $\pi_i$, the <strong>potential</strong> of node $i$, for its conservation equation, and a non-negative dual variable $\alpha_{ij}$ for the capacity of $(i,j)$.

!!! chiave ""

    Using free dual variables $\pi_i$ for the constraints [(4.1b)](the-minimum-cost-flow-model.md#mjx-eqn:nf:cons) and non-negative dual variables $\alpha_{ij}$ for the capacities, the dual model of the $\mathrm{MCF}$ model with $\vet{l}=\vet{0}$ is:

    <a id="eq-nf-DUAL"></a>

    \begin{align*}
    &&   \max \;\;{\sum_{i \in N} b_i \, \pi_i - \sum_{(i,j) \in A} u_{ij} \, \alpha_{ij}}        \label{nf:dobj}  \tag{4.2a}\\[1ex]
    && \text{subject to} \quad  \pi_i - \pi_j - \alpha_{ij} &\le c_{ij}, & \forall (i,j) \in A, \label{nf:dcons}  \tag{4.2b}\\[1ex]
    && \pi_i &\in \R, & \forall i \in N,                                                    \label{nf:dfree}  \tag{4.2c}\\[1ex]
    && \alpha_{ij} &\ge 0, & \forall (i,j) \in A.                                         \label{nf:dalpha} \tag{4.2d}
    \end{align*}

    This LP model is referred to as the $D(\mathrm{MCF})$ model.

- Description of the dual model:

    - the column of $x_{ij}$ has $+1$ in the equation of $i$, $-1$ in the equation of $j$ and $-1$ in its capacity constraint, which gives the dual constraint $\eqref{nf:dcons}$, one for every arc;

    - the primal variables are non-negative, so the dual constraints are of type $\le$.

- Adding the same constant to all the potentials changes neither $\eqref{nf:dcons}$ nor the objective, since $\sum_{i \in N} b_i=0$: the potentials can be normalized, for example with $\pi_n=0$.

<a id="box-24-nf-def-reduced"></a>

!!! definizione "Definition 4.17: reduced cost"

    Given potentials $\vet{\pi} \in \R^n$, the <strong>reduced cost</strong> of the arc $(i,j) \in A$ is

    $$
    \bar{c}_{ij}=c_{ij}-\pi_i+\pi_j .
    $$

- The dual constraint $\eqref{nf:dcons}$ reads $\bar{c}_{ij}+\alpha_{ij} \ge 0$. For fixed potentials, the best choice of $\alpha_{ij} \ge 0$ is the smallest one, $\alpha_{ij}=\max\{0,-\bar{c}_{ij}\}$.

<a id="box-25-nf-lem-identity"></a>

!!! teorema "Lemma 4.18: cost and reduced cost"

    For every $\vet{x}$ with $\mat{B}\vet{x}=\vet{b}$ and every $\vet{\pi} \in \R^n$,

    $$
    \sum_{(i,j) \in A} c_{ij}\, x_{ij}=\sum_{(i,j) \in A} \bar{c}_{ij}\, x_{ij}+\sum_{i \in N} b_i\, \pi_i .
    $$

??? dimostrazione "Proof"

    Since $c_{ij}=\bar{c}_{ij}+\pi_i-\pi_j$, it suffices to show $\sum_{(i,j) \in A}(\pi_i-\pi_j)\,x_{ij}=\sum_{i \in N} b_i\pi_i$. The term $\pi_i x_{ij}$ goes to the tail and $-\pi_j x_{ij}$ to the head, so

    $$
    \sum_{(i,j) \in A}(\pi_i-\pi_j)\,x_{ij}=\sum_{i \in N} \pi_i \Big(\sum_{(i,j) \in \delta^+(i)} x_{ij}-\sum_{(j,i)
    \in \delta^-(i)} x_{ji}\Big)=\sum_{i \in N} \pi_i\, b_i .
    \qedhere
    $$

    <p class="qed-riga"><span class="qed">□</span></p>

<a id="box-26-nf-th-gap"></a>

!!! teorema "Theorem 4.19: duality gap"

    Let $\vet{x}$ be a feasible flow ($\vet{l}=\vet{0}$) and $(\vet{\pi},\vet{\alpha})$ a feasible solution of the $D(\mathrm{MCF})$ model. Then

    $$
    \sum_{(i,j) \in A} c_{ij}x_{ij}-\Big(\sum_{i \in N} b_i\pi_i-\sum_{(i,j) \in A} u_{ij}\alpha_{ij}\Big)
    =\sum_{(i,j) \in A} (\bar{c}_{ij}+\alpha_{ij})\,x_{ij}+\sum_{(i,j) \in A} \alpha_{ij}\,(u_{ij}-x_{ij}) \;\ge\; 0,
    $$

    and both solutions are optimal if and only if, for every arc, $(\bar{c}_{ij}+\alpha_{ij})\,x_{ij}=0$ and $\alpha_{ij}(u_{ij}-x_{ij})=0$.

??? dimostrazione "Proof"

    By <span style="color:#1971c2">[Lemma 4.18](#box-25-nf-lem-identity)</span>, the left-hand side is $\sum \bar{c}_{ij}x_{ij}+\sum u_{ij}\alpha_{ij}$, and $u_{ij}\alpha_{ij}=\alpha_{ij}x_{ij}+\alpha_{ij}(u_{ij}-x_{ij})$ gives the identity.

    - Every term is non-negative: $\bar{c}_{ij}+\alpha_{ij} \ge 0$ by $\eqref{nf:dcons}$, $\alpha_{ij} \ge 0$, and $0 \le x_{ij} \le u_{ij}$.

    - If the gap is zero, the primal cost equals a dual value, which is a lower bound on every primal cost by the inequality just proved: $\vet{x}$ is optimal, and in the same way $(\vet{\pi},\vet{\alpha})$ is optimal.

    - If both are optimal, the gap is zero by the strong duality theorem of [Chapter 9 «Duality theory»](https://fabiofurini.github.io/linear-programming/duality/09-duality/). A sum of non-negative terms is zero if and only if every term is zero.

    <p class="qed-riga"><span class="qed">□</span></p>

<a id="box-27-nf-cor-certificate"></a>

!!! teorema "Corollary 4.20: reduced cost certificate"

    Let $\vet{x}$ be a feasible flow ($\vet{l}=\vet{0}$) and $\vet{\pi} \in \R^n$ potentials such that, for every arc,

    $$
    \bar{c}_{ij}>0 \;\Rightarrow\; x_{ij}=0, \qquad\qquad \bar{c}_{ij}<0 \;\Rightarrow\; x_{ij}=u_{ij}.
    $$

    Then $\vet{x}$ is an optimal flow, and $\vet{\pi}$ with $\alpha_{ij}=\max\{0,-\bar{c}_{ij}\}$ is an optimal solution of the $D(\mathrm{MCF})$ model.

??? dimostrazione "Proof"

    The pair $(\vet{\pi},\vet{\alpha})$ is dual feasible, since $\alpha_{ij} \ge 0$ and $\bar{c}_{ij}+\alpha_{ij} \ge 0$. We check the two conditions of <span style="color:#1971c2">[Theorem 4.19](#box-26-nf-th-gap)</span> on every arc.

    - If $\bar{c}_{ij} \ge 0$, then $\alpha_{ij}=0$, and $\bar{c}_{ij}x_{ij}=0$ because $\bar{c}_{ij}>0$ forces $x_{ij}=0$.

    - If $\bar{c}_{ij}<0$, then $\bar{c}_{ij}+\alpha_{ij}=0$, and $\alpha_{ij}(u_{ij}-x_{ij})=0$ because $x_{ij}=u_{ij}$.

    The gap is zero, so both solutions are optimal. <span class="qed">□</span>

- An arc with positive reduced cost is empty, an arc with negative reduced cost is saturated, and an arc strictly between its bounds has reduced cost zero.

<a id="box-28-nf-ex-dual"></a>

!!! esempio "Example 4.8: the dual of the reference network"

    For the network of <span style="color:#1971c2">[Example 4.1](networks-and-flows.md#box-3-nf-ex-ref)</span>, the $D(\mathrm{MCF})$ model is

    $$
    \max\; 5\pi_1+2\pi_2-3\pi_4-4\pi_6-\big(4\alpha_{12}+4\alpha_{13}+4\alpha_{24}+2\alpha_{32}+4\alpha_{35}+3\alpha_{43}
    +5\alpha_{46}+3\alpha_{54}+2\alpha_{56}\big)
    $$

    with $\vet{\alpha} \ge \vet{0}$, free potentials, and one constraint per arc:

    $$
    \begin{array}{lll}
    \pi_1-\pi_2-\alpha_{12} \le 2, & \pi_1-\pi_3-\alpha_{13} \le 2, & \pi_2-\pi_4-\alpha_{24} \le 5,\\
    \pi_3-\pi_2-\alpha_{32} \le 2, & \pi_3-\pi_5-\alpha_{35} \le 3, & \pi_4-\pi_3-\alpha_{43} \le 3,\\
    \pi_4-\pi_6-\alpha_{46} \le 5, & \pi_5-\pi_4-\alpha_{54} \le 5, & \pi_5-\pi_6-\alpha_{56} \le 3.
    \end{array}
    $$

    The balances $b_3=b_5=0$ make $\pi_3$ and $\pi_5$ disappear from the objective.

- The potentials and the reduced costs are the basis of the optimality tests of [Chapter 6 «Minimum cost flow»](https://fabiofurini.github.io/network-optimization/flows/min-cost-flow/).

!!! chiave ""

    The dual of the $\mathrm{MCF}$ model has a potential $\pi_i$ per node; the reduced cost is $\bar{c}_{ij}=c_{ij}-\pi_i+\pi_j$. A feasible flow whose positive-reduced-cost arcs are empty and negative-reduced-cost arcs are saturated is optimal.

---

**Next:** [4.8 Special cases](special-cases.md)

---
title: "Negative cycle optimality conditions"
---

# 6.3 Negative cycle optimality conditions { #sez-sec-mc-negcycle }

<div class="info-capitolo" markdown>

**Part 3 · Flows · Chapter 6** · [:material-book-open-variant: Chapter 6: Minimum cost flow](index.md) · [:material-file-pdf-box: Lecture notes, volume 3 (PDF)](../../pdf/lecture-notes-3-flows.pdf) · [:material-presentation: Slides](../../pdf/slides-min-cost-flow.pdf) · [:material-pencil: Exercises: Minimum cost flow](../../exercises/min-cost-flow.md) · [:material-gesture-tap: App: Minimum cost flow: cycle canceling and successive shortest paths](../../lab/minimum-cost-flow.md)

</div>

<a id="box-9-mc-th-negcycle"></a>

!!! teorema "Theorem 6.7: negative cycle optimality"

    A feasible flow $\vet{x}$ is optimal if and only if its residual network $G(\vet{x})$ has no negative cycle.

??? dimostrazione "Proof"

    We prove the two implications.

    - <em>A negative cycle improves $\vet{x}$.</em> Let $W$ be a negative cycle of $G(\vet{x})$ and $\theta=\min\{r(W), 1\}>0$. By <span style="color:#1971c2">[Proposition 6.3](the-residual-network-with-costs.md#box-3-mc-prop-augment)</span>, $\vet{x}$ augmented along $W$ by $\theta$ is a feasible flow of cost $\vet{c}'\vet{x}+\theta\,c(W)<\vet{c}'\vet{x}$, so $\vet{x}$ is not optimal.

    - <em>Without negative cycles $\vet{x}$ is optimal.</em> Let $\vet{x}'$ be any feasible flow. By <span style="color:#1971c2">[Lemma 6.6](circulations-and-their-decomposition.md#box-7-mc-lem-diff)</span>, $\vet{c}'\vet{x}'=\vet{c}'\vet{x}+\sum_h\theta_h\,c(W_h)$ with cycles $W_h$ of $G(\vet{x})$ and $\theta_h>0$. Every $c(W_h)$ is non-negative, so $\vet{c}'\vet{x}' \ge \vet{c}'\vet{x}$.

    <p class="qed-riga"><span class="qed">□</span></p>

- The proof compares two flows through their difference, and uses no LP duality.

- When some capacities are infinite the model can be unbounded, and the next proposition tells exactly when.

<a id="box-10-mc-prop-unbounded"></a>

!!! teorema "Proposition 6.8: unbounded instances"

    Assume that the $\mathrm{MCF}$ model has a feasible flow. It is unbounded if and only if $G$ has a directed cycle $C$ of negative cost, $\sum_{(i,j) \in C} c_{ij}<0$, whose arcs all have $u_{ij}=+\infty$.

??? dimostrazione "Proof"

    <em>If.</em> Let $\vet{x}$ be feasible. Every arc of $C$ has $x_{ij}<u_{ij}=+\infty$, so $C$ is a cycle of forward arcs of $G(\vet{x})$ with $r(C)=+\infty$. Augmenting along $C$ by any $\theta>0$ gives feasible flows of cost $\vet{c}'\vet{x}+\theta\,c(C)$, which tends to $-\infty$.

    <em>Only if.</em> Assume that there is no such cycle $C$, and fix a feasible flow $\vet{x}$. Let $R$ be the largest finite residual capacity of an arc of $G(\vet{x})$ ($R=0$ if there is none), and $K=\max_{(i,j) \in A}|c_{ij}|$. Let $\vet{x}'$ be any feasible flow, decomposed as in <span style="color:#1971c2">[Lemma 6.6](circulations-and-their-decomposition.md#box-7-mc-lem-diff)</span>.

    1. A cycle $W_h$ with $c(W_h)<0$ has an arc $a$ of finite residual capacity: backward arcs have finite residual capacity, and a cycle of forward arcs with infinite capacity would be a cycle $C$. Hence $\theta_h \le y_a \le r_a \le R$.

    2. $W_h$ has at most $n$ arcs, so $c(W_h) \ge -nK$; there are at most $m$ cycles.

    Hence $\vet{c}'\vet{x}' \ge \vet{c}'\vet{x}-m\,R\,n\,K$ for every feasible $\vet{x}'$: the model is bounded. <span class="qed">□</span>

- A feasible LP that is bounded has an optimal solution ([Linear Programming, Chapter 15 «The geometry of Linear Programming»](https://fabiofurini.github.io/linear-programming/advanced-methods/15-geometry/)). With finite capacities the $\mathrm{MCF}$ model is never unbounded.

<a id="box-11-mc-ex-negcycle"></a>

!!! esempio "Example 6.3: a flow that is not optimal and an unbounded instance"

    - The feasible flow $\bar{\vet{x}}=(1,4,3,0,4,0,2,2,2)$ of [Chapter 4](https://fabiofurini.github.io/network-optimization/flows/network-flow-models/networks-and-flows/) costs $63$. Its residual network has the cycle $W=1,2,4,5,3,1$, made of the forward arcs $(1,2)$, $(2,4)$ and of the backward arcs $(4,5)$, $(5,3)$, $(3,1)$:

        $$
        c(W)=2+5-5-3-2=-3, \qquad r(W)=\min\{3,1,2,4,4\}=1 .
        $$

        By <span style="color:#1971c2">[Theorem 6.7](#box-9-mc-th-negcycle)</span> $\bar{\vet{x}}$ is not optimal. Augmenting by $1$ gives $\tilde{\vet{x}}$, of cost $63-3=60$: the gap $3$ of $\bar{\vet{x}}$ computed with the dual solution in Chapter 4.

    - With $c_{54}=-12$ and $u_{35}=u_{54}=u_{43}=+\infty$, the directed cycle $3,5,4,3$ of $G$ costs $3-12+3=-6$ and has infinite capacities. By <span style="color:#1971c2">[Proposition 6.8](#box-10-mc-prop-unbounded)</span> the model is unbounded, as Gurobi confirms: each unit sent around the cycle lowers the cost by $6$.

!!! chiave ""

    A feasible flow is optimal if and only if its residual network has no negative cycle. A feasible model is unbounded if and only if a negative directed cycle has all its capacities infinite.

---

**Next:** [6.4 Optimality conditions with potentials](optimality-conditions-with-potentials.md)

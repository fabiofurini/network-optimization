---
title: "Feasibility conditions"
---

# 4.3 Feasibility conditions { #sez-sec-nf-feasibility }

<div class="info-capitolo" markdown>

**Part 3 · Flows · Chapter 4** · [:material-book-open-variant: Chapter 4: Flow models](index.md) · [:material-file-pdf-box: Lecture notes, volume 3 (PDF)](../../pdf/lecture-notes-3-flows.pdf) · [:material-presentation: Slides](../../pdf/slides-network-flow-models.pdf) · [:material-pencil: Exercises: Flow models](../../exercises/network-flow-models.md)

</div>

<a id="box-7-nf-def-balanced"></a>

!!! definizione "Definition 4.5: balanced network"

    A network is <strong>balanced</strong> if $\sum_{i \in N} b_i=0$, that is, if the total supply equals the total demand.

<a id="box-8-nf-prop-balance"></a>

!!! teorema "Proposition 4.6: a feasible network is balanced"

    If a network $G=(N,A)$ has a feasible flow, then $\sum_{i \in N} b_i=0$.

??? dimostrazione "Proof"

    Apply <span style="color:#1971c2">[Lemma 4.3](networks-and-flows.md#box-4-nf-lem-cut)</span> with $S=N$: no arc leaves or enters $N$, so $\delta^+(N)=\delta^-(N)= \emptyset$ and $\sum_{i \in N} b_i=0$. In matrix form, the rows of $\mat{B}$ add up to the zero vector, hence so do the entries of $\vet{b}=\mat{B}\vet{x}$. <span class="qed">□</span>

<a id="box-9-nf-prop-cut"></a>

!!! teorema "Proposition 4.7: cut condition"

    If a network $G=(N,A)$ has a feasible flow, then for every $S \subseteq N$

    $$
    \sum_{i \in S} b_i \;\le\; u(\delta^+(S)) - l(\delta^-(S)),
    $$

    where $u(F)$ and $l(F)$ are the sums of the capacities and of the lower bounds of the arcs of $F$.

??? dimostrazione "Proof"

    Let $\vet{x}$ be a feasible flow. By <span style="color:#1971c2">[Lemma 4.3](networks-and-flows.md#box-4-nf-lem-cut)</span> and the bounds $x_{ij} \le u_{ij}$ on $\delta^+(S)$ and $x_{ij} \ge l_{ij}$ on $\delta^-(S)$,

    $$
    \sum_{i \in S} b_i = x(\delta^+(S))-x(\delta^-(S)) \le u(\delta^+(S))-l(\delta^-(S)).
    \qedhere
    $$

    <p class="qed-riga"><span class="qed">□</span></p>

- The supply of the nodes of $S$, net of their demand, must be able to leave $S$ through the arcs of $\delta^+(S)$, while the arcs of $\delta^-(S)$ bring at least their lower bounds into $S$.

- A balanced network can still have no feasible flow: the balance is only a necessary condition.

<a id="box-10-nf-ex-infeasible"></a>

!!! esempio "Example 4.3: balanced networks without a feasible flow"

    We keep the arcs, costs and capacities of the reference network and change the balances.

    1. With $b_5=-1$, $b_6=1$ and $b_i=0$ for the other nodes, the network is balanced. But node $6$ has no leaving arc: for $S=\{6\}$ we get $\delta^+(S)=\emptyset$, and the cut condition fails, since $b_6=1>0$.

    2. With $b_1=9$, $b_6=-8$ and the other balances as in <span style="color:#1971c2">[Example 4.1](networks-and-flows.md#box-3-nf-ex-ref)</span>, the network is balanced, since $9+2-3-8=0$. For $S=\{1\}$ we get $u(\delta^+(S))=u_{12}+u_{13}=8<9=b_1$: node $1$ cannot send out its supply.

    For the reference network itself, all the $62$ sets $S$ with $\emptyset \neq S \neq N$ satisfy the cut condition, and the flow $\bar{\vet{x}}$ of <span style="color:#1971c2">[Example 4.1](networks-and-flows.md#box-3-nf-ex-ref)</span> is feasible.

!!! chiave ""

    A network with a feasible flow is balanced, and every cut can carry the net supply of the nodes inside it. These conditions are necessary: a balanced network may have no feasible flow.

---

**Next:** [4.4 Removing the lower bounds](removing-the-lower-bounds.md)

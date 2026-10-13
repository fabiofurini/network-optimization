---
title: "Cuts"
---

# 5.2 Cuts { #sez-sec-mf-cuts }

<div class="info-capitolo" markdown>

**Part 3 · Flows · Chapter 5** · [:material-book-open-variant: Chapter 5: Maximum flow](index.md) · [:material-file-pdf-box: Lecture notes, volume 3 (PDF)](../../pdf/lecture-notes-3-flows.pdf) · [:material-pencil: Exercises: Maximum flow](../../exercises/maximum-flow.md) · [:material-gesture-tap: App: Maximum flow: Ford–Fulkerson and Edmonds–Karp](../../lab/maximum-flow-ford-fulkerson-edmonds-karp.md)

</div>

<a id="box-3-mf-def-cut"></a>

!!! definizione "Definition 5.2: $s$–$t$ cut"

    Let $S \subseteq N$ with $s \in S$ and $t \notin S$. The <strong>$s$–$t$ cut</strong> $(S,N \setminus S)$ is the partition of the nodes into $S$ and $N \setminus S$.

    - Its <strong>forward arcs</strong> are the arcs of $\delta^+(S)$, from $S$ to $N \setminus S$, and its <strong>backward arcs</strong> the arcs of $\delta^-(S)$, from $N \setminus S$ to $S$.

    - Its <strong>capacity</strong> is the total capacity of the forward arcs:

        $$
        u(S,N \setminus S)=\sum_{(i,j) \in \delta^+(S)} u_{ij} .
        $$

    - A <strong>minimum cut</strong> is an $s$–$t$ cut of minimum capacity.

- The capacities of the backward arcs do not enter $u(S,N \setminus S)$.

- Each node other than $s$ and $t$ can be on either side, so a network has $2^{n-2}$ $s$–$t$ cuts.

- As in Chapter 4, $x(F)=\sum_{(i,j) \in F} x_{ij}$ for a set of arcs $F$.

<a id="box-4-mf-lem-cut"></a>

!!! teorema "Lemma 5.3: flow across an $s$–$t$ cut"

    Let $\vet{x}$ be a feasible flow of value $v$. Then, for every $s$–$t$ cut $(S,N \setminus S)$,

    $$
    v=x(\delta^+(S))-x(\delta^-(S)).
    $$

    In particular, with $S=N \setminus \{t\}$, the net inflow of $t$ is $v$.

??? dimostrazione "Proof"

    Let $b_i$ be the net outflow of node $i$ under $\vet{x}$: $b_s=v$ and $b_i=0$ for $i \notin \{s,t\}$. Then $\vet{x}$ satisfies flow conservation with these balances, and [Chapter 4, Lemma «flow across a cut»](https://fabiofurini.github.io/network-optimization/flows/network-flow-models/networks-and-flows/) gives $x(\delta^+(S))-x(\delta^-(S))=\sum_{i \in S} b_i$ for every $S \subseteq N$.

    1. With $S=N$ no arc leaves or enters $S$, so $\sum_{i \in N} b_i=0$ and $b_t=-v$.

    2. For an $s$–$t$ cut, $s \in S$ and $t \notin S$, so $\sum_{i \in S} b_i=b_s=v$. <span class="qed">□</span>

<a id="box-5-mf-cor-weak"></a>

!!! teorema "Corollary 5.4: weak duality"

    For every feasible flow $\vet{x}$ of value $v$ and every $s$–$t$ cut $(S,N \setminus S)$,

    $$
    v \le u(S,N \setminus S),
    $$

    with equality if and only if $x_{ij}=u_{ij}$ for every $(i,j) \in \delta^+(S)$ and $x_{ij}=0$ for every $(i,j) \in \delta^-(S)$. In case of equality, $\vet{x}$ is a maximum flow and $(S,N \setminus S)$ is a minimum cut.

??? dimostrazione "Proof"

    By <span style="color:#1971c2">[Lemma 5.3](#box-4-mf-lem-cut)</span> and the bounds $x_{ij} \le u_{ij}$ on $\delta^+(S)$ and $x_{ij} \ge 0$ on $\delta^-(S)$,

    $$
    v=x(\delta^+(S))-x(\delta^-(S)) \le u(S,N \setminus S)-0 .
    $$

    - Equality holds if and only if every bound used is tight, arc by arc.

    - In case of equality, every feasible flow $\vet{x}'$ has value $v' \le u(S,N \setminus S)=v$, and every $s$–$t$ cut $(S',N \setminus S')$ has $u(S',N \setminus S') \ge v=u(S,N \setminus S)$.

    <p class="qed-riga"><span class="qed">□</span></p>

<a id="box-6-mf-ex-cuts"></a>

!!! esempio "Example 5.2: the cuts of the reference network"

    The reference network of <span style="color:#1971c2">[Example 5.1](the-maximum-flow-problem.md#box-2-mf-ex-ref)</span> has $2^4=16$ $s$–$t$ cuts. Next to each set $S$, the capacity $u(S,N \setminus S)$:

    $$
    \begin{array}{cc|cc|cc|cc}
    \hline {S} & {u} & {S} & {u} & {S} & {u} & {S} & {u} \\
    \hline {\{1\}} & {9} & {\{1,2\}} & {7} & {\{1,3\}} & {11} & {\{1,4\}} & {15} \\
    {\{1,5\}} & {14} & {\{1,2,3\}} & {7} & {\{1,2,4\}} & {10} & {\{1,2,5\}} & {12} \\
    {\{1,3,4\}} & {15} & {\{1,3,5\}} & {12} & {\{1,4,5\}} & {18} & {\{1,2,3,4\}} & {8} \\
    {\{1,2,3,5\}} & {8} & {\{1,2,4,5\}} & {13} & {\{1,3,4,5\}} & {14} & {\{1,2,3,4,5\}} & {7} \\
    \hline
    \end{array}
    $$

    - The minimum capacity is $7$, attained by three cuts: $S=\{1,2\}$, $S=\{1,2,3\}$ and $S=\{1,2,3,4,5\}$. By <span style="color:#1971c2">[Corollary 5.4](#box-5-mf-cor-weak)</span>, no feasible flow has value larger than $7$.

    - For $S=\{1,2,3\}$ the forward arcs are $(2,4)$, $(3,5)$ and the backward arc is $(4,3)$. With the flow $\bar{\vet{x}}$ of <span style="color:#1971c2">[Example 5.1](the-maximum-flow-problem.md#box-2-mf-ex-ref)</span>,

        $$
        \bar{x}_{24}+\bar{x}_{35}-\bar{x}_{43}=3+2-2=3=v, \qquad u(S,N \setminus S)=u_{24}+u_{35}=3+4=7 .
        $$

!!! attenzione "The capacity of a cut"

    The capacity $u(S,N \setminus S)$ adds up the capacities of the forward arcs only. For $S=\{1,2,3\}$ it is $u_{24}+u_{35}=7$; adding the capacity of the backward arc $(4,3)$ would give $9$, which bounds nothing. A flow on a backward arc brings units back into $S$ and lowers the net flow across the cut.

!!! chiave ""

    The net flow across every $s$–$t$ cut is the value $v$, so $v \le u(S,N \setminus S)$ for every flow and every cut, with equality when the forward arcs are saturated and the backward arcs empty. On the reference network no flow has value larger than $7$.

---

**Next:** [5.3 The residual network](the-residual-network.md)

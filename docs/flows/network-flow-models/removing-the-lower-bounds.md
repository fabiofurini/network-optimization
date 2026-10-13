---
title: "Removing the lower bounds"
---

# 4.4 Removing the lower bounds { #sez-sec-nf-lower }

<div class="info-capitolo" markdown>

**Part 3 · Flows · Chapter 4** · [:material-book-open-variant: Chapter 4: Flow models](index.md) · [:material-file-pdf-box: Lecture notes, volume 3 (PDF)](../../pdf/lecture-notes-3-flows.pdf) · [:material-pencil: Exercises: Flow models](../../exercises/network-flow-models.md)

</div>

<a id="box-11-nf-def-subst"></a>

!!! definizione "Definition 4.8: substitution of the lower bounds"

    Given a network with lower bounds $\vet{l}$, the <strong>substituted network</strong> has the same nodes, arcs and costs, zero lower bounds and

    $$
    b'_i=b_i-\sum_{(i,j) \in \delta^+(i)} l_{ij}+\sum_{(j,i) \in \delta^-(i)} l_{ji}, \quad \forall i \in N,
    \qquad\quad u'_{ij}=u_{ij}-l_{ij}, \quad \forall (i,j) \in A,
    $$

    that is, $\vet{b}'=\vet{b}-\mat{B}\vet{l}$ and $\vet{u}'=\vet{u}-\vet{l}$.

- The $l_{ij}$ units that must travel on $(i,j)$ are sent in advance: the tail $i$ has $l_{ij}$ units less to send, the head $j$ has $l_{ij}$ units less to receive, and the arc has $l_{ij}$ units less of free capacity.

<a id="box-12-nf-prop-subst"></a>

!!! teorema "Proposition 4.9: removing the lower bounds"

    The map $\vet{x}'=\vet{x}-\vet{l}$ is a one-to-one correspondence between the feasible flows of a network and those of its substituted network, and

    $$
    \vet{c}'\vet{x}=\vet{c}'\vet{x}'+\vet{c}'\vet{l}.
    $$

    Hence the two $\mathrm{MCF}$ models have the same optimal solutions, up to the shift by $\vet{l}$, and their optimal values differ by the constant $\vet{c}'\vet{l}$.

??? dimostrazione "Proof"

    The map is linear and invertible, with inverse $\vet{x}=\vet{x}'+\vet{l}$. For every $\vet{x} \in \R^m$:

    1. $\mat{B}\vet{x}=\vet{b}$ if and only if $\mat{B}\vet{x}'=\mat{B}\vet{x}-\mat{B}\vet{l}=\vet{b}-\mat{B}\vet{l} =\vet{b}'$;

    2. $\vet{l} \le \vet{x} \le \vet{u}$ if and only if $\vet{0} \le \vet{x}' \le \vet{u}-\vet{l}=\vet{u}'$;

    3. $\vet{c}'\vet{x}=\vet{c}'(\vet{x}'+\vet{l})=\vet{c}'\vet{x}'+\vet{c}'\vet{l}$.

    The cost of every feasible flow changes by the same constant, so the optimal solutions correspond. <span class="qed">□</span>

<a id="box-13-nf-ex-lower"></a>

!!! esempio "Example 4.4: a lower bound on the reference network"

    In the network of <span style="color:#1971c2">[Example 4.1](networks-and-flows.md#box-3-nf-ex-ref)</span> we impose $l_{32}=1$: at least one unit must travel from $3$ to $2$. The column of $(3,2)$ in $\mat{B}$ has $+1$ in row $3$ and $-1$ in row $2$, so $\mat{B}\vet{l}=(0,-1,1,0,0,0)'$ and

    $$
    \vet{b}'=\vet{b}-\mat{B}\vet{l}=(5,\,3,\,-1,\,-3,\,0,\,-4)', \qquad u'_{32}=2-1=1, \qquad \vet{c}'\vet{l}=c_{32}\,
    l_{32}=2.
    $$

    Node $3$ becomes a demand node, because it has already sent one unit, and node $2$ has one more unit to send. The substituted network has optimal value $60$; adding the constant $2$, the optimal value with $l_{32}=1$ is $62$.

!!! chiave ""

    The substitution $\vet{x}=\vet{l}+\vet{x}'$ removes the lower bounds: $\vet{b}'=\vet{b}-\mat{B}\vet{l}$, $\vet{u}'=\vet{u}-\vet{l}$, and the objective changes by the constant $\vet{c}'\vet{l}$.

---

**Next:** [4.5 Unbalanced instances](unbalanced-instances.md)

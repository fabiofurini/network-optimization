---
title: "Special cases"
---

# 4.8 Special cases { #sez-sec-nf-special }

<div class="info-capitolo" markdown>

**Part 3 · Flows · Chapter 4** · [:material-book-open-variant: Chapter 4: Flow models](index.md) · [:material-file-pdf-box: Lecture notes, volume 3 (PDF)](../../pdf/lecture-notes-3-flows.pdf) · [:material-presentation: Slides](../../pdf/slides-network-flow-models.pdf) · [:material-pencil: Exercises: Flow models](../../exercises/network-flow-models.md)

</div>

- Several classical problems are $\mathrm{MCF}$ models with special data; all the lower bounds are zero.

<div class="tabella" markdown="0"><table>
<tr>
<th>problem</th>
<th>the <span class="arithmatex">\(\mathrm{MCF}\)</span> model</th>
</tr>
<tr>
<td><strong>Shortest path</strong></td>
<td><span class="arithmatex">\(b_s=1\)</span>, <span class="arithmatex">\(b_t=-1\)</span>, <span class="arithmatex">\(b_i=0\)</span> otherwise; <span class="arithmatex">\(u_{ij}=+\infty\)</span>, <span class="arithmatex">\(c_{ij}\)</span> the length of the arc: the unit of flow travels from <span class="arithmatex">\(s\)</span> to <span class="arithmatex">\(t\)</span>.</td>
</tr>
<tr>
<td><strong>Maximum flow</strong></td>
<td><span class="arithmatex">\(b_i=0\)</span> for every node and <span class="arithmatex">\(c_{ij}=0\)</span> for every arc, plus the arc <span class="arithmatex">\((t,s)\)</span> with <span class="arithmatex">\(c_{ts}=-1\)</span> and <span class="arithmatex">\(u_{ts}=+\infty\)</span>: the flow on <span class="arithmatex">\((t,s)\)</span> is the value sent from <span class="arithmatex">\(s\)</span> to <span class="arithmatex">\(t\)</span>.</td>
</tr>
<tr>
<td><strong>Transportation</strong></td>
<td><span class="arithmatex">\(N=P \cup D\)</span> with arcs from the origins <span class="arithmatex">\(P\)</span> to the destinations <span class="arithmatex">\(D\)</span>; <span class="arithmatex">\(b_i\)</span> the supply of <span class="arithmatex">\(i \in P\)</span>, <span class="arithmatex">\(-b_j\)</span> the demand of <span class="arithmatex">\(j \in D\)</span>, <span class="arithmatex">\(u_{ij}=+\infty\)</span>.</td>
</tr>
<tr>
<td><strong>Assignment</strong></td>
<td>a transportation model with <span class="arithmatex">\(|P|=|D|\)</span>, <span class="arithmatex">\(b_i=1\)</span> for <span class="arithmatex">\(i \in P\)</span> and <span class="arithmatex">\(b_j=-1\)</span> for <span class="arithmatex">\(j \in D\)</span>.</td>
</tr>
</table></div>

- In the four models the balances and the bounds are integer, so the integer vertices of <span style="color:#1971c2">[Theorem 4.15](total-unimodularity-and-integrality.md#box-21-nf-th-vertices)</span> are paths, integer flows and assignments.

!!! chiave ""

    Shortest path, maximum flow, transportation and assignment are minimum cost flow models with special balances, capacities and costs.

---

**Next:** [4.9 A transshipment instance](a-transshipment-instance.md)

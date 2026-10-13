---
title: "The forward pass: earliest times"
---

# 9.3 The forward pass: earliest times { #sez-pm-sec-forward }

<div class="info-capitolo" markdown>

**Part 5 · Project management · Chapter 9** · [:material-book-open-variant: Chapter 9: Project management](index.md) · [:material-file-pdf-box: Lecture notes, volume 5 (PDF)](../../pdf/lecture-notes-5-project-management.pdf) · [:material-pencil: Exercises: Project management](../../exercises/project-management.md)

</div>

- We first assume that no delay occurs: every activity takes its estimated duration and starts as soon as all its immediate predecessors are finished.

<a id="box-9-pm-def-earliest"></a>

!!! definizione "Definition 9.7: earliest start and finish times"

    Let $v_0,v_1,\dots,v_{n+1}$ be a topological order of the project network. The <strong>earliest start time</strong> $\mathit{ES}_j$ and the <strong>earliest finish time</strong> $\mathit{EF}_j$ of the nodes are computed in this order by the <strong>forward pass</strong>:

    $$
    \mathit{ES}_0=0, \qquad \mathit{ES}_j=\max_{(i,j) \in \delta^-(j)} \mathit{EF}_i, \quad \forall j \in N \setminus \{0\}, \qquad
    \mathit{EF}_j=\mathit{ES}_j+d_j, \quad \forall j \in N .
    $$

- This is the <strong>earliest start time rule</strong>: the earliest start time of an activity is the largest earliest finish time of its immediate predecessors. When node $j$ is processed, its predecessors come before it in the topological order, so their earliest finish times are known.

- As in [Chapter 3](https://fabiofurini.github.io/network-optimization/trees-and-paths/shortest-paths/shortest-paths-in-acyclic-graphs/), the topological order removes, at every step, the node without entering arcs of <strong>smallest index</strong>. Node $0$ is removed first.

<a id="box-10-pm-th-earliest"></a>

!!! teorema "Theorem 9.8: earliest times"

    For every node $j \in N$, $\mathit{ES}_j$ is the length of a longest path from START to $j$. Moreover, $\mathit{ES}$ is a schedule, and every schedule $\vet{t}$ satisfies $t_j \ge \mathit{ES}_j$ for every $j \in N$.

??? dimostrazione "Proof"

    We prove the first and the last claim by induction along the topological order.

    1. <em>Node $0$.</em> No arc enters START: the only path from START to $0$ has no arcs and length $0=\mathit{ES}_0$, and every schedule has $t_0=0=\mathit{ES}_0$.

    2. <em>Longest paths.</em> Let $j \neq 0$. Every path from START to $j$ is a path from START to some $i$ followed by an arc $(i,j) \in \delta^-(j)$ of length $d_i$, and $i$ comes before $j$. By induction its maximum length is

        $$
        \max_{(i,j) \in \delta^-(j)} \big(\mathit{ES}_i+d_i\big)=\max_{(i,j) \in \delta^-(j)} \mathit{EF}_i=\mathit{ES}_j .
        $$

    3. <em>Lower bound.</em> For every arc $(i,j) \in \delta^-(j)$, by induction $t_j \ge t_i+d_i \ge \mathit{ES}_i+d_i=\mathit{EF}_i$; hence $t_j \ge \mathit{ES}_j$.

    4. <em>$\mathit{ES}$ is a schedule.</em> $\mathit{ES}_0=0$, and $\mathit{ES}_j \ge \mathit{EF}_i=\mathit{ES}_i+d_i$ for every arc $(i,j) \in A$, by the maximum in the definition. <span class="qed">□</span>

<a id="box-11-pm-th-duration"></a>

!!! teorema "Theorem 9.9: minimum project duration"

    Under (H1) and (H2), the minimum project duration is $T=\mathit{ES}_{n+1}$, the length of a critical path, and the schedule $\mathit{ES}$ attains it.

??? dimostrazione "Proof"

    By <span style="color:#1971c2">[Theorem 9.8](#box-10-pm-th-earliest)</span>, $\mathit{ES}$ is a schedule of duration $\mathit{ES}_{n+1}$, and every schedule has $t_{n+1} \ge \mathit{ES}_{n+1}$: hence $T=\mathit{ES}_{n+1}$. By the same theorem, $\mathit{ES}_{n+1}$ is the length of a longest path from START to FINISH, that is, of a critical path. <span class="qed">□</span>

- Both assumptions are used: (H1) makes the lengths of the paths fixed numbers, and (H2) makes the precedences the only constraints of a schedule.

- The forward pass is the algorithm for acyclic graphs of [Chapter 3 «Shortest paths»](https://fabiofurini.github.io/network-optimization/trees-and-paths/shortest-paths/shortest-paths-in-acyclic-graphs/), with the maximum in place of the minimum: with the arc lengths $-d_i$, that algorithm computes the labels $d(j)=-\mathit{ES}_j$. A longest path is easy to find because the network is acyclic.

<a id="box-12-pm-ex-forward"></a>

!!! esempio "Example 9.3: the forward pass on the case study"

    In the case study every activity has immediate predecessors of smaller index, so the topological order is $0,1,2,\dots,15$. Each row processes one node: the earliest finish times of its immediate predecessors (the maximum in bold), then $\mathit{ES}_j$ and $\mathit{EF}_j$.

    <div class="tabella" markdown="0"><table>
    <tr>
    <th>node <span class="arithmatex">\(j\)</span></th>
    <th><span class="arithmatex">\(d_j\)</span></th>
    <th><span class="arithmatex">\(\mathit{EF}_i\)</span> of the predecessors (<span class="arithmatex">\(i\)</span>)</th>
    <th><span class="arithmatex">\(\mathit{ES}_j\)</span></th>
    <th><span class="arithmatex">\(\mathit{EF}_j\)</span></th>
    </tr>
    <tr>
    <td><span class="arithmatex">\(0\)</span></td>
    <td><span class="arithmatex">\(0\)</span></td>
    <td>—</td>
    <td><span class="arithmatex">\(0\)</span></td>
    <td><span class="arithmatex">\(0\)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">\(1\)</span></td>
    <td><span class="arithmatex">\(2\)</span></td>
    <td><span class="arithmatex">\(\mathbf{0}\)</span> (<span class="arithmatex">\(0\)</span>)</td>
    <td><span class="arithmatex">\(0\)</span></td>
    <td><span class="arithmatex">\(2\)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">\(2\)</span></td>
    <td><span class="arithmatex">\(4\)</span></td>
    <td><span class="arithmatex">\(\mathbf{2}\)</span> (<span class="arithmatex">\(1\)</span>)</td>
    <td><span class="arithmatex">\(2\)</span></td>
    <td><span class="arithmatex">\(6\)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">\(3\)</span></td>
    <td><span class="arithmatex">\(10\)</span></td>
    <td><span class="arithmatex">\(\mathbf{6}\)</span> (<span class="arithmatex">\(2\)</span>)</td>
    <td><span class="arithmatex">\(6\)</span></td>
    <td><span class="arithmatex">\(16\)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">\(4\)</span></td>
    <td><span class="arithmatex">\(6\)</span></td>
    <td><span class="arithmatex">\(\mathbf{16}\)</span> (<span class="arithmatex">\(3\)</span>)</td>
    <td><span class="arithmatex">\(16\)</span></td>
    <td><span class="arithmatex">\(22\)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">\(5\)</span></td>
    <td><span class="arithmatex">\(4\)</span></td>
    <td><span class="arithmatex">\(\mathbf{16}\)</span> (<span class="arithmatex">\(3\)</span>)</td>
    <td><span class="arithmatex">\(16\)</span></td>
    <td><span class="arithmatex">\(20\)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">\(6\)</span></td>
    <td><span class="arithmatex">\(5\)</span></td>
    <td><span class="arithmatex">\(\mathbf{20}\)</span> (<span class="arithmatex">\(5\)</span>)</td>
    <td><span class="arithmatex">\(20\)</span></td>
    <td><span class="arithmatex">\(25\)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">\(7\)</span></td>
    <td><span class="arithmatex">\(7\)</span></td>
    <td><span class="arithmatex">\(\mathbf{22}\)</span> (<span class="arithmatex">\(4\)</span>)</td>
    <td><span class="arithmatex">\(22\)</span></td>
    <td><span class="arithmatex">\(29\)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">\(8\)</span></td>
    <td><span class="arithmatex">\(9\)</span></td>
    <td><span class="arithmatex">\(20\)</span> (<span class="arithmatex">\(5\)</span>), <span class="arithmatex">\(\mathbf{29}\)</span> (<span class="arithmatex">\(7\)</span>)</td>
    <td><span class="arithmatex">\(29\)</span></td>
    <td><span class="arithmatex">\(38\)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">\(9\)</span></td>
    <td><span class="arithmatex">\(7\)</span></td>
    <td><span class="arithmatex">\(\mathbf{16}\)</span> (<span class="arithmatex">\(3\)</span>)</td>
    <td><span class="arithmatex">\(16\)</span></td>
    <td><span class="arithmatex">\(23\)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">\(10\)</span></td>
    <td><span class="arithmatex">\(8\)</span></td>
    <td><span class="arithmatex">\(\mathbf{25}\)</span> (<span class="arithmatex">\(6\)</span>), <span class="arithmatex">\(23\)</span> (<span class="arithmatex">\(9\)</span>)</td>
    <td><span class="arithmatex">\(25\)</span></td>
    <td><span class="arithmatex">\(33\)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">\(11\)</span></td>
    <td><span class="arithmatex">\(4\)</span></td>
    <td><span class="arithmatex">\(\mathbf{33}\)</span> (<span class="arithmatex">\(10\)</span>)</td>
    <td><span class="arithmatex">\(33\)</span></td>
    <td><span class="arithmatex">\(37\)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">\(12\)</span></td>
    <td><span class="arithmatex">\(5\)</span></td>
    <td><span class="arithmatex">\(\mathbf{33}\)</span> (<span class="arithmatex">\(10\)</span>)</td>
    <td><span class="arithmatex">\(33\)</span></td>
    <td><span class="arithmatex">\(38\)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">\(13\)</span></td>
    <td><span class="arithmatex">\(2\)</span></td>
    <td><span class="arithmatex">\(\mathbf{38}\)</span> (<span class="arithmatex">\(8\)</span>)</td>
    <td><span class="arithmatex">\(38\)</span></td>
    <td><span class="arithmatex">\(40\)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">\(14\)</span></td>
    <td><span class="arithmatex">\(6\)</span></td>
    <td><span class="arithmatex">\(37\)</span> (<span class="arithmatex">\(11\)</span>), <span class="arithmatex">\(\mathbf{38}\)</span> (<span class="arithmatex">\(12\)</span>)</td>
    <td><span class="arithmatex">\(38\)</span></td>
    <td><span class="arithmatex">\(44\)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">\(15\)</span></td>
    <td><span class="arithmatex">\(0\)</span></td>
    <td><span class="arithmatex">\(40\)</span> (<span class="arithmatex">\(13\)</span>), <span class="arithmatex">\(\mathbf{44}\)</span> (<span class="arithmatex">\(14\)</span>)</td>
    <td><span class="arithmatex">\(44\)</span></td>
    <td><span class="arithmatex">\(44\)</span></td>
    </tr>
    </table></div>

    The FINISH node gives $T=\mathit{ES}_{15}=44$: if everything stays on schedule, the project is completed in $44$ weeks. In the figure, next to each node, its duration (blue) and its earliest times.

    ![Figure 2](../../img/project-management/fig02.svg){ .fig loading=lazy  }

!!! chiave ""

    The forward pass computes, in topological order, $\mathit{ES}_j=\max \mathit{EF}_i$ over the immediate predecessors and $\mathit{EF}_j=\mathit{ES}_j+d_j$. $\mathit{ES}_j$ is the length of a longest path from START to $j$, and $T=\mathit{ES}_{n+1}$ is the length of a critical path.

---

**Next:** [9.4 The backward pass: latest times](the-backward-pass-latest-times.md)

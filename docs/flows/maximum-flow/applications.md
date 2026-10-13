---
title: "Applications"
---

# 5.7 Applications

<div class="info-capitolo" markdown>

**Part 3 · Flows · Chapter 5** · [:material-book-open-variant: Chapter 5: Maximum flow](index.md) · [:material-file-pdf-box: Lecture notes, volume 3 (PDF)](../../pdf/lecture-notes-3-flows.pdf) · [:material-pencil: Exercises: Maximum flow](../../exercises/maximum-flow.md) · [:material-gesture-tap: App: Maximum flow: Ford–Fulkerson and Edmonds–Karp](../../lab/maximum-flow-ford-fulkerson-edmonds-karp.md)

</div>

<a id="sez-sec-mf-applications"></a>
### 5.7.1 Maximum matching in a bipartite graph

<a id="box-24-mf-def-matching"></a>

!!! definizione "Definition 5.16: bipartite graph and matching"

    An undirected graph $H=(V_1 \cup V_2,E)$ is <strong>bipartite</strong> if $V_1$ and $V_2$ are disjoint and every edge has one endpoint in $V_1$ and one in $V_2$; we write the edges as $\{i,j\}$ with $i \in V_1$ and $j \in V_2$.

    - A <strong>matching</strong> is a set $M \subseteq E$ of edges, no two of which have a common endpoint.

    - The <strong>maximum matching problem</strong> asks for a matching with the largest number of edges.

    The <strong>network of $H$</strong> has the nodes $\{s\} \cup V_1 \cup V_2 \cup \{t\}$, the arcs $(s,i)$ for $i \in V_1$, $(i,j)$ for every edge $\{i,j\} \in E$, $(j,t)$ for $j \in V_2$, and all capacities equal to $1$.

- With $V_1$ a set of workers, $V_2$ a set of jobs, and an edge when a worker can do a job, a matching assigns jobs to workers, at most one job per worker and one worker per job.

- In the order of the nodes, $s$ comes first and $t$ last; the other nodes keep their indices.

<a id="box-25-mf-prop-matching"></a>

!!! teorema "Proposition 5.17: matchings and flows"

    The maximum number of edges of a matching of $H$ equals the maximum value $\tilde{v}$ of a flow in the network of $H$. If $\tilde{\vet{x}}$ is an integer maximum flow, then $M=\{\{i,j\} \in E : \tilde{x}_{ij}=1\}$ is a maximum matching.

??? dimostrazione "Proof"

    1. <em>From matchings to flows.</em> Given a matching $M$, set $x=1$ on the arcs $(s,i)$, $(i,j)$, $(j,t)$ of every edge $\{i,j\} \in M$, and $x=0$ elsewhere. Every node of $V_1 \cup V_2$ is an endpoint of at most one edge of $M$, so the flow is feasible, and its value is $|M|$.

    2. <em>From integer flows to matchings.</em> Let $\vet{x}$ be an integer feasible flow, so $x_{ij} \in \{0,1\}$. A node $i \in V_1$ has the single entering arc $(s,i)$, so at most one arc $(i,j)$ carries flow; a node $j \in V_2$ has the single leaving arc $(j,t)$, so at most one arc $(i,j)$ carries flow. Hence $M=\{\{i,j\} : x_{ij}=1\}$ is a matching. For $S=\{s\} \cup V_1$, the forward arcs are the arcs $(i,j)$ and there are no backward arcs: by <span style="color:#1971c2">[Lemma 5.3](cuts.md#box-4-mf-lem-cut)</span>, $v=|M|$.

    3. By <span style="color:#1971c2">[Corollary 5.10](the-ford-fulkerson-algorithm.md#box-15-mf-cor-integral)</span> there is an integer maximum flow $\tilde{\vet{x}}$. By 1, no matching has more than $\tilde{v}$ edges, and by 2 the matching of $\tilde{\vet{x}}$ has $\tilde{v}$ edges. <span class="qed">□</span>

<a id="box-26-mf-ex-matching"></a>

!!! esempio "Example 5.9: workers and jobs"

    Four workers $V_1=\{1,2,3,4\}$ and three jobs $V_2=\{5,6,7\}$ have the edges

    $$
    E=\big\{\{1,5\},\{1,6\},\{2,5\},\{3,6\},\{3,7\},\{4,6\}\big\}.
    $$

    The Edmonds–Karp algorithm on the network of $H$, with the nodes in the order $s,1,2,\dots,7,t$, gives:

    <div class="tabella" markdown="0"><table>
    <tr>
    <th>iteration</th>
    <th>augmenting path</th>
    <th><span class="arithmatex">\(r_{ij}\)</span> on <span class="arithmatex">\(P\)</span></th>
    <th>backward arcs</th>
    <th><span class="arithmatex">\(\delta\)</span></th>
    <th><span class="arithmatex">\(v\)</span></th>
    </tr>
    <tr>
    <td><span class="arithmatex">\(1\)</span></td>
    <td><span class="arithmatex">\(s,1,5,t\)</span></td>
    <td><span class="arithmatex">\(1,1,1\)</span></td>
    <td>–</td>
    <td><span class="arithmatex">\(1\)</span></td>
    <td><span class="arithmatex">\(1\)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">\(2\)</span></td>
    <td><span class="arithmatex">\(s,3,6,t\)</span></td>
    <td><span class="arithmatex">\(1,1,1\)</span></td>
    <td>–</td>
    <td><span class="arithmatex">\(1\)</span></td>
    <td><span class="arithmatex">\(2\)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">\(3\)</span></td>
    <td><span class="arithmatex">\(s,4,6,3,7,t\)</span></td>
    <td><span class="arithmatex">\(1,1,1,1,1\)</span></td>
    <td><span class="arithmatex">\((6,3)\)</span></td>
    <td><span class="arithmatex">\(1\)</span></td>
    <td><span class="arithmatex">\(3\)</span></td>
    </tr>
    </table></div>

    - Iteration $3$ uses the backward arc $(6,3)$: worker $3$ leaves job $6$ for job $7$, and worker $4$ takes job $6$.

    - The maximum matching is $M=\{\{1,5\},\{3,7\},\{4,6\}\}$, with $3$ edges; worker $2$ stays without a job. In the figure the arcs with flow $1$ are blue.

    - At the stop the search labels $S=\{s,1,2,4,5,6\}$; the forward arcs of the cut are $(s,3)$, $(5,t)$, $(6,t)$, with capacity $3=|M|$.

    ![Figure 6](../../img/maximum-flow/fig06.svg){ .fig loading=lazy  }

### 5.7.2 Arc-disjoint paths

- Two directed paths are <strong>arc-disjoint</strong> if they have no common arc; they may share nodes.

<a id="box-27-mf-th-menger"></a>

!!! teorema "Theorem 5.18: Menger, arc version"

    Let $G=(N,A)$ be a directed graph and $s \neq t$ two nodes. The maximum number of pairwise arc-disjoint directed paths from $s$ to $t$ equals the minimum number of arcs whose removal leaves no directed path from $s$ to $t$.

??? dimostrazione "Proof"

    Give every arc the capacity $1$, and let $\tilde{v}$ be the maximum value of a flow.

    1. <em>Paths give flows.</em> The sum of the incidence vectors of $k$ arc-disjoint paths from $s$ to $t$ is a feasible flow of value $k$: every arc carries at most $1$, and every path enters and leaves its inner nodes. Hence $k \le \tilde{v}$.

    2. <em>Flows give paths.</em> By <span style="color:#1971c2">[Corollary 5.10](the-ford-fulkerson-algorithm.md#box-15-mf-cor-integral)</span> there is a flow $\vet{x}$ with $x_{ij} \in \{0,1\}$ and value $\tilde{v}$. If $\tilde{v} \ge 1$, walk from $s$ along arcs with $x_{ij}=1$, each used at most once, until $t$ is reached:

        - at a node $i \notin \{s,t\}$ the walk has used one entering arc more than leaving arcs, and conservation gives an unused leaving arc with flow;

        - at $s$ the walk has used as many leaving arcs as entering ones, while the arcs with flow leaving $s$ are $\tilde{v} \ge 1$ more than those entering: an unused one exists.

        The walk ends, at $t$, and it contains a path $P$ from $s$ to $t$ ([Chapter 1, Lemma «a walk contains a path»](https://fabiofurini.github.io/network-optimization/graphs/graphs/undirected-and-directed-graphs/)). Setting $x_{ij}=0$ on $P$ leaves a $0/1$ flow of value $\tilde{v}-1$; repeating gives $\tilde{v}$ arc-disjoint paths.

    3. <em>Removing arcs.</em> If removing a set $F$ of arcs leaves no path from $s$ to $t$, the set $S$ of the nodes still reachable from $s$ has $t \notin S$ and $\delta^+(S) \subseteq F$, so $|F| \ge u(S,N \setminus S) \ge \tilde{v}$. Conversely, every path from $s$ to $t$ leaves $S$ through an arc of $\delta^+(S)$: removing the $\tilde{v}$ forward arcs of a minimum cut (<span style="color:#1971c2">[Theorem 5.8](the-max-flow-min-cut-theorem.md#box-12-mf-th-mfmc)</span>) leaves no path. <span class="qed">□</span>

<a id="box-28-mf-ex-menger"></a>

!!! esempio "Example 5.10: arc-disjoint paths in the reference graph"

    On the reference graph with all capacities $1$, $s=1$ and $t=6$, the Edmonds–Karp algorithm finds the paths $1,2,4,6$ and $1,3,5,6$, and $\tilde{v}=2$. These two paths are arc-disjoint, and removing the two arcs $(1,2)$, $(1,3)$ leaving node $1$ leaves no path from $1$ to $6$: both numbers of <span style="color:#1971c2">[Theorem 5.18](#box-27-mf-th-menger)</span> are $2$.

!!! chiave ""

    A maximum matching of a bipartite graph is an integer maximum flow in a network with unit capacities, and so are the arc-disjoint paths from $s$ to $t$; the minimum cut certifies both.

## 5.8 Typical mistakes

!!! attenzione "Warning"

    - <strong>Counting the backward arcs of a cut.</strong> The capacity $u(S,N \setminus S)$ adds up only the arcs from $S$ to $N \setminus S$.

    - <strong>Forgetting the backward arcs of the residual network.</strong> With forward arcs only, the method can stop at a flow that is not maximum, as at value $5$ on the reference network.

    - <strong>Giving a backward arc the capacity $u_{ij}$.</strong> The backward arc $(j,i)$ has $r_{ji}=x_{ij}$: only the flow already sent can be sent back.

    - <strong>Taking the bottleneck from the capacities.</strong> The bottleneck is the smallest residual capacity $r_{ij}$ on the path, not the smallest $u_{ij}$.

    - <strong>Adding $\delta$ on a backward arc.</strong> Along a backward arc $(j,i)$ the flow $x_{ij}$ decreases by $\delta$.

    - <strong>Reading the cut from the saturated arcs.</strong> The minimum cut is given by the nodes reachable from $s$ in the residual network at the stop; the saturated arcs need not form a cut.

    - <strong>Calling Ford–Fulkerson polynomial.</strong> Its number of augmentations can grow with the capacities, as $2M$ in <span style="color:#1971c2">[Example 5.7](the-ford-fulkerson-algorithm.md#box-18-mf-ex-bad)</span>; Edmonds–Karp makes at most $n\,m$.

## 5.9 In summary

!!! chiave "In summary"

    - A feasible flow respects the capacities and is conserved at the nodes other than $s$ and $t$; its value is the net outflow of $s$, and it equals the net flow across every $s$–$t$ cut.

    - Weak duality: $v \le u(S,N \setminus S)$ for every flow and every cut.

    - The residual network has forward arcs with $r_{ij}=u_{ij}-x_{ij}$ and backward arcs with $r_{ji}=x_{ij}$; an augmenting path raises the value by its bottleneck $\delta$.

    - Max-flow min-cut: a flow is maximum if and only if no augmenting path exists, and $\tilde{v}$ equals the minimum cut capacity; with integer capacities there is an integer maximum flow.

    - Ford–Fulkerson (depth-first search): with integer capacities at most $\tilde{v}$ augmentations, pseudopolynomial. Edmonds–Karp (breadth-first search): at most $n\,m$ augmentations, $O(n\,m^2)$ time.

    - Maximum matchings in bipartite graphs and arc-disjoint paths are integer maximum flows.

    <strong>The reference network at a glance.</strong>

    <div class="tabella" markdown="0"><table>
    <tr>
    <td>capacities, <span class="arithmatex">\(s=1\)</span>, <span class="arithmatex">\(t=6\)</span></td>
    <td><span class="arithmatex">\(\vet{u}=(5,4,3,2,4,2,4,2,3)\)</span></td>
    </tr>
    <tr>
    <td>maximum flow (unique)</td>
    <td><span class="arithmatex">\(\tilde{\vet{x}}=(3,4,3,0,4,0,4,1,3)\)</span>, <span class="arithmatex">\(\tilde{v}=7\)</span></td>
    </tr>
    <tr>
    <td>minimum cuts, capacity <span class="arithmatex">\(7\)</span></td>
    <td><span class="arithmatex">\(S=\{1,2\}\)</span>, <span class="arithmatex">\(\{1,2,3\}\)</span>, <span class="arithmatex">\(\{1,2,3,4,5\}\)</span></td>
    </tr>
    <tr>
    <td>Ford–Fulkerson (DFS)</td>
    <td><span class="arithmatex">\(5\)</span> augmentations, <span class="arithmatex">\(\delta=2,1,2,1,1\)</span></td>
    </tr>
    <tr>
    <td>Edmonds–Karp (BFS)</td>
    <td><span class="arithmatex">\(3\)</span> augmentations, <span class="arithmatex">\(\delta=3,3,1\)</span></td>
    </tr>
    <tr>
    <td>all capacities <span class="arithmatex">\(1\)</span></td>
    <td>arc-disjoint paths <span class="arithmatex">\(1,2,4,6\)</span> and <span class="arithmatex">\(1,3,5,6\)</span></td>
    </tr>
    </table></div>

---

**Exercises on this chapter:** [:material-pencil: Maximum flow](../../exercises/maximum-flow.md)


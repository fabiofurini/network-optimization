---
title: "The Edmonds–Karp algorithm"
---

# 5.6 The Edmonds–Karp algorithm { #sez-sec-mf-ek }

<div class="info-capitolo" markdown>

**Part 3 · Flows · Chapter 5** · [:material-book-open-variant: Chapter 5: Maximum flow](index.md) · [:material-file-pdf-box: Lecture notes, volume 3 (PDF)](../../pdf/lecture-notes-3-flows.pdf) · [:material-presentation: Slides](../../pdf/slides-maximum-flow.pdf) · [:material-pencil: Exercises: Maximum flow](../../exercises/maximum-flow.md) · [:material-gesture-tap: App: Maximum flow: Ford–Fulkerson and Edmonds–Karp](../../lab/maximum-flow-ford-fulkerson-edmonds-karp.md)

</div>

<a id="box-19-mf-def-ek"></a>

!!! definizione "Definition 5.12: Edmonds–Karp algorithm"

    The <strong>Edmonds–Karp algorithm</strong> is the Ford–Fulkerson algorithm in which Step 1 uses the <strong>breadth-first search</strong>: $\mathit{LIST}$ is a queue, the residual arcs leaving each node are scanned by increasing index of the head, and the search stops as soon as $t$ is labelled. The capacities are any non-negative real numbers.

- By [Chapter 1, Proposition «BFS finds shortest paths in number of arcs»](https://fabiofurini.github.io/network-optimization/graphs/graphs/graph-search/), the augmenting path has the minimum number of arcs among the paths from $s$ to $t$ in $G(\vet{x})$.

- For a feasible flow $\vet{x}$ and a node $i$, $d_{\vet{x}}(i)$ is the minimum number of arcs of a path from $s$ to $i$ in $G(\vet{x})$, and $d_{\vet{x}}(i)=+\infty$ if $i$ is not reachable.

- An arc of the augmenting path is <strong>critical</strong> if its residual capacity equals $\delta$: after the augmentation its residual capacity is zero, and it leaves the residual network.

- An augmentation along $P$ lowers $r_{ij}$ by $\delta$ and raises $r_{ji}$ by $\delta$ on every arc $(i,j)$ of $P$, and changes no other residual capacity. Hence the arcs that enter the residual network are reverses of arcs of $P$.

<a id="box-20-mf-lem-dist"></a>

!!! teorema "Lemma 5.13: the distances do not decrease"

    Let $\vet{x}'$ be obtained from $\vet{x}$ by an augmentation along a path $P$ from $s$ to $t$ of $G(\vet{x})$ with the minimum number of arcs. Then $d_{\vet{x}'}(i) \ge d_{\vet{x}}(i)$ for every $i \in N$.

??? dimostrazione "Proof"

    We show that every arc $(a,b)$ of $G(\vet{x}')$ satisfies $d_{\vet{x}}(b) \le d_{\vet{x}}(a)+1$.

    1. If $(a,b)$ is an arc of $G(\vet{x})$, a shortest path from $s$ to $a$ followed by $(a,b)$ reaches $b$ with $d_{\vet{x}}(a)+1$ arcs.

    2. Otherwise $(a,b)$ is the reverse of an arc $(b,a)$ of $P$. The part of $P$ from $s$ to each of its nodes has the minimum number of arcs: a path to that node with fewer arcs, followed by the rest of $P$, would give a walk from $s$ to $t$ with fewer arcs than $P$, and a path inside it ([Chapter 1, Lemma «a walk contains a path»](https://fabiofurini.github.io/network-optimization/graphs/graphs/undirected-and-directed-graphs/)). Hence $d_{\vet{x}}(a)=d_{\vet{x}}(b)+1$, and $d_{\vet{x}}(b) \le d_{\vet{x}}(a)+1$.

    Now let $s=i_0,i_1,\dots,i_q=i$ be a path of $G(\vet{x}')$ with $q=d_{\vet{x}'}(i)$ arcs. Along its arcs $d_{\vet{x}}$ grows by at most $1$ at a time, so $d_{\vet{x}}(i) \le d_{\vet{x}}(s)+q=d_{\vet{x}'}(i)$. If $i$ is not reachable in $G(\vet{x}')$, then $d_{\vet{x}'}(i)=+\infty$. <span class="qed">□</span>

<a id="box-21-mf-lem-critical"></a>

!!! teorema "Lemma 5.14: critical arcs"

    In the Edmonds–Karp algorithm, let the residual arc $(i,j)$ be critical in the augmentation at the flow $\vet{x}$, and critical again in a later augmentation at the flow $\vet{y}$. Then $d_{\vet{y}}(i) \ge d_{\vet{x}}(i)+2$.

??? dimostrazione "Proof"

    We apply <span style="color:#1971c2">[Lemma 5.13](#box-20-mf-lem-dist)</span> at every augmentation between $\vet{x}$ and $\vet{y}$.

    1. At $\vet{x}$, the arc $(i,j)$ lies on a path with the minimum number of arcs, so $d_{\vet{x}}(j)=d_{\vet{x}}(i)+1$; after the augmentation $r_{ij}=0$.

    2. At $\vet{y}$ the arc $(i,j)$ is back in the residual network, so some augmentation in between, at a flow $\vet{z}$, raised $r_{ij}$: its path used the reverse arc $(j,i)$, and $d_{\vet{z}}(i)=d_{\vet{z}}(j)+1$.

    3. The distances never decrease, so $d_{\vet{z}}(j) \ge d_{\vet{x}}(j)$ and $d_{\vet{y}}(i) \ge d_{\vet{z}}(i)$. Hence

        $$
        d_{\vet{y}}(i) \ge d_{\vet{z}}(i)=d_{\vet{z}}(j)+1 \ge d_{\vet{x}}(j)+1=d_{\vet{x}}(i)+2 .
        $$

    <p class="qed-riga"><span class="qed">□</span></p>

<a id="box-22-mf-th-ek"></a>

!!! teorema "Theorem 5.15: running time of Edmonds–Karp"

    For any non-negative capacities, the Edmonds–Karp algorithm stops after at most $n\,m$ augmentations with a maximum flow and a minimum cut, and it runs in $O(n\,m\,(n+m))$ time, that is $O(n\,m^2)$ when $m \ge n-1$.

??? dimostrazione "Proof"

    1. Every augmentation has at least one critical arc: an arc of $P$ whose residual capacity equals $\delta$.

    2. When $(i,j)$ is critical, $i$ lies before $t$ on a path from $s$ to $t$ with at most $n-1$ arcs, so $0 \le d(i) \le n-2$. By <span style="color:#1971c2">[Lemma 5.14](#box-21-mf-lem-critical)</span> this distance grows by at least $2$ between two critical times, so $(i,j)$ is critical at most $\lfloor \frac{n-2}{2} \rfloor+1 \le \frac{n}{2}$ times.

    3. Every residual arc is $(i,j)$ or $(j,i)$ for an arc $(i,j) \in A$: there are at most $2m$ of them, and at most $2m \cdot \frac{n}{2}=n\,m$ augmentations.

    4. Every iteration takes $O(n+m)$ time, as in <span style="color:#1971c2">[Theorem 5.11](the-ford-fulkerson-algorithm.md#box-16-mf-th-ff-time)</span>. At the stop $G(\vet{x})$ has no augmenting path, and <span style="color:#1971c2">[Theorem 5.8](the-max-flow-min-cut-theorem.md#box-12-mf-th-mfmc)</span> applies as in the proof of <span style="color:#1971c2">[Theorem 5.9](the-ford-fulkerson-algorithm.md#box-14-mf-th-ff)</span>. <span class="qed">□</span>

- The bound depends only on $n$ and $m$, not on the capacities: the Edmonds–Karp algorithm is <strong>strongly polynomial</strong>, and it stops also with irrational capacities.

## 5.6.1 Edmonds–Karp on the reference network

<a id="box-23-mf-ex-ek"></a>

!!! esempio "Example 5.8: Edmonds–Karp on the reference network"

    We run the algorithm on the network of <span style="color:#1971c2">[Example 5.1](the-maximum-flow-problem.md#box-2-mf-ex-ref)</span>; the column «arcs» is the number of arcs of the augmenting path.

    <div class="tabella" markdown="0"><table>
    <tr>
    <th>iteration</th>
    <th>augmenting path</th>
    <th>arcs</th>
    <th><span class="arithmatex">\(r_{ij}\)</span> on <span class="arithmatex">\(P\)</span></th>
    <th>backward arcs</th>
    <th><span class="arithmatex">\(\delta\)</span></th>
    <th><span class="arithmatex">\(v\)</span></th>
    </tr>
    <tr>
    <td><span class="arithmatex">\(1\)</span></td>
    <td><span class="arithmatex">\(1,2,4,6\)</span></td>
    <td><span class="arithmatex">\(3\)</span></td>
    <td><span class="arithmatex">\(5,3,4\)</span></td>
    <td>–</td>
    <td><span class="arithmatex">\(3\)</span></td>
    <td><span class="arithmatex">\(3\)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">\(2\)</span></td>
    <td><span class="arithmatex">\(1,3,5,6\)</span></td>
    <td><span class="arithmatex">\(3\)</span></td>
    <td><span class="arithmatex">\(4,4,3\)</span></td>
    <td>–</td>
    <td><span class="arithmatex">\(3\)</span></td>
    <td><span class="arithmatex">\(6\)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">\(3\)</span></td>
    <td><span class="arithmatex">\(1,3,5,4,6\)</span></td>
    <td><span class="arithmatex">\(4\)</span></td>
    <td><span class="arithmatex">\(1,1,2,1\)</span></td>
    <td>–</td>
    <td><span class="arithmatex">\(1\)</span></td>
    <td><span class="arithmatex">\(7\)</span></td>
    </tr>
    </table></div>

    The distances $d_{\vet{x}}(i)$ in the residual network before each search are:

    <div class="tabella" markdown="0"><table>
    <tr>
    <th>iteration</th>
    <th><span class="arithmatex">\(d(1)\)</span></th>
    <th><span class="arithmatex">\(d(2)\)</span></th>
    <th><span class="arithmatex">\(d(3)\)</span></th>
    <th><span class="arithmatex">\(d(4)\)</span></th>
    <th><span class="arithmatex">\(d(5)\)</span></th>
    <th><span class="arithmatex">\(d(6)\)</span></th>
    </tr>
    <tr>
    <td><span class="arithmatex">\(1\)</span></td>
    <td><span class="arithmatex">\(0\)</span></td>
    <td><span class="arithmatex">\(1\)</span></td>
    <td><span class="arithmatex">\(1\)</span></td>
    <td><span class="arithmatex">\(2\)</span></td>
    <td><span class="arithmatex">\(2\)</span></td>
    <td><span class="arithmatex">\(3\)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">\(2\)</span></td>
    <td><span class="arithmatex">\(0\)</span></td>
    <td><span class="arithmatex">\(1\)</span></td>
    <td><span class="arithmatex">\(1\)</span></td>
    <td><span class="arithmatex">\(3\)</span></td>
    <td><span class="arithmatex">\(2\)</span></td>
    <td><span class="arithmatex">\(3\)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">\(3\)</span></td>
    <td><span class="arithmatex">\(0\)</span></td>
    <td><span class="arithmatex">\(1\)</span></td>
    <td><span class="arithmatex">\(1\)</span></td>
    <td><span class="arithmatex">\(3\)</span></td>
    <td><span class="arithmatex">\(2\)</span></td>
    <td><span class="arithmatex">\(4\)</span></td>
    </tr>
    <tr>
    <td>stop</td>
    <td><span class="arithmatex">\(0\)</span></td>
    <td><span class="arithmatex">\(1\)</span></td>
    <td><span class="arithmatex">\(\infty\)</span></td>
    <td><span class="arithmatex">\(\infty\)</span></td>
    <td><span class="arithmatex">\(\infty\)</span></td>
    <td><span class="arithmatex">\(\infty\)</span></td>
    </tr>
    </table></div>

    - Iteration $1$ is the breadth-first search of [Chapter 1, Example «BFS from node $1$»](https://fabiofurini.github.io/network-optimization/graphs/graphs/graph-search/), whose tree path to node $6$ is $1,2,4,6$.

    - The critical arcs are $(2,4)$ in iteration $1$, $(5,6)$ in iteration $2$, and $(1,3)$, $(3,5)$, $(4,6)$ in iteration $3$. When $(2,4)$ leaves the residual network, $d(4)$ grows from $2$ to $3$; no distance ever decreases.

    - The algorithm needs $3$ augmentations, against the $5$ of <span style="color:#1971c2">[Example 5.6](the-ford-fulkerson-algorithm.md#box-17-mf-ex-ff)</span>, far below the bound $n\,m=54$. It ends with the same maximum flow $\tilde{\vet{x}}$, the unique one, and the same cut $S=\{1,2\}$.

    - On the network of <span style="color:#1971c2">[Example 5.7](the-ford-fulkerson-algorithm.md#box-18-mf-ex-bad)</span> the breadth-first search finds $1,2,4$ and then $1,3,4$, each with $\delta=M$: two augmentations for every $M$.

!!! chiave ""

    The Edmonds–Karp algorithm augments along paths with the fewest arcs, found by the breadth-first search. The distances from $s$ in the residual network never decrease, every arc is critical at most $\frac{n}{2}$ times, and the algorithm makes at most $n\,m$ augmentations: $O(n\,m^2)$ time, for any capacities.

---

**Next:** [5.7 Applications](applications.md)

---
title: "Paths and critical paths"
---

# 9.2 Paths and critical paths { #sez-pm-sec-paths }

<div class="info-capitolo" markdown>

**Part 5 · Project management · Chapter 9** · [:material-book-open-variant: Chapter 9: Project management](index.md) · [:material-file-pdf-box: Lecture notes, volume 5 (PDF)](../../pdf/lecture-notes-5-project-management.pdf) · [:material-pencil: Exercises: Project management](../../exercises/project-management.md)

</div>

- Under (H1) and (H2), the critical path method answers the following questions.

    1. What is the minimum time required to complete the project?

    2. When can each activity start and finish at the earliest?

    3. When must each activity start and finish at the latest, so as not to delay the completion of the project?

    4. Which activities are critical, so that any delay on them delays the project?

    5. For the other activities, how much delay can be tolerated?

<a id="box-6-pm-def-critical"></a>

!!! definizione "Definition 9.5: length of a path and critical path"

    Every arc $(i,j) \in A$ has the <strong>length</strong> $d_i$, the duration of its tail. The <strong>length</strong> of a directed path $P=i_0,i_1,\dots,i_k$ is

    $$
    L(P)=\sum_{s=0}^{k-1} d_{i_s},
    $$

    the total duration of its nodes except the last one. A <strong>critical path</strong> is a path from START to FINISH of maximum length. An activity is <strong>critical</strong> if it lies on a critical path.

- On a path from START to FINISH the durations of the first and the last node are zero: $L(P)$ is the total duration of the activities of the path.

- A project can have several critical paths: when several paths tie for the maximum length, they are all critical.

<a id="box-7-pm-lem-path"></a>

!!! teorema "Lemma 9.6: every path bounds the duration"

    For every schedule $\vet{t}$ and every path $P$ from START to FINISH, $t_{n+1} \ge L(P)$.

??? dimostrazione "Proof"

    Let $P=i_0,i_1,\dots,i_k$ with $i_0=0$ and $i_k=n+1$. Adding up the constraints $t_{i_{s+1}} \ge t_{i_s}+d_{i_s}$ of the arcs of $P$, the start times telescope:

    $$
    t_{n+1}-t_0 \ge \sum_{s=0}^{k-1} d_{i_s}=L(P),
    $$

    and $t_0=0$. <span class="qed">□</span>

- The activities of a path must be done one after the other, without overlap: the project cannot be shorter than any path.

<a id="box-8-pm-ex-paths"></a>

!!! esempio "Example 9.2: the paths of the case study"

    The network of <span style="color:#1971c2">[Example 9.1](projects-and-project-networks.md#box-3-pm-ex-case)</span> has six paths from START to FINISH; their lengths, in weeks, are:

    <div class="tabella" markdown="0"><table>
    <tr>
    <th>path from START to FINISH</th>
    <th>length (weeks)</th>
    </tr>
    <tr>
    <td><span class="arithmatex">\(\text{START},1,2,3,4,7,8,13,\text{FINISH}\)</span></td>
    <td><span class="arithmatex">\(2+4+10+6+7+9+2=40\)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">\(\text{START},1,2,3,5,6,10,11,14,\text{FINISH}\)</span></td>
    <td><span class="arithmatex">\(2+4+10+4+5+8+4+6=43\)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">\(\text{START},1,2,3,5,6,10,12,14,\text{FINISH}\)</span></td>
    <td><span class="arithmatex">\(2+4+10+4+5+8+5+6=44\)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">\(\text{START},1,2,3,5,8,13,\text{FINISH}\)</span></td>
    <td><span class="arithmatex">\(2+4+10+4+9+2=31\)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">\(\text{START},1,2,3,9,10,11,14,\text{FINISH}\)</span></td>
    <td><span class="arithmatex">\(2+4+10+7+8+4+6=41\)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">\(\text{START},1,2,3,9,10,12,14,\text{FINISH}\)</span></td>
    <td><span class="arithmatex">\(2+4+10+7+8+5+6=42\)</span></td>
    </tr>
    </table></div>

    - The longest path is START$,1,2,3,5,6,10,12,14,$FINISH, of length $44$: by <span style="color:#1971c2">[Lemma 9.6](#box-7-pm-lem-path)</span>, every schedule lasts at least $44$ weeks.

    - The project can last more than a given path. On the path START$,1,2,3,5,8,13,$FINISH, of length $31$, activity $8$ waits for activity $5$, which can finish at week $2+4+10+4=20$, but also for activity $7$, which is not on the path and cannot finish before week $2+4+10+6+7=29$.

!!! attenzione "The number of paths"

    Listing the paths does not work on large projects: their number can grow exponentially with $n$. A sequence of $k$ pairs of parallel activities, each pair after the previous one, has $2^k$ paths from START to FINISH. The critical path method finds the length of a longest path without listing the paths.

!!! chiave ""

    The length of a path from START to FINISH is the total duration of its activities. Every schedule lasts at least as long as every such path; the critical paths are the longest ones.

---

**Next:** [9.3 The forward pass: earliest times](the-forward-pass-earliest-times.md)

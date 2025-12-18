---
title: "On random trees with limited information"
draft: false
date: 2025-12-01
summary: "Post on Random Trees with limited memory"
layout: "simple"
---

{{< katex >}}

{{< katex >}}

On this post I intend to present some thoughts I have gathered when coming across [^neeladri]. How I found that paper is a good starting point. I had the idea of representing the network of “Mathematics”, its own fields and how they are connected. The initial objective was to portray the obvious idea that not even Mathematics escape trends. You can find the product of those thoughts in the miscellaneous section.

However, when working with Wikipedia as a network, I observed that the “relevant” information, i.e., the information that “matters” when introducing a new vertex, was diluting when increasing the graph size: new vertices rarely linked with old vertices. Obviously there is some fault in how I designed the algorithm and structured the network exploration. Nevertheless, there was something mathematically interesting under it. Thus, I searched on arXiv for the latest preprints on this topic and found [^neeladri].

Let’s lay down some groundwork:

We denote \(\{\mathcal{T}_n : n \geq 1\}\) a sequence of trees, and \(B(T,r)\) the tree up to distance \(r\) from the root. Unfortunately they denote \(\mathbb{T}\) the space of $\textbf{finite}$ trees; one accustomed to other fields might see the circle. This space is endowed with the following distance. For \(t,s \in \mathbb{T}\),

\[
d(t,s) := \frac{1}{1 + R^*}
\qquad
R^* = \sup\{ r : B(t,r) \sim B(s,r) \}.
\]

<div style="display:flex; justify-content:center; gap:1rem; flex-wrap:wrap;">

  {{< figure src="/images/Images/tree-avocado.png" alt="Tree 1" caption="t" >}}

  {{< figure src="/images/Images/output_2.png" alt="Tree 2" caption="s" >}}

</div>

On that figure, clearly \(d_{\mathbb{T}}(t,s)=1\) because even at distance \(1\) from the root they are not isomorphic. This also tells us that \(d_{\mathbb{T}}(t,s) \leq 1\) for any \(t,s \in \mathbb{T}\). One must note that, thanks to the supremum, we can achieve distance \(0\): if \(t,s\) are both isomorphic up to their maximal distance, i.e. their height, say \(n\), then they are also isomorphic up to \(n+1\).

Now a concept central to everything we will work on later is the decomposition of a tree into its subtrees, or fringes. Given a walk inside the tree \(t\) from vertex to root,
\((v_0, v_1, \dots, v_h = \rho)\), we can decompose the tree uniquely into \(h+1\) trees
\(f_0(v,t), \dots, f_h(v,t)\), where \(f_i(v,t)\) is the tree rooted at \(v_i\) with all the vertices for which there exists a walk in \(t\) from the root passing through \(v_i\) but not \(v_{i-1}\). This is just the mathematical way of partitioning the tree from bottom to top. A representation is due:

<div style="display:flex; justify-content:center; gap:1rem; flex-wrap:wrap;">

  {{< figure src="/images/Images/output_3.png" alt="Tree 1" caption="Tree" >}}

</div>
If we take the penultimate vertex from the right and take the unique path to the root, the fringe decomposition would be the following
<div style="display:flex; justify-content:center; gap:1rem; flex-wrap:wrap;">

  {{< figure src="/images/Images/f_0.png" alt="Tree 1" caption="f_0" width="70">}}
  {{< figure src="/images/Images/f_1.png" alt="Tree 1" caption="f_1" width="70">}}
</div>
<div style="display:flex; justify-content:center; gap:1rem; flex-wrap:wrap;">

  {{< figure src="/images/Images/f_2.png" alt="Tree 1" caption="f_2" width="70">}}
  {{< figure src="/images/Images/f_3.png" alt="Tree 1" caption="f_3" width="70">}}
</div>

Now, if we take each $f_i$ and join their roots in order we would recover the original tree.

We now formalise these ideas with the space of sequences of trees and the notion of fringe decomposition.

Let \(\mathbb{T}\) be the space of finite rooted trees equipped with the metric \(d_{\mathbb{T}}\) defined above, and let
\[
\mathbb{T}^{\infty}
:= \big\{ (t_0,t_1,\dots) : t_i \in \mathbb{T} \text{ for all } i \ge 0 \big\}
\]
be the space of sequences of finite trees.

Given a rooted tree \(t \in \mathbb{T}\) and a vertex \(v\) of \(t\), we define the **fringe decomposition** of \(t\) along the path from \(v\) to the root by
\[
F(v,t)
  = \bigl( f_0(v,t),f_1(v,t),\dots,f_h(v,t),\varnothing,\varnothing,\dots \bigr)
  \in \mathbb{T}^{\infty},
\]
where \(f_i(v,t)\) is the subtree of \(t\) rooted at the \(i\)-th vertex on the (unique) path from \(v\) to the root, and \(h\) is the length of that path.  

For \(k \ge 0\) we write
\[
F_k(v,t)
  := \bigl( f_0(v,t),\dots,f_k(v,t),\varnothing,\varnothing,\dots \bigr),
\]
and we call \(f_0(v,t)\) the **fringe of \(t\) at \(v\)**.

On \(\mathbb{T}^{\infty}\) we extend the metric \(d_{\mathbb{T}}\) by
\[
d_{\mathbb{T}^{\infty}} \bigl( (t_0,t_1,\dots),(s_0,s_1,\dots) \bigr)
  := \sum_{i=0}^{\infty} \frac{1}{2^{i}}\, d_{\mathbb{T}}(t_i,s_i).
\]

An element
\[
\omega = (t_0,t_1,\dots) \in \mathbb{T}^{\infty}
\quad\text{with}\quad |t_i| \ge 1 \text{ for all } i \ge 0
\]
can be viewed as a locally finite infinite rooted tree with a unique infinite path, in the following way.  


To obtain the infinite tree, identify the collection of fringes \(\{t_i : i \ge 0\}\) with the positive integers \(\mathbb{Z}_+\) and add nearest–neighbour edges between the roots of \(t_i\) and \(t_{i+1}\) for each \(i \ge 0\). In other words, we join the roots of the fringes along a single infinite ray
\[
t_0 \text{ -- } t_1 \text{ -- } t_2 \text{ -- } \cdots ,
\]
and attach each finite tree \(t_i\) at its root. The resulting object is an infinite, locally finite tree with a **unique infinite path**.

For each \(k\) we may look at the truncated sequence
\[
F_k(0,\omega) = (t_0,\dots,t_k),
\]
and we call \(t_0\) the **fringe of the sin-tree** associated with \(\omega\).

## Intro ##

Now, after we have the basics of the $\mathbb{T}$ space, we can state their model and how it differs the classical uniform tree.
They construct a sequence of trees $\{\mathcal{T}_n\}$ in the following way:

* $\mathcal{T}_1$ is the root
* Each $n$ we add a vertex and assign the edge $e_{n,k}$ uniformly following
\[\mathbb{P}(k=v)=1_{\{j(n)\leq v \leq n\}}\]
where $j(n): \mathbb{N}\rightarrow \mathbb{N}$ non-decreasing function such that $j(n)\leq n \: \forall n\geq 1$.

One must think of the function $j(n)$ as dilution of information I mentioned on the intro.


***Observation***

* The original paper has a $f(D_n(v))$ function in front of the indicator for the cases when one want to take into account the degree of the vertex.
* Also, note that taking $j(n)=1$ is just the standard random tree.


The paper consider the following functions
\[j(n)=\lfloor \beta n\rfloor \qquad j(n)=n-\lfloor n^{\beta} \rfloor\]
with $\beta\in (0,1)$.
In order to understand what the paper problem is, let's first do some simulations. In order,

<div style="display:flex; justify-content:center; gap:1rem; flex-wrap:wrap;">

  {{< figure src="/images/Images/Tree_snap.png" alt="Tree 1" caption="$\beta=0.3$" >}}
  {{< figure src="/images/Images/Tree_snap2.png" alt="Tree 1" caption="$\beta=0.7$">}}
</div>

This regime looks quite like a standard uniform random tree. However, 

<div style="display:flex; justify-content:center; gap:1rem; flex-wrap:wrap;">

  {{< figure src="/images/Images/Tree_snap3.png" alt="Tree 1" caption="$\beta=0.3$" >}}
  {{< figure src="/images/Images/Tree_snap4.png" alt="Tree 1" caption="$\beta=0.7$">}}
</div>

There is a major change in geometry, one would suspect there is a phase transition in $\beta=0.5$. The whole objective of their paper is to understand these processes when $n\rightarrow \infty$. But for us to even approach that, we should first understand how or to what can a sequence of trees converge.

## Convergence on the space of trees

Let \(\{\mathcal{T}_n\}_{n\ge 1}\) be a sequence of rooted trees. For \(n\ge 1\) and each fixed \(k\ge 0\), we define the empirical distribution of the fringes up to distance \(k\) by  
\[
\mathcal{B}_n^{(k)}
  := \frac{1}{n}\sum_{v\in \mathcal{T}_n}
      \delta_{F_k\bigl(v,\mathcal{T}_n\bigr)}.
\]

Thus \(\{\mathcal{B}_n^{(k)}\}_{n\ge 1}\) can be viewed as a sequence of random probability measures on the space \(M(\mathbb{T}^k)\).

Fix a probability measure \(\omega\) on \(\mathbb{T}\).

* We say that the sequence of trees \(\{ \mathcal{T}_n \}\) **converges in expectation in the fringe sense** to \(\omega\) if
  \[
  \mathbb{E}\bigl[\mathcal{B}_n^{(0)}\bigr]\;\to\; \omega
  \qquad\text{as } n\to\infty.
  \]

* We say that \(\{\mathcal{T}_n\}\) **converges in probability in the fringe sense** to \(\omega\) if
  \[
  \mathcal{B}_n^{(0)} \;\to\; \omega
  \]
  in probability, with respect to the weak topology on measures (Portmanteau).

* We say that \(\{\mathcal{T}_n\}\) **converges in probability in the extended fringe sense** to a limiting infinite random sin-tree \(\mathcal{T}_\infty\) if, for all \(k\ge 0\),
  \[
  \mathcal{B}_n^{(k)}
    \;\to\;
    \mathbb{P}\bigl(F_k(0,\mathcal{T}_\infty)\in \cdot\bigr),
  \]
  again in the weak sense, taking the right-hand side as a probability measure on \(\mathbb{T}^k\).

It is immediate that if we take the fixed measure \(\omega\) to be the law of the fringe of \(\mathcal{T}_\infty\) on \(\mathbb{T}\), that is
\[
\omega(\cdot)
  = \mathbb{P}\bigl(F_0(0,\mathcal{T}_\infty)\in \cdot\bigr),
\]
then convergence in the extended fringe sense implies convergence in probability in the fringe sense.

Aldous developed the general theory of fringe distributions [^aldous] and many related results; his work on extremal points of the corresponding space of measures is particularly powerful. We will later use that, in fact, if one works with an extremal distribution (in terms of point inside said convex space), convergence in means is sufficient. 

## Results

Here I state the two results that interest me most.

**Result 1.**  
For the case \(j(n)=\lfloor \beta n\rfloor\) with \(\beta\in(0,1)\), the sequence \(\{\mathcal{T}_n\}\) converges in the extended fringe sense to a distribution \(\omega_\beta\).

Here \(\omega_\beta\) is the distribution of the standard branching process driven by a Poisson process \(N_\beta\) with rate \((1-\beta)^{-1}\) on the time interval \([0,\log(\beta^{-1})]\), observed at a random time \(T_1\), where \(T_1\sim \mathrm{Exp}(1)\).

The mere fact that one can write down the limiting distribution explicitly is, to me, quite striking.

**Result 2.**  
For the case \(j(n)=n-\lfloor \beta n\rfloor\) with \(\beta\in(0,1)\), the sequence \(\{\mathcal{T}_n\}\) converges in the extended fringe sense to the unique infinite sin-tree whose fringe distribution is \(\omega_{P,1}\).

The measure \(\omega_{P,1}\) is the law of a standard critical Galton–Watson branching process with Poisson offspring distribution of mean \(1\). Notice that this limit is **independent of \(\beta\)**, and in fact coincides with the local weak limit of a uniform random tree.

One might suspect that this contradicts the geometric differences we observed earlier, but these are **local** results. In fact, they covered the global geometry and phase transitions in a topological framework (via Gromov–Hausdorff convergence).

## Outline proof 1 ##

We call \(T_k^n\) the time at which the \(k\)-th child of vertex \(n\) arrives; i.e.
\[
T_k^n := \inf\{\ell : \deg(n,\mathcal{T}_\ell) = k+1\},
\]
and \(\rho_j^n\) the \(j\)-th vertex in the fringe of \(n\).

We then define, for \(j\ge 0\) and \(k\ge 1\),
\[
T_{j,k}^n := T_k^{\rho_j^n},
\qquad
\tau_{j,k}^n := \log\!\left(\frac{T_{j,k}^n}{T_{j,k-1}^n}\right),
\]
the arrival time between \(k-1\) and \(k\) inside the fringe of \(\rho_j^n\).

They show, with some effort, that
\[
\bigl((\tau_{j,k}^n),\: j\geq 0\bigr)
\;\xrightarrow{d}\;
\bigl((\mathcal{E}_ {j,k}), \:j\geq 0 \bigr),
\]
where \(\mathcal{E}_ {j,k}\) are the arrival times of \(N_\beta\).

In fact, if we consider our process in logarithmic time, vertex \(j\ge 2\) appears at time \(\log j\), and a uniformly chosen vertex appears at time
\[
\log n - \log \lfloor nU\rfloor,
\]
where \(U\sim \mathrm{Unif}(0,1)\).

We now rely on the following construction. Given \(t\in\mathbb{R}_+\) and \(w\in\mathbb{R}^{\mathbb{N}\times\mathbb{N}}\) we can construct a finite tree
\[
\mathbf{T}(t,w)\in\mathbb{T}
\]
by taking, for \(j>0\), \(k\ge 1\), that \(w_{j,k}\) is the age of vertex \(j\) when its \(k\)-th child is born.

We keep all vertices that satisfy \(w_{j,k}\le t\). For \(0\le j\le \mathbf{T}(t,w)\) we denote by \(\tau_j(t,w)\) the birth time of the \(j\)-th vertex of \(\mathbf{T}(t,w)\) and set
\[
n(t,w) := \sup\{j\ge 0 : \tau_j(t,w)\le t\},
\]
the last vertex we have with birth time less than \(t\), i.e. the height.

We define
\[
\mathbf{W} := \{(t,w) : n(t,w)<\infty,\ \tau_{j}(t,w)\neq t\},
\]
and thus \(\mathbf{T}:\mathbf{W}\to\mathbb{T}\) is continuous.

Applying this to the discrete construction above, we can write the fringe of a uniformly chosen vertex \(\ell\) as
\[
\mathbf{T}\bigl(\log n - \log \lfloor nU\rfloor,\; W^{\lfloor nU\rfloor}\bigr),
\]
where \(W^{\lfloor nU\rfloor}\) is the matrix formed by the \(\tau^{\lfloor nU\rfloor}_{j,k}\).

By the convergence of the inter-arrival times,
\[
\bigl(\log n - \log \lfloor nU\rfloor,\; W^{\lfloor nU\rfloor}\bigr)
\;\xrightarrow{d}\;
\bigl(T_1, W^*\bigr),
\]
where \(T_1\sim\mathrm{Exp}(1)\) and \(W^*\) is the matrix associated to \((\mathcal{E}_ {j,k})\). By the continuous mapping theorem,
\[
\mathbf{T}\bigl(\log n - \log \lfloor nU\rfloor,\; W^{\lfloor nU\rfloor}\bigr)
\;\xrightarrow{d}\;
\mathbf{T}(T_1,W^*),
\]
which has distribution \(\omega_\beta\).


## Outline proof 2 ##

Again the idea is to approximate the discrete tree using a continuous time branching process. In fact, what we approximate is the BFS of the fringe of a vertex in the \(\mathcal{T}_ n\).

A lemmas is needed, approximate de degree of vertex \(j\) at time \(n \equiv D_{j,n}\) by a \(Poiss(1)\).

**Lemma.** Let \(D_{j,n}\) as before. For any \(\delta>1\), there exists \(j_0\) such that

\[
d\bigl(D_{j,n}, \text{Pois}(1)\bigr)
\le
\delta\bigl(1-(1+\delta j^{\beta-1})^{-\beta}\bigr)+\delta j^{-\beta}
+\max(\delta-1, j^{-\beta})
+\mathbf{1}_{\{N_j \ge n-j\}}
\left|\frac{n-j}{j^\beta}-1\right|,
\]
where \(d\) is just the total variation distance between distributions and
\[
N_j := |\{i : i-i^\beta \le j < i\}|.
\]

In order to proceed we need to understand \(N_j\). Recall that we are under the regime \(j(n)=n-\lfloor n^\beta \rfloor\) so \(N_j\) just tells us the amount of vertices that have access to \(j\). Thus also tells us the max possible vertex that could reach \(j\).

Now, the expression above just partition the cases on whether the vertex \(j\) is reachable at time \(n\), \(N_j \le n\) or not. We first need to understand some properties of \(N_j\).

**Lemma.** We have  

i) \(N_j \ge j^{\beta}-1\), \(j>1\).  

ii) For any \(\delta>1\), there exists \(j_0>1\) such that
\[
N_j \le \delta j^\beta \qquad \forall j\ge j_0.
\]

Proving this is almost immediate.

For i) just note that \(\lfloor j^\beta\rfloor \le (j+\lfloor j^\beta\rfloor)^\beta\) because
\(\lfloor j^\beta\rfloor \le \lfloor j\rfloor ^{\beta}\) and \( \lfloor j\rfloor \le j+\lfloor j^\beta\rfloor\).

Thus,
\[
(j+\lfloor j^\beta\rfloor) - (j+\lfloor j^\beta\rfloor)^\beta \le j,
\]
and because \(N_j\) is the biggest index such that \(i-i^\beta \le j\) we have
\[
N_j \ge j+\lfloor j^\beta\rfloor \ge j^\beta-1.
\]

For (ii) the argument is quite amusing. If
\[
(j+\delta j^\beta) - (j+\delta j^\beta)^\beta \le j,
\]
then
\[
\delta = (1+\delta j^{\beta-1})^{-\beta}.
\]
When \(j\to\infty\) the right side tends to \(1\).

Hence if \(\delta>1\) there must be a \(j_0\) such that
\[
(j_0+\delta j_0^\beta) - (j_0+\delta j_0^\beta)^\beta \ge j_0.
\]
\(\Rightarrow \delta j_0^\beta > N_j \quad \forall j\ge j_0.\)

---

Now the proof of the original lemma follows.

Taking \(j\leq i \)
\[
Y_{i,j} = \mathbf{1}_{\{ i \text{ connects to } j \}}.
\]
Thus,
\[
Y_{i,j} \equiv \text{Ber}\!\left(\frac{\mathbf{1}_{\{i-i^\beta \le j\}}}{i^\beta}\right)
\]
because the positive case is when \(i-i^\beta\le j\) and the total possibilities are \((i-(i-i^\beta))=i^\beta\).

Also take
\[
N_{j,n} = \min\{N_j,\, n-j\}.
\]

We approximate the degree summing up these Bernoullis, thus using the lemma we state that for \(j\) large enough, we can bound the "error" by
\[
d\bigl(D_{j,n}, \text{Bin}(N_{j,n}, j^{-\beta})\bigr)
\le
\sum_i \mathbf{1}_{\{i-i^\beta \le j\}}
\left| j^{-\beta} - i^{-\beta} \right|
\le
N_{j,n}\left| j^{-\beta} - (j+\delta j^\beta)^{-\beta} \right|
\le
\delta\bigl(1-(1+\delta j^{\beta-1})^{-\beta}\bigr).
\]

Now we approximate the binomial with a Poisson(1):
\[
d\bigl(\text{Bin}(N_{j,n}, j^{-\beta}), \text{Poiss}(1)\bigr)
\le
d\!\left(\text{Bin}(N_{j,n}, j^{-\beta}), \text{Poiss}\!\left(\frac{N_{j,n}}{j^\beta}\right)\right)
+
d\!\left(\text{Poiss}\!\left(\frac{N_{j,n}}{j^\beta}\right), \text{Poiss}(1)\right)
\]
\[
\le
\frac{N_{j,n}}{j^{2\beta}} + \left|\frac{N_{j,n}}{j^\beta} - 1\right|.
\]

Using \(N_{j,n}\le \delta j^\beta\) and
\[
\left|\frac{N_{j,n}}{j^\beta}-1\right|
\le
\left|\frac{N_j}{j^\beta}-1\right|
+
\mathbf{1}_{\{N_j>n-j\}}\left|\frac{n-j}{j^\beta}-1\right|
\]
we obtain the desired inequality
\[
d\bigl(D_{j,n}, \text{Poiss}(1)\bigr)
\le
\delta\bigl(1-(1+\delta j^{\beta-1})^{-\beta}\bigr)+\delta j^{-\beta}+ \max(\delta-1, j^{-\beta})+ \mathbf{1}_{\{N_j>n-j\}}\left|\frac{n-j}{j^\beta}-1\right|.
\]

---

The proof of the result now stems from the Aldous extremal point tool mentioned. We just have to show.

For a tree \(\mathcal{T}\in\mathbb{T}\) with \(|\mathcal{T}|=k\), \(U\equiv \text{Unif}(0,1)\),


\[\lim_{n\to\infty} \mathbb{P}\bigl(F(\lfloor nU\rfloor, \mathcal{T}_ n)=\mathcal{T} \bigr)=\lim_{n\to\infty}\int^{1}_ {0} \mathbb{P}\bigl(F(\lfloor nu\rfloor, \mathcal{T}_ n)=\mathcal{T} \bigr) du \rightarrow \mathbb{P}(w_{Poiss,1}=\mathcal{T} )\]

For this, fix \(u\in[0,1]\). Tomamos la BFS of the fringe of \(T_n^u\), where we stop if the \(\lfloor nu\rfloor\) fringe differs from \(T\) or if it is equal to \(T\). Recall at most we encounter \(k\).

They argue the \(k\) explorated vertices are all such \(N_j\le nu\).

Using previous lemma with \(\delta=2\) there exists \(N\in\mathbb{N}\) such that the index of any vertex attatching to \(j\) for \(j \geq N\) is bounded by \(j+2j^\beta\). Thus for \(n\ge N/u\) the index of the vertex that attaches to \(\lfloor nu\rfloor\) is bounded by \(nu+2(nu)^\beta\). We could iterate this idea so the index of the \(k\) vertex attatching the fringe is bounded by
\[
nu+2(nu)^\beta+2(nu+2(nu)^\beta)^\beta + \cdots= nu+O(n^\beta).
\]
Thus the lemma tells us that those \(k\) vertices are good at time \(n\), i.e. \(N_j\le nu\).

Now just take \(\delta>1\Rightarrow \exists \widetilde{N}>N_u\) such that \(1\le j \le k\)
\[
d\bigl(D_{j,n}, \text{Poiss}(1)\bigr)
\le
\delta\bigl(1-(1+\delta j^{\beta-1})^{-\beta}\bigr)+ \delta j^{-\beta}+\max(\delta-1, j^{-\beta})
\qquad\forall n\ge \widetilde{N}.
\]
We conclude by

\[\limsup_{n\to\infty} \left| \mathbb{P}\left(F(\lfloor nu \rfloor,\mathcal{T}_ n)=\mathcal{T} \right)-\mathbb{P}\left(w_{Poiss,1}=\mathcal{T} \right)\right| \leq k(\delta-1) \quad \forall \delta >1. 
\]

# Conclusion

I had a lot of fun reading the paper, it is true that they go on to analyze the geometry and height of each regime, but I was mainly interested in the concept of local weak convergence.

I had the idea of considering the regime \(j(n)= n- \lfloor ln(n) \rfloor \) but one may note that for any \(\beta \in (0,1)\), \(n-ln(n)\geq n-\lfloor n^{\beta} \rfloor\). Thus the overall result should be the same, representationwise looks pretty similar to taking a small \(\beta\)


<div style="display:flex; justify-content:center; gap:1rem; flex-wrap:wrap;">

  {{< figure src="/images/Images/Tree_snap5.png" alt="Tree 1" caption="$j(n)=n-\lfloor ln(n)\rfloor $" >}}
  {{< figure src="/images/Images/Tree_snap6.png" alt="Tree 1" caption="$j(n)=n-\lfloor ln(n^{1/3}) \rfloor $">}}
</div>




[^aldous]: D. Aldous, Asymptotic fringe distributions for general families of random trees, The Annals of Applied Probability
(1991), 228–266
[^neeladri]: Omer Angel, Shankar Bhamidi, Serte Donderwinkel, Neeladri Maitra, Akshay Sakanaveeti, Evolution of recursive trees with limited memory, arXiv:2510.18856 

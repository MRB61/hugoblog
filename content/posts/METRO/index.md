---
title: "On Metropolis Chains"
draft: false
date: 2025-12-28
summary: "Quick post on Metro Chains and optim"
layout: "simple"
---

{{< katex >}}
This post is more a quic knote than a deep dive.

## Motivation
As with every post, I will lay down the timeline on how I ended up writing about this. I was reading the book on Markov Chains by Levin and Peres [^Peres] and found the following section really interesting. Mainly because it is completely straightforward but has made me wonder about possible relevant applications I would mention later.


Anyone who has ever worked with Markov chains knows that, given an irreducible transition matrix \(P\), there is a unique stationary distribution \(\pi\) satisfying
\[
\pi P = \pi .
\]
This result is incredible in itself, and the proof is far from immediate. However, one thing I had never considered was the inverse problem, i.e., given a probability distribution \(\pi\) on a state space \(\Omega\), can we find a transition matrix \(P\) for which \(\pi\) is its stationary distribution?

Once you are familiar with the basics it is both a natural question and a rather straightforward answer.

Suppose \(A\) is a symmetric transition matrix (this is not the general case but will suffice for now). Now we modify \(A\) in order to obtain distribution \(\pi\) on \(\Omega\).

The idea is as follows. When at \(x\) we choose from the distribution \(A(x,\cdot)\), meaning possible states to go from \(x\) and their probabilities. If we choose the state \(y\), we move to the state with probability \(g(x,y)\), and we stay at \(x\) with probability \(1-g(x,y)\), where \(g(x,y)\) is a function we will select later. Thus we can see \(g(x,y)\) as the probability of accepting the move from \(x\) to \(y\).

The new chain is as follows:
\[
P(x,y)=
\begin{cases}
A(x,y)\,g(x,y), & \text{if } x\neq y,\\[6pt]
1-\displaystyle\sum_{z\neq x} A(x,z)\,g(x,z), & \text{if } x=y.
\end{cases}
\]

## Enforcing stationarity (detailed balance)

Now we want to force \(P\) to have distribution \(\pi\). One immediate natural way is forcing the detailed balance condition, which is sufficient:
\[
\pi(x)\,A(x,y)\,g(x,y)=\pi(y)\,A(y,x)\,g(y,x).
\]

Recall \(A\) symmetric, hence it suffices:
\[
\pi(x)\,g(x,y)=\pi(y)\,g(y,x),
\qquad x\neq y.
\]

Now recall \(g(x,y)\le 1\), thus we may choose the largest possible probability. The natural choice would be
\[
g(x,y)=\frac{\pi(y)}{\pi(x)},
\]
but one of the symmetric would be \(>1\). Thus, we may take
\[
g(x,y)=\min\left\{\frac{\pi(y)}{\pi(x)},\,1\right\}.
\]

Obtaining the so-called Metropolis chain:
\[
P(x,y)=
\begin{cases}
A(x,y)\,\min\left\{\dfrac{\pi(y)}{\pi(x)},\,1\right\}, & \text{if } x\neq y,\\[10pt]
1-\displaystyle\sum_{z\neq x}A(x,z)\,\min\left\{\dfrac{\pi(z)}{\pi(x)},\,1\right\}, & \text{if } x=y.
\end{cases}
\]

Note that if \(A\) is not symmetric it suffices to take for pairs \(A(x,y)>0\)
\[g(x,y)=\min\left\{1, \frac{\pi(y)A(y,x)}{\pi(x)A(x,y)} \right\}. \] 

## Example (optimization viewpoint)

I was completely surprised when on Peres [^Peres] they used the previous idea for an optimization problem, as old as maximizing a 1D function. They propose the following example as a better version of a hill-climb algorithm.

The setting is easy, take a regular graph \(G\). Thus a random walk on it has a symmetric transition matrix. This is straightforward because regular means every vertex has the same degree.

Fix \(\lambda \ge 1\) and define
\[
\pi_\lambda(x)=\frac{\lambda^{f(x)}}{Z(\lambda)},
\]
where
\[
Z(\lambda):=\sum_{x\in\Omega}\lambda^{f(x)}
\]
is the normalizing constant.

This constant may be costly to compute depending on \(\Omega\) size. However, our arguments do not need it!. We are concerned only by the ratio
\[
\frac{\pi_\lambda(y)}{\pi_\lambda(x)}=\lambda^{\,f(y)-f(x)}.
\]
The key is that when we make \(\lambda\to\infty\) the chain resembles a deterministic climb algorithm.

## Limit: uniform distribution over global maxima

Say
\[
\Omega^ *=\left\{x\in\Omega:\ f(x)=f^ *:=\max_{\Omega} f\right\},
\]
i.e. the set of global maxima.

Then
\[
\lim_{\lambda\to\infty}\pi_\lambda(x)
=\lim_{\lambda\to\infty}\frac{\lambda^{f(x)}}{\sum_{u\in\Omega}\lambda^{f(u)}}
=\lim_{\lambda\to\infty}\frac{\lambda^{f(x)-f^ *}}{\sum_{u\in\Omega}\lambda^{f(u)-f^ *}}.
\]

Splitting the denominator into maximizers and non-maximizers gives
\[
\lim_{\lambda\to\infty}\pi_\lambda(x)
=\lim_{\lambda\to\infty}\frac{\lambda^{f(x)-f^ *}}{|\Omega^ *|+\sum_{u\in\Omega\setminus\Omega^ *}\lambda^{f(u)-f^ *}}
=\frac{\mathbf{1}_{\{x\in\Omega^ *\}}}{|\Omega^ *|}.
\]

i.e., the uniform distribution over global maxima.

## Comparison

At first, I thought that we could consider a graph \(G\) to be a uniform one dimensional grid on \(\mathbb{R}\). Using this idea, we would fix a massive lambda and minimize nonconvex functions with ease. Well, it is not as good as it sounds, at first we cannot achieve the limit case so there would always be error. Moreover, **fixing** \(\lambda\) too large reduces the probability of leaving local maxima. This is because when fixing \(\lambda\) we are sampling from the distribution \(\pi_\lambda\), the thing is that some chains can mix quite slowly we need to approach the limit in some way. This problem is already addressed in [^Peres], they mention the existence of better algorithms that tackle precisely this. Tuning \(\lambda\) as the walk progresses, these are called simulated annealing algorithms.

Here I did some simulations to assure myself that the idea is not that good. We compare the performance of this random hill climb, an algorithm based on selecting points at random and keeping the maximum, and a standard hill climb over different types of functions. I should note I took the same number of steps with all three algorithms. The orange line represents the mean value obtained by the algorithms over 10000 simulations.

<div style="display:flex; justify-content:center; gap:1rem; flex-wrap:wrap;">

  {{< figure src="/images/METRO/Brownian_comp.png" alt="" caption="Comparison on Brownian motion">}}
  {{< figure src="/images/METRO/Sin_comp.png" alt="" caption="Comparison on $\sin (15\pi x) +x^2-8x^3 $">}}
  {{< figure src="/images/METRO/Pulse_comp.png" alt="" caption="Comparison on $e^{-(30x-15)^2}$ ">}}
</div>

Gaussian aside, which is the best scenario for a standard hill climb, the random hill climb consistently outperforms the standard on functions with several local maxima, meaning we do get out of some local maxima. However, taking \(100\) samples uniformly on a \([0,1]\) grid makes the random max a pretty safe bet.

To finish this quick note, I want to really highlight that the importance of the theorem is that we could theoretically sample from the distribution of global maxima. There are some details to work on because, in the end, we are considering the discrete case where we are taking a grid as a graph and considering a function over said graph. However, for basic functions where mixing occurs quickly we can get pretty decent results in terms of sampling. Look at the following simulation,


<div style="display:flex; justify-content:center; gap:1rem; flex-wrap:wrap;">

  {{< figure src="/images/METRO/Distrrr.png" alt="" caption="Empirical distribution of MCMC over 10000 samples">}}
</div>

As for the theory, the really interesting part is measuring when chains mix quickly and when they do not, this is done measuring when and how \(\pi_{\lambda}\) comes "close" to \(\pi \) in the TV distance. I have a lot to read on that end. But for now my interest lie on the possible use of this explicit example on determining the unicity of maxima.


[^Peres]: Markov chains and mixing times D. Levin, Y. Peres, and E. Wilmer. American Mathematical Society, (2006)
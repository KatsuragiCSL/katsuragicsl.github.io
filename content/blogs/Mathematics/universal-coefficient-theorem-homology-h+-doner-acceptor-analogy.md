---
title: "The H+ doner and acceptor analogy in universal coefficient theorem for homology"
math: true
date: 2025-10-23T00:14:00+08:00
TocOpen: true
categories: ["mathematics"]
tags: ['alegbraic-topology', 'homology', 'intuition']
cover:
  image: "https://images.unsplash.com/photo-1728406970522-1d42256abec8?ixlib=rb-4.1.0&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&q=80&w=1170"
---

## Using fields to detect integral homology?

So in the universal coefficient theorem, by taking $R = \mathbb{Z}$, we know that there is a short exact sequence:

$0 \rightarrow H_n(C_{\*}) \otimes_R M \rightarrow H_n(C_{\*} \otimes_R M) \rightarrow Tor^R_1(H_{n-1}(C_*), M) \rightarrow 0$

Some interesting cases are when $M = \mathbb{Z}_{p} \text{ or } \mathbb{Q}$ , do the homology over $\mathbb{Q}$ and $\mathbb{Z}_p$ tells us something about the integral homology? In particular, if $\tilde{H}(X; \mathbb{Q}) = 0$ and $\tilde{H}(X; \mathbb{Z}_p) = 0$ for all $p$, does it imply that $\tilde{H}(X) = 0$ ? .This is a problem suggested in [Kup2020][^1].

From the short exact sequence, it is obvious that $H_n(C_{\*}) \otimes_R M$ and $Tor^R_1(H_{n-1}(C_*), M)$ must equal to 0. But what does it tell us? It boils down to understanding what does taking tensor product and taking Tor with $\mathbb{Z}_p$ mean.

## Z_p in tensor product is like a p torsion acceptor, Tor_1(- , Z_p) is like a p torsion doner

When I was tryig to understand what does it mean for a fixed $p$, I was struck by an analogy popped up in my mind: it acts like the defintion of (strong) acid/base in high school chemistry :upside_down_face: acids are $H^+$ doner and bases are acceptors. So if you add a base to an acid the $H^+$ will get eliminated (if you get your calculations right) and vanish. This is just like the p-torsion elements in the $H_n(C_{\*}) \otimes \mathbb{Z_p}$ and $Tor_1(H_{n-1}(C_*), \mathbb{Z_p})$:

$\mathbb{Z_p}$ in $Tor_1(A, \mathbb{Z_p})$ is like a p-torsion elements doner. Since $Tor_1(A, \mathbb{Z_p})$ is the kernel of the map $\mathbb{Z_p} \otimes A \xrightarrow{p \times id} \mathbb{Z_p} \otimes A$, $pn \otimes a = 0$ if $a \in A$ is a p-torsion element because it "absorbs" the factor $p$ and vanishes. Hence $Tor_1(A, \mathbb{Z_p}) = 0$ only if every elements in $A$ has no p-torsion elements.

$\mathbb{Z_p}$ in $A \otimes \mathbb{Z_p}$ is like a p-torsion elements receiver: easy to see this tensor product is $0$ only if every elements in $A$ can "donate" a factor $p$ for elements in $\mathbb{Z_p}$ to absorb.

Can we have $H_{\*}(X) \neq 0$ but vanishes both when taking tensor product with $\mathbb{Z_p}$ and taking $Tor_1(- , \mathbb{Z_p})$ ? Sure, we just need an abelian group that always donate p factors but never acceptor it (like $O^-$ blood type. Ha, another chemistry/biology analogy). For example $\mathbb{Z}[\frac{1}{p}]$ does the job.



Now similar thought process will tell you what happens when $M = \mathbb{Q}$. $\mathbb{Q}$ is torsion free, which means it never accepts torsion but only donates, so if $A$ has a non-torsion element $a$, then $a \otimes q$ for some $q$ is non-zero. So in order for $A \otimes \mathbb{Q}$ to be zero, $A$ must have all of its elements being torsion, which contradicts what we have seen above, unless $A = 0$.

Hence we have proved that $\tilde{H}(X) = 0$.



[^1]: Kupers, A. (2020). Lectures on algebraic topology. Lecture. Retrieved 2025, from https://www.utsc.utoronto.ca/people/kupers/teaching/algebraic-topology-lecture-notes/. 
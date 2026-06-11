---
title: "Understanding Yoneda lemma"
date: 2026-06-03T01:33:43+08:00
TocOpen: true
categories: ["mathematics"]
tags: ['category-theory', 'intuition']
math: true
tikz: true
cover:
  image: "https://images.unsplash.com/photo-1560763150-5f34e9c1e68d?q=80&w=1935&auto=format&fit=crop&ixlib=rb-4.1.0&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D"
---


### The Yoneda Lemma

The Yoneda lemma has been being complainted as "hard to understand" for a long time. Indeed it is not very easy, so I was trying to come up with a way to understand it more intuitively.

Everyone knows the analogy by Ravi Vakil:

> You work at a particle accelerator. You want to understand some particle. All you can do are throw other particles at it and see what happens. If you understand how your mystery particle responds to all possible test particles at all possible test energies, then you know everything there is to know about your mystery particle.

But how to see that in actions?

### Throw a particle at it...or we can throw more at once?

Start with the simplest probe with a one-point set $A = \{\ast\}$. A probe $\{\ast\} \to X$ just selects an element of $X$, so $X$ is bijective to the set of all maps from $A$ to $X$.

But...what stops us from throwing 2 at the same time?

Our first instinct might be probing with $A = \{a, b\}$. But if there is no restrictions on where can $a$ and $b$ map to, it would be a lot of redundancy in the set of all maps from $A$ to $X$: because in this case, for a finite $X$, the set of all maps has size $2^X$. The extra element in the probing set is doing duplicated work.

So, the easiest solution of this is to force $a$ and $b$ map to different elements --- which means we want some kind of relation between the things that we use to probe, and the probes need to respect the relation.

That's exactly what bring us to the idea of using category theory, isn't it?

If we can probe with 2 elements, we can also probe with any sets; if we can probe with any set, we can also probe with many many sets at once. We can go even further: why stop at probing a set at a time? We can probe all of them at the same time!

That should give us the idea to have the following setup: We probe the category $\mathbf{Set}$ with another category $\mathbf{C}$, with a functor $F$ as a probe. Now, pick a set $F(c)$ that is probed by an object $c$, we should be able to recover $F(c)$ by two things: the probe, and the relations/structure (i.e. either $Hom(c, -)$ or $Hom(-, c)$).

With these two data, we can ask: how many different ways you can project the structure concerning $c$ into F?

### The homomorphisms between cyclic groups.

Just like functors respect the structure of categories, natural transformations respect the structure of functors. $Nat(Hom(c,-), F)$ is exactly what we want.

Think about a group homomorphism (which respect the structure of groups) $\phi: \mathbb{Z} \to G$, once you commit to $\phi(1) = g$ everything else follows.

Now $Hom(c, -)$. It is the relation-free, freely-generated case just like $\mathbb{Z}$. The "generator" of $Hom(c, -)$ is the most natural one: $\mathbf{C}(c, c)$. So deciding $u = \alpha_c(\text{id}_c) \in F(c)$ locks in $\alpha_X(f) = F(f)(u)$ for all $f$, and any $u$ is a legal choice. One decision, no strings attached, the entire transformation.

{{< tikz >}}

\usepackage{tikz}
\usepackage{amsfonts}

\begin{document}
\begin{tikzpicture}[scale=1.5, font=\sffamily, >=stealth]

  % --- LEFT PANEL: Cyclic Group Homomorphism ---
  \node at (1, 3.5) {\textbf{Cyclic Group Homomorphism}};
  
  \node (Z1) at (0, 2) {$1 \in \mathbb{Z}$ (Generator)};
  \node (Zn) at (0, 0) {$n \in \mathbb{Z}$};
  \node (Gg) at (2.5, 2) {$g \in G$};
  \node (Ggn) at (2.5, 0) {$g^n \in G$};

  % Vertical internal arrows
  \draw[|->, dashed, blue, thick] (Z1) -- (Zn) node[midway, left, align=center, scale=0.8] {multiply\\by $n$};
  \draw[|->, dashed, red, thick] (Gg) -- (Ggn) node[midway, right, align=center, scale=0.8] {apply group\\operation $n$ times};

  % Horizontal projection arrows
  \draw[|->, thick, purple] (Z1) -- (Gg) node[midway, above] {$\phi$};
  \draw[|->, thick, purple] (Zn) -- (Ggn) node[midway, below] {$\phi$};

  % Divider - Shifted right
  \draw[thick, gray, dotted] (5.5, -0.5) -- (5.5, 4);

  % --- RIGHT PANEL: Yoneda Lemma --- 
  % Everything shifted right by 2.5 units
  \node at (10, 3.5) {\textbf{Yoneda Lemma}};

  \node (Id_c) at (7.5, 2) {$\mathrm{id}_c \in \mathcal{C}(c, c)$ (Generator)};
  \node (f) at (7.5, 0) {$f \in \mathcal{C}(c, X)$};
  \node (u) at (12.5, 2) {$u \in F(c)$};
  \node (Ffu) at (12.5, 0) {$F(f)(u) \in F(X)$};

  % Vertical internal arrows
  \draw[|->, dashed, blue, thick] (Id_c) -- (f) node[midway, left, align=center, scale=0.8] {post-compose\\with $f$};
  \draw[|->, dashed, red, thick] (u) -- (Ffu) node[midway, right, align=center, scale=0.8] {apply functor\\logic $F(f)$};

  % Horizontal projection arrows
  \draw[|->, thick, purple] (Id_c) -- (u) node[midway, above] {$\alpha_c$};
  \draw[|->, thick, purple] (f) -- (Ffu) node[midway, below] {$\alpha_X$};

\end{tikzpicture}
\end{document}

{{< /tikz >}}

And that's exactly how you think about proving Yoneda lemma too.
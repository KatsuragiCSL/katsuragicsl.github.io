---
title: "Understanding Yoneda lemma"
date: 2026-06-02T17:59:01+08:00
TocOpen: true
categories: ["mathematics"]
tags: ['category-theory']
math: true
---


### The Yoneda Lemma, and why it acts like a cyclic group

Sooner or later, anyone learning category theory runs into the Yoneda Lemma. People like to call it the "hardest trivial theorem" in mathematics --- the proof is a few lines of pushing definitions through a diagram, but it can take weeks before the point of it lands.

The covariant version says, roughly: you understand an object by the maps coming out of it, and a map out of that whole family of morphisms is pinned down by a single choice. Below I build it up from a probing metaphor --- probe one element, then probe many at once and watch the structure constrain you --- and then show that the constraint is the same one that makes a cyclic group fall out of its generator.

### Objects you can't open

In set theory you understand a set by looking at its elements. Categories don't give you that. An object is opaque --- there's no inside to inspect.

What you get instead is the morphisms. For an object $A$, collect every map out of $A$: this is the functor $h^A = \mathcal{C}(A, -)$, which sends an object $X$ to the set $\mathcal{C}(A, X)$ of morphisms from $A$ to $X$. (Conventions vary on the notation --- some books write $h^A$ for the contravariant functor instead --- so it's worth fixing yours up front. Everything here is covariant: probes point *out* of $A$.)

Call a morphism $g: A \to X$ a **probe**. Then $h^A$ is the whole system of probes you can fire out of $A$, sorted by where they land. The smallest, most boring probe is the identity $\text{id}_A: A \to A$ --- the probe that goes nowhere. Hold onto it; it does all the work later.

### Probing more than one target at a time

Start in $\mathbf{Set}$ with the simplest possible source, a one-point set $A = \{\ast\}$. A probe $\{\ast\} \to X$ just selects an element of $X$, so

$$\mathcal{C}(\{*\}, X) \cong X.$$

Probing elements one at a time is fine, but it throws something away: the elements of different sets are tied together by the functions between those sets, and one-at-a-time probing ignores all of that. So let's probe several targets at once and **insist that the probes respect the maps between targets**.

To compare against, fix some observable --- a functor $F: \mathbf{Set} \to \mathbf{Set}$ --- and record, for each probe, a piece of $F$-data. That assignment is a family of functions $\alpha_X: \mathcal{C}(\{*\}, X) \to F(X)$, one per target. "Respecting structure" means: for any map $h: X \to Y$ between targets,

$$\alpha_Y(h \circ g) = F(h)\big(\alpha_X(g)\big).$$

A family that obeys this is exactly a **natural transformation** $\alpha: h^{\{*\}} \to F$. Nothing more exotic than "the probes you fire and the data you record must agree along every map between targets."

Here's that agreement in miniature. Take two targets $\{a\}$ and $\{a, b\}$ and the inclusion $\iota: \{a\} \hookrightarrow \{a, b\}$ sending $a \mapsto a$. The element $a$ lives in both. Naturality forces

$$\alpha_{\{a,b\}}(a) = F(\iota)\big(\alpha_{\{a\}}(a)\big),$$

so once you've recorded data for the probe hitting $a$ in $\{a\}$, the data for $a$ inside $\{a, b\}$ is no longer yours to choose --- the inclusion fixes it. Only the genuinely new element $b$ looks free at this stage. The structure between the targets lets you trace exactly which recorded datum determines which.

So why stop at two targets? Push the same logic everywhere. Every element $x \in X$ is itself a probe $\hat{x}: \{\ast\} \to X$, and it factors through the trivial probe as $\hat{x} = \hat{x} \circ \text{id}_{\{\ast\}}$. Run naturality along $\hat{x}$:

$$\alpha_X(\hat{x}) = F(\hat{x})\big(\alpha_{\{\ast\}}(\text{id}_{\{\ast\}})\big).$$

Every value of $\alpha$, on every target, is computed from the single datum $u = \alpha_{\{\ast\}}(\text{id}_{\{\ast\}}) \in F(\{\ast\})$. The whole infinite family is the image of the trivial probe, carried around by $F$. That "free" element $b$ from a moment ago wasn't free after all --- it's another probe $\{\ast\} \to \{a,b\}$, so its datum is $F$ applied to the same $u$.

Reading it the other way: every datum $u \in F(\{\ast\})$ does give a consistent family, and different $u$'s give different families. So the natural transformations are *exactly* the elements of $F(\{\ast\})$:

$$\text{Nat}\big(h^{\{\ast\}}, F\big) \cong F(\{\ast\}).$$

Nothing used that the source was a point. Replace $\{\ast\}$ with any object $A$, replace "element of $X$" with "probe $A \to X$", and replace the trivial probe with $\text{id}_A$, and the same argument runs unchanged.

### The statement

For a locally small category $\mathcal{C}$, an object $A$, and a functor $F: \mathcal{C} \to \mathbf{Set}$, there is an isomorphism

$$\text{Nat}(h^A, F) \cong F(A),$$

natural in both $A$ and $F$, given by sending a natural transformation $\alpha$ to the element $\alpha_A(\text{id}_A) \in F(A)$.

Take a second on the left-hand side. A natural transformation looks enormous: a function $\alpha_X: \mathcal{C}(A, X) \to F(X)$ for every object $X$ at once. The probing argument above is the whole content of why that collapses to one element of $F(A)$. The next section is the same fact wearing different clothes.

### The homomorphisms between cyclic groups as an analogy.

Think about a group homomorphism $\phi: \mathbb{Z} \to G$. The integers are infinite, so naively you'd have to say where every $n$ goes. But $\mathbb{Z}$ is generated by $1$, and $\phi$ has to respect the group operation, so once you commit to $\phi(1) = g$ everything else follows: $\phi(2) = g^2$, $\phi(-1) = g^{-1}$, and so on. The image of the generator is the only real decision --- the exact role the trivial probe $\text{id}_A$ played above.

Two things are worth separating. First, the map is *determined* by where $1$ goes. Second, and this is the part that matters --- you can send $1$ to *any* $g$ you like and still get a valid homomorphism. That second property is special to $\mathbb{Z}$. It comes from $\mathbb{Z}$ being *free* on one generator, with no relations to satisfy, and it gives a clean bijection:

$$\text{Hom}(\mathbb{Z}, G) \cong G.$$

To see why "free" is doing the work, break it. A homomorphism $\mathbb{Z}/n \to \mathbb{Z}/m$ is still fixed by the image of the generator, but now that image isn't free: the relation $n \cdot 1 = 0$ forces it to land on an element whose order divides $n$. Count them and you get

$$\big|\text{Hom}(\mathbb{Z}/n, \mathbb{Z}/m)\big| = \gcd(n, m),$$

which is usually *smaller* than $m = |\mathbb{Z}/m|$. Relations cut down where the generator may go, so the maps no longer match the elements one-for-one.

This is exactly why the representable $h^A$ is the right analogue of $\mathbb{Z}$ and not of $\mathbb{Z}/n$. The probing argument showed that *every* $u \in F(A)$ extends to a valid natural transformation, with no order-of-the-generator condition cutting anything down. $h^A$ is the relation-free, freely-generated case --- which is what makes Yoneda an honest bijection $\text{Nat}(h^A, F) \cong F(A)$ rather than a strict subset like the $\gcd$ count above.

### The same move, in Yoneda

$h^A$ behaves like $\mathbb{Z}$, and $\text{id}_A \in \mathcal{C}(A, A)$ is its generator. Every probe $f \in \mathcal{C}(A, X)$ is the generator pushed forward, $f = f \circ \text{id}_A$, so deciding $u = \alpha_A(\text{id}_A) \in F(A)$ locks in $\alpha_X(f) = F(f)(u)$ for all $f$, and any $u$ is a legal choice. One decision, no strings attached, the entire transformation.

### Visualizing

Here's the bookkeeping. Take any probe $f \in \mathcal{C}(A, X)$ and ask where $\alpha$ sends it. Two routes:

- Push $\text{id}_A$ along $f$ first (giving $f$), then apply $\alpha_X$.
- Apply $\alpha_A$ first (giving $u$), then carry it across with $F(f)$.

Naturality says the square commutes, so the routes agree:

$$\alpha_X(f) = F(f)(u), \qquad u = \alpha_A(\text{id}_A).$$

The picture puts the cyclic-group version on the left and the Yoneda version on the right, so you can see it's the same diagram twice.

{{< tikz >}}

\usepackage{tikz}

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

  \node (IdA) at (7.5, 2) {$\mathrm{id}_A \in \mathcal{C}(A, A)$ (Generator)};
  \node (f) at (7.5, 0) {$f \in \mathcal{C}(A, X)$};
  \node (u) at (12.5, 2) {$u \in F(A)$};
  \node (Ffu) at (12.5, 0) {$F(f)(u) \in F(X)$};

  % Vertical internal arrows
  \draw[|->, dashed, blue, thick] (IdA) -- (f) node[midway, left, align=center, scale=0.8] {post-compose\\with $f$};
  \draw[|->, dashed, red, thick] (u) -- (Ffu) node[midway, right, align=center, scale=0.8] {apply functor\\logic $F(f)$};

  % Horizontal projection arrows
  \draw[|->, thick, purple] (IdA) -- (u) node[midway, above] {$\alpha_A$};
  \draw[|->, thick, purple] (f) -- (Ffu) node[midway, below] {$\alpha_X$};

\end{tikzpicture}
\end{document}

{{< /tikz >}}


### So what

The lemma isn't symbol-pushing that happens to come out clean. It's the same fact you already trust about free objects: a map out of something freely generated is the image of its generator and nothing more. Probing taught us the generator is the trivial probe $\text{id}_A$; the cyclic-group picture taught us why a free generator gives an exact count instead of a $\gcd$. Put them together and Yoneda reads in one line: find where $\text{id}_A$ lands, and you've found the whole thing.
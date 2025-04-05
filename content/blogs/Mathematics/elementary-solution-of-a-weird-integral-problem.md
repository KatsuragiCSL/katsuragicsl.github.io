---
title: "An elementary solution of a weird intergal problem (Putnam 1985 A5)"
subtitle: "by observing symmetry"
math: true
tikz: true
date: 2025-04-05T22:38:14+08:00
TocOpen: true
categories: ["mathematics"]
tags: ['putnam', 'elementary', 'fourier-analysis', 'symmetry']
---

### Problem

Let $I_{m} = \int^{2\pi}_{0} \cos(x)\cos(2x)\dots\cos(mx) dx$. For $m$ in $1, 2, \dots, 10$,
for which $m$ is $I_m \neq 0$ ?


### Solution

$I_m$ is non-zero if and only if $m \equiv 0, 3 \pmod{4}$.


### Main idea

The official(seemingly? It is in the putnam problem book and a few solutions I found online do the same.) solution is to substitute $\cos x = \frac{e^{ix} + e^{-ix}}{2}$ followed by grouping the terms into $\cos x \cos (2x) \dots \cos (mx) = e^{\text{something}}$, and analyze the `something`. This approach of cause is of cause good in its own right: it is exactly how you split up the $e^{in\theta}$ terms into triginometric polynomials (or ) in Fourier analysis 101. However it is a little bit annoying to manipulate those powers of $e$. And for this problem it could be done much in a much simpler and elementary way: exploiting the point of symmetry.

Let $f_m(x) = \cos(x)\cos(2x)\dots\cos(mx)$ and $g_m(x) = \cos(mx)$. Notice that $g_m(x-\pi) = -g_m(x)$ if $m$ is odd and $ = g_m(x)$ if $m$ is even. \
Hence $f_1(x-\pi) = -f_2(x)$ , $f_2(x-\pi) = -f_2(x)$ , $f_3(x-\pi) = f_3(x), \dots$ 

So $\int^{2\pi}\_{0} f_m = \int^{2\pi}\_{\pi} f_m + \int^{\pi}_{0} f_m = \int^{\pi}\_{0} (af_m + f_m)$ by change of variable, where $a$ is $-1$ when $m$ has a value such that $f_m(x-\pi) = -f_m(x)$ and is $1$ otherwise. 

If we note $0$ when the integral gives $0$ and $1$ if not, then it looks like:

$$
m = 1, 2, 3, 4, 5, 6, 7, 8, \dots
$$

$$
\int f_m = 0, 0, 1, 1, 0, 0, 1, 1, \dots
$$

In general, the integral of $f$ is non-zero if and only if $m \equiv 0, 3 \pmod{4}$.

The $x-\pi$ thing is obvious from staring at the following graphs:


{{< tikz >}}
\usepackage{pgfplots}
\usepackage{amsmath}
\pgfplotsset{compat=1.16}
\pgfkeys{/pgfplots/Axis Style/.style={
    width=13.5cm, height=5cm,
    axis x line=center, 
    axis y line=middle, 
    samples=100,
    ymin=-1.5, ymax=1.5,
    xmin=0, xmax=7.0,
    domain=0:2*pi
}}

\begin{document}
\begin{tikzpicture}[scale=1.5]
\begin{axis}[
    Axis Style,
    xtick={
        pi/2, pi, 3*pi/2, 2*pi
    },
    xticklabels={
        $\frac{\pi}{2}$, $\pi$, $\frac{3\pi}{2}$, $2\pi$
    }
]

\addplot [mark=none, ultra thick, blue] {cos(deg(x))} node[above] {cos x};

\draw[dashed] ({pi},-1.5) -- ({pi},1.5);

\end{axis}
\end{tikzpicture}

\end{document}
{{< /tikz >}}

{{< tikz >}}
\usepackage{pgfplots}
\usepackage{amsmath}
\pgfplotsset{compat=1.16}
\pgfkeys{/pgfplots/Axis Style/.style={
    width=13.5cm, height=5cm,
    axis x line=center, 
    axis y line=middle, 
    samples=100,
    ymin=-1.5, ymax=1.5,
    xmin=0, xmax=7.0,
    domain=0:2*pi
}}

\begin{document}
\begin{tikzpicture}[scale=1.5]
\begin{axis}[
    Axis Style,
    xtick={
        pi/2, pi, 3*pi/2, 2*pi
    },
    xticklabels={
        $\frac{\pi}{2}$, $\pi$, $\frac{3\pi}{2}$, $2\pi$
    }
]

\addplot [mark=none, ultra thick, blue] {cos(deg(2*x))} node[above] {cos 2x};

\draw[dashed] ({pi},-1.5) -- ({pi},1.5);

\end{axis}
\end{tikzpicture}

\end{document}
{{< /tikz >}}

{{< tikz >}}
\usepackage{pgfplots}
\usepackage{amsmath}
\pgfplotsset{compat=1.16}
\pgfkeys{/pgfplots/Axis Style/.style={
    width=13.5cm, height=5cm,
    axis x line=center, 
    axis y line=middle, 
    samples=100,
    ymin=-1.5, ymax=1.5,
    xmin=0, xmax=7.0,
    domain=0:2*pi
}}

\begin{document}
\begin{tikzpicture}[scale=1.5]
\begin{axis}[
    Axis Style,
    xtick={
        pi/2, pi, 3*pi/2, 2*pi
    },
    xticklabels={
        $\frac{\pi}{2}$, $\pi$, $\frac{3\pi}{2}$, $2\pi$
    }
]

\addplot [mark=none, ultra thick, blue] {cos(deg(3*x))} node[above] {cos 3x};

\draw[dashed] ({pi},-1.5) -- ({pi},1.5);

\end{axis}
\end{tikzpicture}

\end{document}
{{< /tikz >}}

### Thought process

Here I try to recall my thought process when I solve this problem, which is in general a good thing to do after solving a problem (reflect on the process instead of moving right on to the next thing). It will be less organized and more in a dialectical way:

1. What is this problem about? Some weird integrals and some of them are supposed to be zero. I need to find out which are zero and which are not.
2. The integrals are too awkward, don't try to use trigo multiplying formulas.
3. What is important? The integrals are awkward, but I don't need to evaluate their values, only need to know whether they can be zero. How? Okay, I know integrating cosine from 0 to 2pi gives you zero. But that does not scale to the products of cos(mx).
4. Let's see why exactly integrating cosine from 0 to 2pi gives you zero. Do not use the antiderivative argument since that does not scale too.
5. Okay cos is an even function, it is symmetric along 0. And it is periodic, so you can shfit the domain to be like integrating from -pi to pi, and boom, easy to see that it is zero.
7. But what is the role of symmetry here? Merely symmetry does not anything about the value of the integral, especially doesn't suggest that it should be zero.
8. Okay, it is also symmetric along pi. But the good thing about it is that the "areas" cancel each other and that's why the integral of cos x is zero. Accurately cos(x-pi) = -cos(x).
9. So what? that means $\int^{2\pi}_0 \cos(x) = \int^{2\pi}\_{\pi} \cos(x) + \int^{\pi}_0 \cos(x) = \int^{\pi}_0 -\cos(x) + \int^{\pi}_0 \cos(x) = 0$
10. Now this can scale to cos(mx): for a given m, all we need to know is its behavior under shifting the graph by pi (and see whether it gives you a minus sign or not).
11. Done! I only need to write down the pattern of the sign flipping now.
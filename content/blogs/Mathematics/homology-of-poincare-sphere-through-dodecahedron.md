---
title: "Calculating the homology of Poincaré's homology sphere through dodecahedron and cellular homology"
math: true
tikz: true
date: 2025-11-10T04:01:59+08:00
TocOpen: true
categories: ["mathematics"]
tags: ['alegbraic-topology', 'homology', 'CW-complex']
cover:
  image: "https://media.sciencephoto.com/image/c0530106/800wm/C0530106-Dodecahedron_universe,_conceptual_illustration.jpg"
  caption: "Credits: https://www.sciencephoto.com/media/1198122/view/dodecahedron-universe-conceptual-illustration"
---

## Homology sphere

A homology sphere is a (closed connected oriented) $n$-mainfolds with the same homology as the $n$-sphere. Poincaré first conjectured that any $n$-manifolds homologous (i.e. having the same homology) to the $n$-sphere should be homeomorphic to the $n$-sphere, then later he found a counterexample, which led him to a modified conjecture (which is the Poincaré's conjecture).

The counterexample he found is very interesting, one of the way to construct it is the folowing:
1. take a dodecahedron
2. identify the pairs of opposite faces by rotating each of them by $\dfrac{\pi}{5}$

This will identify $4$ vertices into $1$, $3$ edges into $1$, and $2$ faces into $1$. The resulting manifold will be a CW-complex with **$5$** $0$-cells, **$10$** $1$-cells and **$6$** $2$-cells. And it can be shown that it has the same homology as $\mathbb{S}^3$, but I have never seen anyone worked it out...so I decided to do it by myself with nice diagrams, since it is quite hard to keep track of everything while computing, and I thought that it will be beautiful to draw them out :smiley:


## Clumsy (but colorful) computation

Below is a figure showing the identified vertices (with numbers) and edges (with colors) of the dodecahedron aftering taking quotient:

{{< tikz >}}

\usepackage{tikz}
\tikzset{style={inner sep=0pt}}
\tikzset{every path/.style={line width=0.4 mm}}
\begin{document}

\begin{tikzpicture}[scale=3]

\definecolor{aqua}{rgb}{0.0, 1.0, 1.0}
\definecolor{brightgreen}{rgb}{0.4, 1.0, 0.0}
\definecolor{bronze}{rgb}{0.8, 0.5, 0.2}
\definecolor{cadmiumyellow}{rgb}{1.0, 0.96, 0.0}
\definecolor{cobalt}{rgb}{0.0, 0.28, 0.67}
\definecolor{hotpink}{rgb}{1.0, 0.41, 0.71}
\definecolor{lavenderindigo}{rgb}{0.58, 0.34, 0.92}
\definecolor{pumpkin}{rgb}{1.0, 0.46, 0.09}

\newdimen\R
\R=2cm


\draw (270:\R)
\foreach [count=\n] \x in {342,414,486,...,630} {
	-- (\x:\R) node (in-\n) {}
};

\R=2.1cm
\draw[dashed] (306:\R)
\foreach [count=\n] \x in {378,450,522,...,666} {
	-- (\x:\R) node (mid-\n)  {}
};

\R=3cm
\draw (54:\R)
\foreach [count=\n] \x in {90,126,162,...,414} {
	-- (\x:\R) node (out-\n) (out-\n) {}
};

\draw[dashed] (out-1) -- (mid-2);
\node[yshift=4pt] at (out-1.north) {\LARGE 4};
\node[xshift=4pt,yshift=4pt] at (mid-2.north east) {\LARGE 2};

\draw (out-2) -- (in-3);
\node[yshift=4pt] at (out-2.north) {\LARGE 1};
\node[xshift=-4pt] at (in-3.north) {\LARGE 3};

\draw[dashed] (out-3) -- (mid-3);
\node[xshift=-4pt] at (out-3.west) {\LARGE 5};
\node[yshift=-4pt] at (mid-3.west) {\LARGE 3};

\draw (out-4) -- (in-4);
\node[xshift=-4pt] at (out-4.west) {\LARGE 2};
\node[yshift=-4pt] at (in-4.west) {\LARGE 4};

\draw[dashed] (out-5) -- (mid-4);
\node[xshift=-4pt] at (out-5.west) {\LARGE 1};
\node[yshift=-4pt] at (mid-4.west) {\LARGE 4};

\draw (out-6) -- (in-5);
\node[xshift=-4pt] at (out-6.west) {\LARGE 3};
\node[yshift=-4pt] at (in-5.west) {\LARGE 5};

\draw[dashed] (out-7) -- (mid-5);
\node[xshift=-4pt] at (out-7.west) {\LARGE 2};
\node[yshift=-4pt] at (mid-5.west) {\LARGE 5};

\draw (out-8) -- (in-1);
\node[xshift=-4pt] at (out-8.west) {\LARGE 4};
\node[yshift=-4pt] at (in-1.west) {\LARGE 1};

\draw[dashed] (out-9) -- (mid-1);
\node[xshift=-4pt] at (out-9.west) {\LARGE 3};
\node[xshift=4pt,yshift=-4pt] at (mid-1.south east) {\LARGE 1};

\draw (out-10) -- (in-2);
\node[xshift=-4pt] at (out-10.west) {\LARGE 5};
\node[xshift=8pt,yshift=4pt] at (in-2.east) {\LARGE 2};

% coloring
\draw[red] (in-1) -- (in-2);
\draw[red, dashed] (mid-1) -- (mid-2);
\draw[red] (out-4) -- (out-5);

\draw[aqua] (in-2) -- (in-3);
\draw[aqua, dashed] (mid-2) -- (mid-3);
\draw[aqua] (out-6) -- (out-7);

\draw[brightgreen] (in-3) -- (in-4);
\draw[brightgreen, dashed] (mid-3) -- (mid-4);
\draw[brightgreen] (out-8) -- (out-9);

\draw[bronze] (in-4) -- (in-5);
\draw[bronze, dashed] (mid-4) -- (mid-5);
\draw[bronze] (out-10) -- (out-1);

\draw[cadmiumyellow] (in-5) -- (in-1);
\draw[cadmiumyellow, dashed] (mid-5) -- (mid-1);
\draw[cadmiumyellow] (out-2) -- (out-3);

\draw[cobalt] (in-2) -- (out-10);
\draw[cobalt, dashed] (mid-5) -- (out-7);
\draw[cobalt] (out-3) -- (out-4);

\draw[hotpink] (out-1) -- (out-2);
\draw[hotpink, dashed] (out-5) -- (mid-4);
\draw[hotpink] (out-8) -- (in-1);

\draw[lavenderindigo] (out-2) -- (in-3);
\draw[lavenderindigo] (out-5) -- (out-6);
\draw[lavenderindigo,dashed] (out-9) -- (mid-1);

\draw[pumpkin] (out-4) -- (in-4);
\draw[pumpkin] (out-7) -- (out-8);
\draw[pumpkin,dashed] (out-1) -- (mid-2);


\end{tikzpicture}
\end{document}

{{< /tikz >}}

We will calculates its singular homology by CW-homology. To do so, we need to know the how the generators (the faces, edges, vertices) are mapped by the differential. Let's do the differential on each faces first. There are 6 of them, I will mark them out below:

Face A

{{< tikz >}}

\usepackage{tikz}
\tikzset{style={inner sep=0pt}}
\tikzset{every path/.style={line width=0.4 mm}}
\begin{document}

\begin{tikzpicture}[scale=3]

\definecolor{aqua}{rgb}{0.0, 1.0, 1.0}
\definecolor{brightgreen}{rgb}{0.4, 1.0, 0.0}
\definecolor{bronze}{rgb}{0.8, 0.5, 0.2}
\definecolor{cadmiumyellow}{rgb}{1.0, 0.96, 0.0}
\definecolor{cobalt}{rgb}{0.0, 0.28, 0.67}
\definecolor{hotpink}{rgb}{1.0, 0.41, 0.71}
\definecolor{lavenderindigo}{rgb}{0.58, 0.34, 0.92}
\definecolor{pumpkin}{rgb}{1.0, 0.46, 0.09}

\newdimen\R
\R=2cm

% face A
\draw[fill=yellow] (270:\R)
\foreach [count=\n] \x in {342,414,486,...,630} {
	-- (\x:\R) node (in-\n) {}
};
\node at (0,0) {\Huge A};

\R=2.1cm
\draw[dashed,fill=yellow,opacity=0.2] (306:\R)
\foreach [count=\n] \x in {378,450,522,...,666} {
	-- (\x:\R) node (mid-\n)  {}
};

\R=3cm
\draw (54:\R)
\foreach [count=\n] \x in {90,126,162,...,414} {
	-- (\x:\R) node (out-\n) (out-\n) {}
};

\draw[dashed] (out-1) -- (mid-2);
\node[yshift=4pt] at (out-1.north) {\LARGE 4};
\node[xshift=4pt,yshift=4pt] at (mid-2.north east) {\LARGE 2};

\draw (out-2) -- (in-3);
\node[yshift=4pt] at (out-2.north) {\LARGE 1};
\node[xshift=-4pt] at (in-3.north) {\LARGE 3};

\draw[dashed] (out-3) -- (mid-3);
\node[xshift=-4pt] at (out-3.west) {\LARGE 5};
\node[yshift=-4pt] at (mid-3.west) {\LARGE 3};

\draw (out-4) -- (in-4);
\node[xshift=-4pt] at (out-4.west) {\LARGE 2};
\node[yshift=-4pt] at (in-4.west) {\LARGE 4};

\draw[dashed] (out-5) -- (mid-4);
\node[xshift=-4pt] at (out-5.west) {\LARGE 1};
\node[yshift=-4pt] at (mid-4.west) {\LARGE 4};

\draw (out-6) -- (in-5);
\node[xshift=-4pt] at (out-6.west) {\LARGE 3};
\node[yshift=-4pt] at (in-5.west) {\LARGE 5};

\draw[dashed] (out-7) -- (mid-5);
\node[xshift=-4pt] at (out-7.west) {\LARGE 2};
\node[yshift=-4pt] at (mid-5.west) {\LARGE 5};

\draw (out-8) -- (in-1);
\node[xshift=-4pt] at (out-8.west) {\LARGE 4};
\node[yshift=-4pt] at (in-1.west) {\LARGE 1};

\draw[dashed] (out-9) -- (mid-1);
\node[xshift=-4pt] at (out-9.west) {\LARGE 3};
\node[xshift=4pt,yshift=-4pt] at (mid-1.south east) {\LARGE 1};

\draw (out-10) -- (in-2);
\node[xshift=-4pt] at (out-10.west) {\LARGE 5};
\node[xshift=8pt,yshift=4pt] at (in-2.east) {\LARGE 2};

% coloring
\draw[red] (in-1) -- (in-2);
\draw[red, dashed] (mid-1) -- (mid-2);
\draw[red] (out-4) -- (out-5);

\draw[aqua] (in-2) -- (in-3);
\draw[aqua, dashed] (mid-2) -- (mid-3);
\draw[aqua] (out-6) -- (out-7);

\draw[brightgreen] (in-3) -- (in-4);
\draw[brightgreen, dashed] (mid-3) -- (mid-4);
\draw[brightgreen] (out-8) -- (out-9);

\draw[bronze] (in-4) -- (in-5);
\draw[bronze, dashed] (mid-4) -- (mid-5);
\draw[bronze] (out-10) -- (out-1);

\draw[cadmiumyellow] (in-5) -- (in-1);
\draw[cadmiumyellow, dashed] (mid-5) -- (mid-1);
\draw[cadmiumyellow] (out-2) -- (out-3);

\draw[cobalt] (in-2) -- (out-10);
\draw[cobalt, dashed] (mid-5) -- (out-7);
\draw[cobalt] (out-3) -- (out-4);

\draw[hotpink] (out-1) -- (out-2);
\draw[hotpink, dashed] (out-5) -- (mid-4);
\draw[hotpink] (out-8) -- (in-1);

\draw[lavenderindigo] (out-2) -- (in-3);
\draw[lavenderindigo] (out-5) -- (out-6);
\draw[lavenderindigo,dashed] (out-9) -- (mid-1);

\draw[pumpkin] (out-4) -- (in-4);
\draw[pumpkin] (out-7) -- (out-8);
\draw[pumpkin,dashed] (out-1) -- (mid-2);


\end{tikzpicture}
\end{document}

{{< /tikz >}}

Face B

{{< tikz >}}

\usepackage{tikz}
\tikzset{style={inner sep=0pt}}
\tikzset{every path/.style={line width=0.4 mm}}
\begin{document}

\begin{tikzpicture}[scale=3]

\definecolor{aqua}{rgb}{0.0, 1.0, 1.0}
\definecolor{brightgreen}{rgb}{0.4, 1.0, 0.0}
\definecolor{bronze}{rgb}{0.8, 0.5, 0.2}
\definecolor{cadmiumyellow}{rgb}{1.0, 0.96, 0.0}
\definecolor{cobalt}{rgb}{0.0, 0.28, 0.67}
\definecolor{hotpink}{rgb}{1.0, 0.41, 0.71}
\definecolor{lavenderindigo}{rgb}{0.58, 0.34, 0.92}
\definecolor{pumpkin}{rgb}{1.0, 0.46, 0.09}

\newdimen\R
\R=2cm

\draw (270:\R)
\foreach [count=\n] \x in {342,414,486,...,630} {
	-- (\x:\R) node (in-\n) {}
};

\R=2.1cm
\draw[dashed] (306:\R)
\foreach [count=\n] \x in {378,450,522,...,666} {
	-- (\x:\R) node (mid-\n)  {}
};

\R=3cm
\draw (54:\R)
\foreach [count=\n] \x in {90,126,162,...,414} {
	-- (\x:\R) node (out-\n) (out-\n) {}
};

\draw[dashed] (out-1) -- (mid-2);
\node[yshift=4pt] at (out-1.north) {\LARGE 4};
\node[xshift=4pt,yshift=4pt] at (mid-2.north east) {\LARGE 2};

\draw (out-2) -- (in-3);
\node[yshift=4pt] at (out-2.north) {\LARGE 1};
\node[xshift=-4pt] at (in-3.north) {\LARGE 3};

\draw[dashed] (out-3) -- (mid-3);
\node[xshift=-4pt] at (out-3.west) {\LARGE 5};
\node[yshift=-4pt] at (mid-3.west) {\LARGE 3};

\draw (out-4) -- (in-4);
\node[xshift=-4pt] at (out-4.west) {\LARGE 2};
\node[yshift=-4pt] at (in-4.west) {\LARGE 4};

\draw[dashed] (out-5) -- (mid-4);
\node[xshift=-4pt] at (out-5.west) {\LARGE 1};
\node[yshift=-4pt] at (mid-4.west) {\LARGE 4};

\draw (out-6) -- (in-5);
\node[xshift=-4pt] at (out-6.west) {\LARGE 3};
\node[yshift=-4pt] at (in-5.west) {\LARGE 5};

\draw[dashed] (out-7) -- (mid-5);
\node[xshift=-4pt] at (out-7.west) {\LARGE 2};
\node[yshift=-4pt] at (mid-5.west) {\LARGE 5};

\draw (out-8) -- (in-1);
\node[xshift=-4pt] at (out-8.west) {\LARGE 4};
\node[yshift=-4pt] at (in-1.west) {\LARGE 1};

\draw[dashed] (out-9) -- (mid-1);
\node[xshift=-4pt] at (out-9.west) {\LARGE 3};
\node[xshift=4pt,yshift=-4pt] at (mid-1.south east) {\LARGE 1};

\draw (out-10) -- (in-2);
\node[xshift=-4pt] at (out-10.west) {\LARGE 5};
\node[xshift=8pt,yshift=4pt] at (in-2.east) {\LARGE 2};

% coloring
\draw[red] (in-1) -- (in-2);
\draw[red, dashed] (mid-1) -- (mid-2);
\draw[red] (out-4) -- (out-5);

\draw[aqua] (in-2) -- (in-3);
\draw[aqua, dashed] (mid-2) -- (mid-3);
\draw[aqua] (out-6) -- (out-7);

\draw[brightgreen] (in-3) -- (in-4);
\draw[brightgreen, dashed] (mid-3) -- (mid-4);
\draw[brightgreen] (out-8) -- (out-9);

\draw[bronze] (in-4) -- (in-5);
\draw[bronze, dashed] (mid-4) -- (mid-5);
\draw[bronze] (out-10) -- (out-1);

\draw[cadmiumyellow] (in-5) -- (in-1);
\draw[cadmiumyellow, dashed] (mid-5) -- (mid-1);
\draw[cadmiumyellow] (out-2) -- (out-3);

\draw[cobalt] (in-2) -- (out-10);
\draw[cobalt, dashed] (mid-5) -- (out-7);
\draw[cobalt] (out-3) -- (out-4);

\draw[hotpink] (out-1) -- (out-2);
\draw[hotpink, dashed] (out-5) -- (mid-4);
\draw[hotpink] (out-8) -- (in-1);

\draw[lavenderindigo] (out-2) -- (in-3);
\draw[lavenderindigo] (out-5) -- (out-6);
\draw[lavenderindigo,dashed] (out-9) -- (mid-1);

\draw[pumpkin] (out-4) -- (in-4);
\draw[pumpkin] (out-7) -- (out-8);
\draw[pumpkin,dashed] (out-1) -- (mid-2);

% face B

\draw[fill=yellow,opacity=0.5] plot coordinates {(in-2) (in-3) (out-2) (out-1) (out-10)};
\draw[fill=yellow,opacity=0.5] plot coordinates {(mid-4) (mid-5) (out-7) (out-6) (out-5)};
\node at (100:2.3cm) {\huge B};

\end{tikzpicture}
\end{document}

{{< /tikz >}}


Face C

{{< tikz >}}

\usepackage{tikz}
\tikzset{style={inner sep=0pt}}
\tikzset{every path/.style={line width=0.4 mm}}
\begin{document}

\begin{tikzpicture}[scale=3]

\definecolor{aqua}{rgb}{0.0, 1.0, 1.0}
\definecolor{brightgreen}{rgb}{0.4, 1.0, 0.0}
\definecolor{bronze}{rgb}{0.8, 0.5, 0.2}
\definecolor{cadmiumyellow}{rgb}{1.0, 0.96, 0.0}
\definecolor{cobalt}{rgb}{0.0, 0.28, 0.67}
\definecolor{hotpink}{rgb}{1.0, 0.41, 0.71}
\definecolor{lavenderindigo}{rgb}{0.58, 0.34, 0.92}
\definecolor{pumpkin}{rgb}{1.0, 0.46, 0.09}

\newdimen\R
\R=2cm


\draw (270:\R)
\foreach [count=\n] \x in {342,414,486,...,630} {
	-- (\x:\R) node (in-\n) {}
};

\R=2.1cm
\draw[dashed] (306:\R)
\foreach [count=\n] \x in {378,450,522,...,666} {
	-- (\x:\R) node (mid-\n)  {}
};

\R=3cm
\draw (54:\R)
\foreach [count=\n] \x in {90,126,162,...,414} {
	-- (\x:\R) node (out-\n) (out-\n) {}
};

\draw[dashed] (out-1) -- (mid-2);
\node[yshift=4pt] at (out-1.north) {\LARGE 4};
\node[xshift=4pt,yshift=4pt] at (mid-2.north east) {\LARGE 2};

\draw (out-2) -- (in-3);
\node[yshift=4pt] at (out-2.north) {\LARGE 1};
\node[xshift=-4pt] at (in-3.north) {\LARGE 3};

\draw[dashed] (out-3) -- (mid-3);
\node[xshift=-4pt] at (out-3.west) {\LARGE 5};
\node[yshift=-4pt] at (mid-3.west) {\LARGE 3};

\draw (out-4) -- (in-4);
\node[xshift=-4pt] at (out-4.west) {\LARGE 2};
\node[yshift=-4pt] at (in-4.west) {\LARGE 4};

\draw[dashed] (out-5) -- (mid-4);
\node[xshift=-4pt] at (out-5.west) {\LARGE 1};
\node[yshift=-4pt] at (mid-4.west) {\LARGE 4};

\draw (out-6) -- (in-5);
\node[xshift=-4pt] at (out-6.west) {\LARGE 3};
\node[yshift=-4pt] at (in-5.west) {\LARGE 5};

\draw[dashed] (out-7) -- (mid-5);
\node[xshift=-4pt] at (out-7.west) {\LARGE 2};
\node[yshift=-4pt] at (mid-5.west) {\LARGE 5};

\draw (out-8) -- (in-1);
\node[xshift=-4pt] at (out-8.west) {\LARGE 4};
\node[yshift=-4pt] at (in-1.west) {\LARGE 1};

\draw[dashed] (out-9) -- (mid-1);
\node[xshift=-4pt] at (out-9.west) {\LARGE 3};
\node[xshift=4pt,yshift=-4pt] at (mid-1.south east) {\LARGE 1};

\draw (out-10) -- (in-2);
\node[xshift=-4pt] at (out-10.west) {\LARGE 5};
\node[xshift=8pt,yshift=4pt] at (in-2.east) {\LARGE 2};

% coloring
\draw[red] (in-1) -- (in-2);
\draw[red, dashed] (mid-1) -- (mid-2);
\draw[red] (out-4) -- (out-5);

\draw[aqua] (in-2) -- (in-3);
\draw[aqua, dashed] (mid-2) -- (mid-3);
\draw[aqua] (out-6) -- (out-7);

\draw[brightgreen] (in-3) -- (in-4);
\draw[brightgreen, dashed] (mid-3) -- (mid-4);
\draw[brightgreen] (out-8) -- (out-9);

\draw[bronze] (in-4) -- (in-5);
\draw[bronze, dashed] (mid-4) -- (mid-5);
\draw[bronze] (out-10) -- (out-1);

\draw[cadmiumyellow] (in-5) -- (in-1);
\draw[cadmiumyellow, dashed] (mid-5) -- (mid-1);
\draw[cadmiumyellow] (out-2) -- (out-3);

\draw[cobalt] (in-2) -- (out-10);
\draw[cobalt, dashed] (mid-5) -- (out-7);
\draw[cobalt] (out-3) -- (out-4);

\draw[hotpink] (out-1) -- (out-2);
\draw[hotpink, dashed] (out-5) -- (mid-4);
\draw[hotpink] (out-8) -- (in-1);

\draw[lavenderindigo] (out-2) -- (in-3);
\draw[lavenderindigo] (out-5) -- (out-6);
\draw[lavenderindigo,dashed] (out-9) -- (mid-1);

\draw[pumpkin] (out-4) -- (in-4);
\draw[pumpkin] (out-7) -- (out-8);
\draw[pumpkin,dashed] (out-1) -- (mid-2);

% face C

\draw[fill=yellow,opacity=0.5] plot coordinates {(in-3) (in-4) (out-4) (out-3) (out-2)};
\draw[fill=yellow,opacity=0.5] plot coordinates {(mid-1) (mid-5) (out-7) (out-8) (out-9)};
\node at (180:2.3cm) {\huge C};


\end{tikzpicture}
\end{document}

{{< /tikz >}}


Face D

{{< tikz >}}

\usepackage{tikz}
\tikzset{style={inner sep=0pt}}
\tikzset{every path/.style={line width=0.4 mm}}
\begin{document}

\begin{tikzpicture}[scale=3]

\definecolor{aqua}{rgb}{0.0, 1.0, 1.0}
\definecolor{brightgreen}{rgb}{0.4, 1.0, 0.0}
\definecolor{bronze}{rgb}{0.8, 0.5, 0.2}
\definecolor{cadmiumyellow}{rgb}{1.0, 0.96, 0.0}
\definecolor{cobalt}{rgb}{0.0, 0.28, 0.67}
\definecolor{hotpink}{rgb}{1.0, 0.41, 0.71}
\definecolor{lavenderindigo}{rgb}{0.58, 0.34, 0.92}
\definecolor{pumpkin}{rgb}{1.0, 0.46, 0.09}

\newdimen\R
\R=2cm


\draw (270:\R)
\foreach [count=\n] \x in {342,414,486,...,630} {
	-- (\x:\R) node (in-\n) {}
};

\R=2.1cm
\draw[dashed] (306:\R)
\foreach [count=\n] \x in {378,450,522,...,666} {
	-- (\x:\R) node (mid-\n)  {}
};

\R=3cm
\draw (54:\R)
\foreach [count=\n] \x in {90,126,162,...,414} {
	-- (\x:\R) node (out-\n) (out-\n) {}
};

\draw[dashed] (out-1) -- (mid-2);
\node[yshift=4pt] at (out-1.north) {\LARGE 4};
\node[xshift=4pt,yshift=4pt] at (mid-2.north east) {\LARGE 2};

\draw (out-2) -- (in-3);
\node[yshift=4pt] at (out-2.north) {\LARGE 1};
\node[xshift=-4pt] at (in-3.north) {\LARGE 3};

\draw[dashed] (out-3) -- (mid-3);
\node[xshift=-4pt] at (out-3.west) {\LARGE 5};
\node[yshift=-4pt] at (mid-3.west) {\LARGE 3};

\draw (out-4) -- (in-4);
\node[xshift=-4pt] at (out-4.west) {\LARGE 2};
\node[yshift=-4pt] at (in-4.west) {\LARGE 4};

\draw[dashed] (out-5) -- (mid-4);
\node[xshift=-4pt] at (out-5.west) {\LARGE 1};
\node[yshift=-4pt] at (mid-4.west) {\LARGE 4};

\draw (out-6) -- (in-5);
\node[xshift=-4pt] at (out-6.west) {\LARGE 3};
\node[yshift=-4pt] at (in-5.west) {\LARGE 5};

\draw[dashed] (out-7) -- (mid-5);
\node[xshift=-4pt] at (out-7.west) {\LARGE 2};
\node[yshift=-4pt] at (mid-5.west) {\LARGE 5};

\draw (out-8) -- (in-1);
\node[xshift=-4pt] at (out-8.west) {\LARGE 4};
\node[yshift=-4pt] at (in-1.west) {\LARGE 1};

\draw[dashed] (out-9) -- (mid-1);
\node[xshift=-4pt] at (out-9.west) {\LARGE 3};
\node[xshift=4pt,yshift=-4pt] at (mid-1.south east) {\LARGE 1};

\draw (out-10) -- (in-2);
\node[xshift=-4pt] at (out-10.west) {\LARGE 5};
\node[xshift=8pt,yshift=4pt] at (in-2.east) {\LARGE 2};

% coloring
\draw[red] (in-1) -- (in-2);
\draw[red, dashed] (mid-1) -- (mid-2);
\draw[red] (out-4) -- (out-5);

\draw[aqua] (in-2) -- (in-3);
\draw[aqua, dashed] (mid-2) -- (mid-3);
\draw[aqua] (out-6) -- (out-7);

\draw[brightgreen] (in-3) -- (in-4);
\draw[brightgreen, dashed] (mid-3) -- (mid-4);
\draw[brightgreen] (out-8) -- (out-9);

\draw[bronze] (in-4) -- (in-5);
\draw[bronze, dashed] (mid-4) -- (mid-5);
\draw[bronze] (out-10) -- (out-1);

\draw[cadmiumyellow] (in-5) -- (in-1);
\draw[cadmiumyellow, dashed] (mid-5) -- (mid-1);
\draw[cadmiumyellow] (out-2) -- (out-3);

\draw[cobalt] (in-2) -- (out-10);
\draw[cobalt, dashed] (mid-5) -- (out-7);
\draw[cobalt] (out-3) -- (out-4);

\draw[hotpink] (out-1) -- (out-2);
\draw[hotpink, dashed] (out-5) -- (mid-4);
\draw[hotpink] (out-8) -- (in-1);

\draw[lavenderindigo] (out-2) -- (in-3);
\draw[lavenderindigo] (out-5) -- (out-6);
\draw[lavenderindigo,dashed] (out-9) -- (mid-1);

\draw[pumpkin] (out-4) -- (in-4);
\draw[pumpkin] (out-7) -- (out-8);
\draw[pumpkin,dashed] (out-1) -- (mid-2);

% face D

\draw[fill=yellow,opacity=0.5] plot coordinates {(in-4) (in-5) (out-6) (out-5) (out-4)};
\draw[fill=yellow,opacity=0.5] plot coordinates {(mid-1) (mid-2) (out-1) (out-10) (out-9)};
\node at (250:2.3cm) {\huge D};


\end{tikzpicture}
\end{document}

{{< /tikz >}}


Face E


{{< tikz >}}

\usepackage{tikz}
\tikzset{style={inner sep=0pt}}
\tikzset{every path/.style={line width=0.4 mm}}
\begin{document}

\begin{tikzpicture}[scale=3]

\definecolor{aqua}{rgb}{0.0, 1.0, 1.0}
\definecolor{brightgreen}{rgb}{0.4, 1.0, 0.0}
\definecolor{bronze}{rgb}{0.8, 0.5, 0.2}
\definecolor{cadmiumyellow}{rgb}{1.0, 0.96, 0.0}
\definecolor{cobalt}{rgb}{0.0, 0.28, 0.67}
\definecolor{hotpink}{rgb}{1.0, 0.41, 0.71}
\definecolor{lavenderindigo}{rgb}{0.58, 0.34, 0.92}
\definecolor{pumpkin}{rgb}{1.0, 0.46, 0.09}

\newdimen\R
\R=2cm


\draw (270:\R)
\foreach [count=\n] \x in {342,414,486,...,630} {
	-- (\x:\R) node (in-\n) {}
};

\R=2.1cm
\draw[dashed] (306:\R)
\foreach [count=\n] \x in {378,450,522,...,666} {
	-- (\x:\R) node (mid-\n)  {}
};

\R=3cm
\draw (54:\R)
\foreach [count=\n] \x in {90,126,162,...,414} {
	-- (\x:\R) node (out-\n) (out-\n) {}
};

\draw[dashed] (out-1) -- (mid-2);
\node[yshift=4pt] at (out-1.north) {\LARGE 4};
\node[xshift=4pt,yshift=4pt] at (mid-2.north east) {\LARGE 2};

\draw (out-2) -- (in-3);
\node[yshift=4pt] at (out-2.north) {\LARGE 1};
\node[xshift=-4pt] at (in-3.north) {\LARGE 3};

\draw[dashed] (out-3) -- (mid-3);
\node[xshift=-4pt] at (out-3.west) {\LARGE 5};
\node[yshift=-4pt] at (mid-3.west) {\LARGE 3};

\draw (out-4) -- (in-4);
\node[xshift=-4pt] at (out-4.west) {\LARGE 2};
\node[yshift=-4pt] at (in-4.west) {\LARGE 4};

\draw[dashed] (out-5) -- (mid-4);
\node[xshift=-4pt] at (out-5.west) {\LARGE 1};
\node[yshift=-4pt] at (mid-4.west) {\LARGE 4};

\draw (out-6) -- (in-5);
\node[xshift=-4pt] at (out-6.west) {\LARGE 3};
\node[yshift=-4pt] at (in-5.west) {\LARGE 5};

\draw[dashed] (out-7) -- (mid-5);
\node[xshift=-4pt] at (out-7.west) {\LARGE 2};
\node[yshift=-4pt] at (mid-5.west) {\LARGE 5};

\draw (out-8) -- (in-1);
\node[xshift=-4pt] at (out-8.west) {\LARGE 4};
\node[yshift=-4pt] at (in-1.west) {\LARGE 1};

\draw[dashed] (out-9) -- (mid-1);
\node[xshift=-4pt] at (out-9.west) {\LARGE 3};
\node[xshift=4pt,yshift=-4pt] at (mid-1.south east) {\LARGE 1};

\draw (out-10) -- (in-2);
\node[xshift=-4pt] at (out-10.west) {\LARGE 5};
\node[xshift=8pt,yshift=4pt] at (in-2.east) {\LARGE 2};

% coloring
\draw[red] (in-1) -- (in-2);
\draw[red, dashed] (mid-1) -- (mid-2);
\draw[red] (out-4) -- (out-5);

\draw[aqua] (in-2) -- (in-3);
\draw[aqua, dashed] (mid-2) -- (mid-3);
\draw[aqua] (out-6) -- (out-7);

\draw[brightgreen] (in-3) -- (in-4);
\draw[brightgreen, dashed] (mid-3) -- (mid-4);
\draw[brightgreen] (out-8) -- (out-9);

\draw[bronze] (in-4) -- (in-5);
\draw[bronze, dashed] (mid-4) -- (mid-5);
\draw[bronze] (out-10) -- (out-1);

\draw[cadmiumyellow] (in-5) -- (in-1);
\draw[cadmiumyellow, dashed] (mid-5) -- (mid-1);
\draw[cadmiumyellow] (out-2) -- (out-3);

\draw[cobalt] (in-2) -- (out-10);
\draw[cobalt, dashed] (mid-5) -- (out-7);
\draw[cobalt] (out-3) -- (out-4);

\draw[hotpink] (out-1) -- (out-2);
\draw[hotpink, dashed] (out-5) -- (mid-4);
\draw[hotpink] (out-8) -- (in-1);

\draw[lavenderindigo] (out-2) -- (in-3);
\draw[lavenderindigo] (out-5) -- (out-6);
\draw[lavenderindigo,dashed] (out-9) -- (mid-1);

\draw[pumpkin] (out-4) -- (in-4);
\draw[pumpkin] (out-7) -- (out-8);
\draw[pumpkin,dashed] (out-1) -- (mid-2);

% face E

\draw[fill=yellow,opacity=0.5] plot coordinates {(in-5) (in-1) (out-8) (out-7) (out-6)};
\draw[fill=yellow,opacity=0.5] plot coordinates {(mid-2) (mid-3) (out-3) (out-2) (out-1)};
\node at (300:2.3cm) {\huge E};


\end{tikzpicture}
\end{document}

{{< /tikz >}}


Face F



{{< tikz >}}

\usepackage{tikz}
\tikzset{style={inner sep=0pt}}
\tikzset{every path/.style={line width=0.4 mm}}
\begin{document}

\begin{tikzpicture}[scale=3]

\definecolor{aqua}{rgb}{0.0, 1.0, 1.0}
\definecolor{brightgreen}{rgb}{0.4, 1.0, 0.0}
\definecolor{bronze}{rgb}{0.8, 0.5, 0.2}
\definecolor{cadmiumyellow}{rgb}{1.0, 0.96, 0.0}
\definecolor{cobalt}{rgb}{0.0, 0.28, 0.67}
\definecolor{hotpink}{rgb}{1.0, 0.41, 0.71}
\definecolor{lavenderindigo}{rgb}{0.58, 0.34, 0.92}
\definecolor{pumpkin}{rgb}{1.0, 0.46, 0.09}

\newdimen\R
\R=2cm


\draw (270:\R)
\foreach [count=\n] \x in {342,414,486,...,630} {
	-- (\x:\R) node (in-\n) {}
};

\R=2.1cm
\draw[dashed] (306:\R)
\foreach [count=\n] \x in {378,450,522,...,666} {
	-- (\x:\R) node (mid-\n)  {}
};

\R=3cm
\draw (54:\R)
\foreach [count=\n] \x in {90,126,162,...,414} {
	-- (\x:\R) node (out-\n) (out-\n) {}
};

\draw[dashed] (out-1) -- (mid-2);
\node[yshift=4pt] at (out-1.north) {\LARGE 4};
\node[xshift=4pt,yshift=4pt] at (mid-2.north east) {\LARGE 2};

\draw (out-2) -- (in-3);
\node[yshift=4pt] at (out-2.north) {\LARGE 1};
\node[xshift=-4pt] at (in-3.north) {\LARGE 3};

\draw[dashed] (out-3) -- (mid-3);
\node[xshift=-4pt] at (out-3.west) {\LARGE 5};
\node[yshift=-4pt] at (mid-3.west) {\LARGE 3};

\draw (out-4) -- (in-4);
\node[xshift=-4pt] at (out-4.west) {\LARGE 2};
\node[yshift=-4pt] at (in-4.west) {\LARGE 4};

\draw[dashed] (out-5) -- (mid-4);
\node[xshift=-4pt] at (out-5.west) {\LARGE 1};
\node[yshift=-4pt] at (mid-4.west) {\LARGE 4};

\draw (out-6) -- (in-5);
\node[xshift=-4pt] at (out-6.west) {\LARGE 3};
\node[yshift=-4pt] at (in-5.west) {\LARGE 5};

\draw[dashed] (out-7) -- (mid-5);
\node[xshift=-4pt] at (out-7.west) {\LARGE 2};
\node[yshift=-4pt] at (mid-5.west) {\LARGE 5};

\draw (out-8) -- (in-1);
\node[xshift=-4pt] at (out-8.west) {\LARGE 4};
\node[yshift=-4pt] at (in-1.west) {\LARGE 1};

\draw[dashed] (out-9) -- (mid-1);
\node[xshift=-4pt] at (out-9.west) {\LARGE 3};
\node[xshift=4pt,yshift=-4pt] at (mid-1.south east) {\LARGE 1};

\draw (out-10) -- (in-2);
\node[xshift=-4pt] at (out-10.west) {\LARGE 5};
\node[xshift=8pt,yshift=4pt] at (in-2.east) {\LARGE 2};

% coloring
\draw[red] (in-1) -- (in-2);
\draw[red, dashed] (mid-1) -- (mid-2);
\draw[red] (out-4) -- (out-5);

\draw[aqua] (in-2) -- (in-3);
\draw[aqua, dashed] (mid-2) -- (mid-3);
\draw[aqua] (out-6) -- (out-7);

\draw[brightgreen] (in-3) -- (in-4);
\draw[brightgreen, dashed] (mid-3) -- (mid-4);
\draw[brightgreen] (out-8) -- (out-9);

\draw[bronze] (in-4) -- (in-5);
\draw[bronze, dashed] (mid-4) -- (mid-5);
\draw[bronze] (out-10) -- (out-1);

\draw[cadmiumyellow] (in-5) -- (in-1);
\draw[cadmiumyellow, dashed] (mid-5) -- (mid-1);
\draw[cadmiumyellow] (out-2) -- (out-3);

\draw[cobalt] (in-2) -- (out-10);
\draw[cobalt, dashed] (mid-5) -- (out-7);
\draw[cobalt] (out-3) -- (out-4);

\draw[hotpink] (out-1) -- (out-2);
\draw[hotpink, dashed] (out-5) -- (mid-4);
\draw[hotpink] (out-8) -- (in-1);

\draw[lavenderindigo] (out-2) -- (in-3);
\draw[lavenderindigo] (out-5) -- (out-6);
\draw[lavenderindigo,dashed] (out-9) -- (mid-1);

\draw[pumpkin] (out-4) -- (in-4);
\draw[pumpkin] (out-7) -- (out-8);
\draw[pumpkin,dashed] (out-1) -- (mid-2);

% face F

\draw[fill=yellow,opacity=0.5] plot coordinates {(in-1) (in-2) (out-10) (out-9) (out-8)};
\draw[fill=yellow,opacity=0.5] plot coordinates {(mid-3) (mid-4) (out-5) (out-4) (out-3)};
\node at (180:2.3cm) {\huge F};


\end{tikzpicture}
\end{document}

{{< /tikz >}}


And here is the edges with their color code:

{{< tikz >}}

\usepackage{tikz}
\tikzset{every path/.style={line width=0.4 mm}}
\begin{document}

\begin{tikzpicture}[scale=3]

\definecolor{aqua}{rgb}{0.0, 1.0, 1.0}
\definecolor{brightgreen}{rgb}{0.4, 1.0, 0.0}
\definecolor{bronze}{rgb}{0.8, 0.5, 0.2}
\definecolor{cadmiumyellow}{rgb}{1.0, 0.96, 0.0}
\definecolor{cobalt}{rgb}{0.0, 0.28, 0.67}
\definecolor{hotpink}{rgb}{1.0, 0.41, 0.71}
\definecolor{lavenderindigo}{rgb}{0.58, 0.34, 0.92}
\definecolor{pumpkin}{rgb}{1.0, 0.46, 0.09}

\filldraw[fill=aqua] (-5,0) circle (10pt) node {\huge a};
\filldraw[fill=brightgreen] (-4,0) circle (10pt) node {\huge b};
\filldraw[fill=bronze] (-3,0) circle (10pt) node {\huge c};
\filldraw[fill=cadmiumyellow] (-2,0) circle (10pt) node {\huge d};
\filldraw[fill=cobalt] (-1,0) circle (10pt) node {\huge e};
\filldraw[fill=hotpink] (0,0) circle (10pt) node {\huge f};
\filldraw[fill=lavenderindigo] (1,0) circle (10pt) node {\huge g};
\filldraw[fill=pumpkin] (2,0) circle (10pt) node {\huge h};
\filldraw[fill=red] (3,0) circle (10pt) node {\huge i};
\filldraw[fill=black,text=gray] (4,0) circle (10pt) node {\huge j};


\end{tikzpicture}
\end{document}

{{< /tikz >}}


So $d(A) = i+a+b+c+d$, $d(B)=-a+e-c+f+g$, $d(C)=-b-g-d-e+h$, $d(D)=-c-h-i+g+j$, $d(E)=-d-j+a+h+f$, $d(F)=-i-f-b+j-e$

The differential of edges should be clear.

So we have the following cellular chain:

$\mathbb{Z}^5 \xleftarrow{A} \mathbb{Z}^{10} \xleftarrow{B} \mathbb{Z}^6 \xleftarrow{0} \mathbb{Z}$

where 

$A = \begin{pmatrix}  0 & 0 & 0 & -1 & 0 & -1 & 1 & 0 & 1 & 0 \\\\  1 & 0 & 0 & 0 & 1 & 0 & 0 & 1 & -1 & 0 \\\\ -1 & 1 & 0 & 0 & 0 & 0 & -1 & 0 & 0 & 1 \\\\ 0 & -1 & 1 & 0 & 0 & 1 & 0 & -1 & 0 & 0 \\\\ 0 & 0 & -1 & 1 & -1 & 0 & 0 & 0 & 0 & -1  \end{pmatrix}$ 

 $B = \begin{pmatrix}  1 & -1 & 0 & 0 & 1 & 0\\\\  1 & 0 & -1 & 0 & 0 & -1\\\\ 1 & -1 & 0 & -1 & 0 & 0\\\\ 1 & 0 & -1 & 0 & -1 & 0\\\\ 0 & 1 & -1 & 0 & 0 & -1\\\\ 0 & 1 & 0 & 0 & 1 & -1\\\\ 0 & 1 & -1 & 1 & 0 & 0\\\\ 0 & 0 & 1 & -1 & 1 & 0\\\\ 1 & 0 & 0 & -1 & 0 & -1\\\\ 0 & 0 & 0 & 1 & -1 & 1  \end{pmatrix}$


 (God I hate huge matrices)

 So $\texttt{ker} B = 0$, $\texttt{ker} A \cong \mathbb{Z}^6$ and we get $\tilde{H}_n (X) = \mathbb{Z}$ for $n = 3$ and $0$ otherwise, the same as $\mathbb{S}^3$.

 It's been a toil... maybe this is something like diagram chasing - not difficult, but better to do it in private :smile:
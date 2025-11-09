---
draft: true
title: "Calculating the homology of Poincaré's sphere through dodecahedron"
math: true
tikz: true
date: 2025-11-10T04:01:59+08:00
TocOpen: true
categories: ["mathematics"]
tags: ['alegbraic-topology', 'homology', 'CW-complex']
cover:
  image: "https://images.unsplash.com/photo-1728406970522-1d42256abec8?ixlib=rb-4.1.0&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&q=80&w=1170"
---

## Dodecahedron

Below is a figure showing the identified vertices of the dodecahedron aftering taking quotient:

{{< tikz >}}

\usepackage{tikz}
\usetikzlibrary{positioning,chains,fit,shapes,calc}
\tikzset{style={inner sep=0pt}}
\begin{document}

\begin{tikzpicture}

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
\node[yshift=4pt] at (out-1.north) {4};
\node[xshift=-4pt] at (mid-2.north) {2};

\draw (out-2) -- (in-3);
\node[yshift=4pt] at (out-2.north) {1};
\node[xshift=-4pt] at (in-3.north) {3};

\draw[dashed] (out-3) -- (mid-3);
\node[xshift=-4pt] at (out-3.west) {5};
\node[yshift=-4pt] at (mid-3.west) {3};

\draw (out-4) -- (in-4);
\node[xshift=-4pt] at (out-4.west) {2};
\node[yshift=-4pt] at (in-4.west) {4};

\draw[dashed] (out-5) -- (mid-4);
\node[xshift=-4pt] at (out-5.west) {1};
\node[yshift=-4pt] at (mid-4.west) {4};

\draw (out-6) -- (in-5);
\node[xshift=-4pt] at (out-6.west) {3};
\node[yshift=-4pt] at (in-5.west) {5};

\draw[dashed] (out-7) -- (mid-5);
\node[xshift=-4pt] at (out-7.west) {2};
\node[yshift=-4pt] at (mid-5.west) {5};

\draw (out-8) -- (in-1);
\node[xshift=-4pt] at (out-8.west) {4};
\node[yshift=-4pt] at (in-1.west) {1};

\draw[dashed] (out-9) -- (mid-1);
\node[xshift=-4pt] at (out-9.west) {3};
\node[yshift=-4pt] at (mid-1.west) {1};

\draw (out-10) -- (in-2);
\node[xshift=-4pt] at (out-10.west) {5};
\node[yshift=-4pt] at (in-2.west) {2};

\end{tikzpicture}
\end{document}

{{< /tikz >}}
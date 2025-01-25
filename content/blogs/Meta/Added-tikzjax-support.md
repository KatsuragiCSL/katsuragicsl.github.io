---
title: "Added tikzjax support"
tikz: true
date: 2025-01-25T17:37:38+08:00
categories: ["meta"]
---

Just added support for tikzjax since I received some feedback about my hand-drawn diagrams are hard to read...now I can use nice graphs like these:

{{< tikz >}}
\usepackage{tikz-cd}
\tikzcdset{scale cd/.style={every label/.append style={scale=#1},
    cells={nodes={scale=#1}}}}
\begin{document}
  \begin{tikzcd}[scale cd=2]
    A \arrow[r, "\phi"] \arrow[d, red]
      & B \arrow[d, "\psi" red] \\
    C \arrow[r, red, "\eta" blue]
      & |[blue, rotate=-15]| D
  \end{tikzcd}
\end{document}
{{< /tikz >}}


{{< tikz >}}
\usepackage{tikz-cd}
\begin{document}
  \begin{tikzpicture}
    \draw (0,0) circle (1in);
  \end{tikzpicture}
\end{document}
{{< /tikz >}}

{{< tikz >}}
\usepackage{chemfig}
\begin{document}
\chemfig{[:-90]HN(-[::-45](-[::-45]R)=[::+45]O)>[::+45]*4(-(=O)-N*5(-(<:(=[::-60]O)-[::+60]OH)-(<[::+0])(<:[::-108])-S>)--)}
\end{document}
{{< /tikz >}}

{{< tikz >}}
\usepackage{tikz}
\usepackage{tikz-3dplot}
\usetikzlibrary{math}
%
% File name: surface-of-revolution.tex
% Description: 
% A geometric representation of a surface of revolution is shown.
% 
% Date of creation: October, 17th, 2021.
% Date of last modification: October, 9th, 2022.
% Author: Efraín Soto Apolinar.
% https://www.aprendematematicas.org.mx/author/efrain-soto-apolinar/instructing-courses/
% Source: page 450 of the 
% Glosario Ilustrado de Matem\'aticas Escolares.
% https://tinyurl.com/5udm2ufy
%
% Terms of use:
% According to TikZ.net
% https://creativecommons.org/licenses/by-nc-sa/4.0/
% Your commitment to the terms of use is greatly appreciated.
%
\begin{document}
	%
	\tdplotsetmaincoords{60}{130}
	\begin{tikzpicture}[tdplot_main_coords]
		% The function that is rotated
		\tikzmath{function f(\x) {return 1.5 - 0.35*sin(\x r);};}
		\pgfmathsetmacro{\dominio}{2.0}
		\pgfmathsetmacro{\xi}{-\dominio}
		\pgfmathsetmacro{\step}{(\dominio-\xi)/70.0}
		\pgfmathsetmacro{\xs}{\xi+\step}
		\pgfmathsetmacro{\max}{3}
		% Circumferences (behind the coordiante axis)
		\foreach \x in {\xi,\xs,...,\dominio}{
			\pgfmathsetmacro{\radio}{f(\x)}	% radius of the circumference of the solid of revolution
			\draw[cyan,very thick,opacity=0.35] plot[domain=0.5*pi:2.0*pi,smooth,variable=\t] ({\radio*cos(\t r)},{\x},{\radio*sin(\t r});	
		}
		% Part of the solid of revolution behind the coordinate axis
		\foreach \angulo in {358,356,...,90}{
			\draw[cyan,very thick,rotate around y=\angulo,opacity=0.35] plot[domain=-\dominio:\dominio,smooth,variable=\t] ({0},{\t},{f(\t)});
		}
		% Graph of the function rotated about the $y$ axis
		\draw[red,ultra thick] plot[domain=-\dominio:\dominio,smooth,variable=\t] ({0},{\t},{f(\t)}) node [above right] {$z = f(y)$};
		% Coordinate axis
		\draw[thick,->] (0,0,0) -- (0,\max,0) node [right] {$y$};
		\draw[thick,->] (0,0,0) -- (\max,0,0) node [left] {$x$};
		\draw[thick,->] (0,0,0) -- (0,0,\max) node [above] {$z$};
		% Circumferences (in front of the coordiante axis)
		\foreach \x in {\xi,\xs,...,\dominio}{
			\pgfmathsetmacro{\radio}{f(\x)}	% Radio del círculo al inicio del sólido de revolución
			\draw[cyan,very thick,opacity=0.35] plot[domain=0.0:0.5*pi,smooth,variable=\t] ({\radio*cos(\t r)},{\x},{\radio*sin(\t r});	
		}
		% The solid of revolution (in front of the coordinate axis)
		\foreach \angulo in {0,2,...,89}{
			\draw[cyan,very thick,rotate around y=\angulo,opacity=0.35] plot[domain=-\dominio:\dominio,smooth,variable=\t] ({0},{\t},{f(\t)});
		}
	\end{tikzpicture}
\end{document}
{{< /tikz >}}
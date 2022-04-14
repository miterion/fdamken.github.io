---
title: "LaTeX Tips & Tricks"
draft: false
date: 2022-02-18
---

I use LaTeX a lot.
In fact, all of my [summaries](/summaries) are written in LaTeX.
Over the years, I found and got used to some tips and tricks that enhance the experience with LaTeX a lot.
I figured it might be useful to collect them in one place, as others might find them useful too.

This page is still a draft will most likely always stay one.
I'll expand it once I find something new, exciting, and useful but it may never be complete.

Last Updated: {{% param lastmod %}} (if someone knows how to format the `lastmod` parameter in Hugo's Markdown renderer, please contact me :D)


## Aligning Subfigure Captions
The `subfigure` environment (from the `subcaption` package) is extremely power- and helpful for placing multiple figures in a single figure.
However, they sometimes look bad if the subcaptions to not align.
This can be fixed by providing the `b`-option (standing for *bottom*) to the subfigures:
```latex
\begin{subfigure}[b]{0.5\linewidth}
    ...
\end{subfigure}
```


## Automatic Space Behind Macro Content
Sometimes, a macro is used for abbreviating a long phrase or ensuring consistency (e.g., `\newcommand{\simtoreal}{sim-to-real}`).
However, LaTeX eats up all whitespace causing texts like “sim-to-realis able”.
This can be fixed with the package `xspace`:
```latex
\usepackage{xspace}
\newcommand{\simtoreal}{sim-to-real\xspace}
```
Opposed to putting a `~`, this has the advantage that the space is not added if the macro is followed by punctuation (e.g., `\simtoreal.`).


## Automatically Using Correct Quotation Marks
Instead of using `` `"`` and quirky things to generate quotation marks pointing in the right direction („“ in German, “” in English), use
```latex
\usepackage{csquotes}
\MakeOuterQuote{"}
```
Now it is possible to just write `"using straight quotes"` and it will be rendered `“using the correct quotes”` without any hassle.
`csquotes` automatically chooses the correct marks based in the language used in the `babel` package.


## Gaussian Elimination
To typeset systems of linear equations and Gaussian elimination, the [`gauss`](https://www.ctan.org/tex-archive/macros/latex/contrib/gauss) package is extremely useful.
It allows documenting the operations (e.g., adding one row to another) applied to the matrix/the system of linear equations reoresent by the coefficient matrix.


## Only Number Referenced Equations
Instead of relying on the starred environments like `equation*` and `align*` to not number specific equations, `amsmath` allows to automatically number only equations that are references by placing
```latex
\mathtoolsset{showonlyrefs}
```
in the preamble. To always show tags set manually (e.g., to name equations) even if they are not referenced, use
```latex
\mathtoolsset{showonlyrefs,showmanualtags}
```
This is probably the most used one.


## Printing Page/Line Width
When generating images with other tools, e.g., Matplotlib, it is important to match the document's width (or height) such that the font size matches.
However, it can be tedious to measure the width by hand.
This is automated with the `layouts` package:
```latex
\usepackage{layouts}
\begin{document}
    \printinunitsof{cm}\prntlen{\linewidth}
\end{document}
```
Other units (such as `in` for inch which is useful for Matplotlib) can be chosen, too.


## Scaling TikZ Pictures and PGF Plots
Stemming from [this TeXExchange question](https://tex.stackexchange.com/q/36297/117107) on scaling pgfplots, the neat package `tikzscale` was created that enables to use `\includegraphics` for TikZ-pictures, too:
```latex
\usepackage{tikzscale}
\begin{document}
    \includegrphics[width=\linewidth]{some-picture.tikz}
\end{document}
```
The file `some-picture.tikz` contains just the `\begin{tikzpicture} … \end{tikzpicture}` part.
Everything except for text is scaled, making TikZ-picture and PGF plots a thousand times more useful.


## Setting the Starting `enumerate`-Number
It is possible to set the number an `enumerate` starts counting with by setting the counter `enumi` to how many items have been “shown before”:
```latex
\begin{enumerate}
    \setcounter{enumi}{3}
    \item This will be compiled as the fourth item.
    \item This will be compiled as the fifth item.
    \item This will be compiled as the sixth item.
\end{enumerate}
```
This can be useful to show intermediate texts.


## Streamlining Matplotlib Plots
Drawing plots in Matplotlib is nice, but including them in documents is horrible as they are never correctly scaled, use different fonts, etc.
Using [tikzplotlib](https://pypi.org/project/tikzplotlib) circumvents all this by generating a PGF plot from a figure that can be included in TeX.
This is ideally combined with the TeX package `tikzscale` introduced before.
Some more minor tips:
- Export the figure as a TeX file: `tikzplotlib.save("some-picture.tikz")`
- Clean the figure before exporting to reduce PDF render time: `tikzplotlib.clean_figure(fig=fig)` (remove the keyword argument to use the non-oop API of Matplotlib).
- Use (in Python) `tikzplotlib.Flavors.latex.preamble()` to get the code that has to be put in the TeX preamble in order for the exports to compile.
- When combined with `tikzscale`, you can add `[trim axis left]` to the end of the first exported line to scale w.r.t. the figure body and not the labels.


## Tooling and Utilites
This section does not cover things that can be directly applied in LaTeX, but some tooling and utilities that can make your life a lot easier.

### Capitalizing Titles
Capitalizing titles in American English is hard as it is not directly obvious which words to capitalize and which not.
[![Capitalize My Title](https://capitalizemytitle.com/wp-content/uploads/2020/11/logo-v1.svg)](https://capitalizemytitle.com/style/AMA)
helps with this by automatically capitalizing the title according to the selected style.
I prefer [AMA capitalization](https://capitalizemytitle.com/#capitalizationrules) rules as it [“is mainly used in the scientific community.”](https://capitalizemytitle.com/#capitalizationrules)
However, choose the style that best fits your needs!

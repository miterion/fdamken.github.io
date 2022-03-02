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
\usepackage{layout}
\begin{document}
    \printinunitsof{cm}\prntlen{\linewidth}
\end{document}
```
Other units (such as `in` for inch which is useful for Matplotlib) can be chosen, too.


## Tooling and Utilites
This section does not cover things that can be directly applied in LaTeX, but some tooling and utilities that can make your life a lot easier.

### Capitalizing Titles
Capitalizing titles in American English is hard as it is not directly obvious which words to capitalize and which not.
[![Capitalize My Title](https://capitalizemytitle.com/wp-content/uploads/2020/11/logo-v1.svg)](https://capitalizemytitle.com/style/AMA)
helps with this by automatically capitalizing the title according to the selected style.
I prefer [AMA capitalization](https://capitalizemytitle.com/#capitalizationrules) rules as it [“is mainly used in the scientific community.”](https://capitalizemytitle.com/#capitalizationrules)
However, choose the style that best fits your needs!

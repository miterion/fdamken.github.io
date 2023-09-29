---
title: "LaTeX Best Practices"
draft: true
---

I use LaTeX a lot.
And every time I work with other people, I notice things people to weirdly when using LaTeX, not pushing it to its full potential or simply doing things that are “dangerous.”
Of course, not dangerous in the sense of physically hurting anybody, but in risking a non-robust document, weird typesetting, or simply an unpleasant document.
Thus, I decided to collect this list of “best practices” so that I can refer to it and, of course, to make these things more well-known.

If you want to contribute, [feel free to create an issue](https://github.com/fdamken/fdamken.github.io/issues/) or [submit a pull request](https://github.com/fdamken/fdamken.github.io/pulls).
Thanks to [Heiko](https://miterion.de/) who helped extending this list.

Note that this is a bit different from my [LaTeX tips & tricks]({{< relref "latex/tips-and-tricks" >}}) and a lot more basic, although I will refer to said page from time to time.


## Best Practices
- Figures
    - Figures belong in `figure` environment, tables in `table` environments, listings in the respective listing environment, etc. [Go to full explanation.](#figure-placement)
    - Figures, tables, algorithms, listings, etc. are _floating_ objects. Do not enforce figure placement, LaTeX knows what it is doing. [Go to full explanation.](#figure-placement)
    - If a small image is tighlty bound to a piece of text and does not carry meaning in itself, it is not a figure. Place it in a `center` environment and keep it where it is.
    - Never place figures within text, they should _float_ to the top (or bottom) of the page. Let LaTeX handle this. [Go to full explanation.](#figure-placement)
- General
    - **Never** allow compilation erorrs to persist in your document. If you are using Overleaf, change `Try to compile despite errors` to `Stop on first error` in the menu next to the `Recompile` button to remind you of this. [Go to full explanation.](#never-allow-errors-to-persist)
    - Set your encoding correctly using `\usepackage[utf8]{inputenc}` to type umlauts without shenanigans such as `\"a` or use LuaLaTeX which handles this correctly.
    - Use an acronym package to automatically introduce acronyms appropriately. Use [`acronym`](#handling-acronyms-acronym) if you just need the handling (for small documents such as papers) and [`glossaries`](#handling-acronyms-glossaries) if you need a glossary (for large documents such as theses).
    - [Use `csquotes` for placing quotation marks.](/latex/tips-and-tricks/#automatically-using-correct-quotation-marks) Only use `"` and `'` in the code, never `‚`, `‘`, `’`, `„`, `“`, `”`, or similar.
- Math
    - Do not use “plain symbols” such as `||`/`...`/etc.. Instead use `\Vert`/`\dots`/etc. [Go to full explanation.](#do-not-use-plain-symbols)
    - Do not use `\text` for “operators,” instead use `\mathrm`. Example: Use `\( D_\mathrm{KL} \)`, not `\( D_\text{KL} \)`. [Go to full explanation.](#do-not-use-text-for-operators)
    - Prefer `\( … \)` over `$ … $` and prefer `\[ … \]` over `$$ … $$`. The dolar notation is a TeX primitive and not meant to be used in LaTeX documents.
    - Use left/right versions of symbols, e.g., `\lvert` and `\rvert` instead of `\vert` whenever semantically reasonable. [Go to full explanation.](#use-leftright-versions-of-symbols)
- Referencing
    - Do not use plain `\ref`s, use `cleveref` and `\cref` or at least `\autoref`. [Go to full explanation.](#do-not-use-plain-ref)
    - Label equations only when they are references. [This can be done automatically.](/latex/tips-and-tricks/#only-number-referenced-equations)
- Typesettings
    - Use `\emph` instead of `\textit`, `\textbf`, or similar for emphasizing. `\emph` is made for emphasizing, can be configured globally, and _toggles_ the font style rather than setting it (i.e., withing an italic text, emphasized words will become straight).


## Full Explanations
Some of the above items need a longer explanation, which is contained in this section.
Note that this section does not contain all best practices and for an exhaustive read, go [here](#best-practices).

### Figures
#### Figure Placement
TODO

### General
#### Handling Acronyms: `acronym`
TODO

#### Handling Acronyms: `glossaries`
TODO

#### Never Allow Errors to Persist
TODO

### Math
#### Do Not Use Plain Symbols
TODO

#### Do Not Use `\text` For Operators
Using `\text` changes the font familiy to the document’s text family while `\mathrm` retains the math font but removes spacing that would otherwise be placed between letters.
Note that for actual text, `\text` can still be used and `\mathrm` removes all spaces (which should never be used in math operators anyway).

#### Use Left/Right Versions of Symbols
TODO

### Referencing
#### Do Not Use Plain `\ref`
TODO


## Notes
This is an unstructured list of things that will be added to list of best practices, but they are not yet formulated well enough.
For completeness and transparency, I will keep them here.
- **format you code**
- decide whether you want to reference equations or embed them in the text; be consistent
- a multi-line equations that should get a single number should be an `aligned` environment inside one `equation`
- use `\DeclareMathOperator`
- prefer `tikzplotlib` over `pgf` over `pdf` over `png` when building figures
	- really never use `png`
	- `tikz` renderings can be cached to speedup compilation time
- use a build tool like `arara` for complex documents
- use `siunitx` for units, numbers, ranges, uncertainties, etc.
- also use `siunitx` for number alignment in tables
- use `\textsuperscript` and `\textsubscript` instead of ‘spontaneous math mode’
- use `\prescript` (or so) instead of `^2T_1`; the latter binds to the wrong symbol
- place every sentence on a new line to make finding compiler errors easier (opinionated)
- use `physics` package for easier, well, physics; but this includes all derivatives, integrals, etc.
- `\/`
- touch layouting only if absolutely necessary; avoid vspace, hspace, minipage, etc. LaTeX knows what it's doing
- Read. Documentation. Most packages have an excellent documentation and reading it helps a lot
- do not rely on parenthesis/brackets/… autoscaling, it looks horrible most of the time
- Use the biblatex package with the Biber backend instead of natbib (or even bibtex directly)
- Try to compile your document with as few warnings as possible. Use SuppressWarning if you want to ignore a specific one to get a cleaner output.
- Do not ignore overfull/underfull hbox or vbox. That warning is *literally* telling you that your document looks shitty somewhere
- use xspace for proper spacing after a stop
- Use booktabs instead of standard tabulars
- Typeset numbers in math font (using siunitx) off they are ‘technical.’ E.g., `we used a learning rate of \num{0.12} and we are 14 people in our lab.``
- Be aware of cool features like `\underbrace`, `\mathclap`, `\phantom`, `\makeeqbox`, etc.
- Don't use `\frac` in inline mode
- Use `\todonotes` (although it can become quite slow with too many todos)
- Know the difference between `\input` and `\include`, and use both of them appropriately
- Know that you can tell latex to just compile some `\includes` while still reading the aux file for labels, saving a ton of compilation time during writing
- Do a clean compile from time to time to check everything is working. Even better, set up a CI
- Know the difference between hyphen, en- and en-dash and use all three appropriately
- Place a `~` right before a cite
- Handle inter-word and inter-sentence spaces correctly. Use `\ ` and `\@` if necessary.
- Configure hyphenation if necessary
- Use datetime for date/time formatting and consistency with the locale
- Center captions if they are too short and left-align them if they are more than one line long. This can be done automatically.
- `microtype`
- don't use `\[ … \]` or `$$ … $$`, use an equation environment instead
- know the differences between `equation`, `gather`, and `align`
- don't define labels multiple times (ideally create labels in the moment you want to reference them)
- make sure no figures is left unreferences
- make sure no unresolved references remain (**read the warnings**)
- whenever you feel like you need a `[vh]space`, think again; you probably do not need it
	- want to space out two parts of an equation? use align
    - `\quad` and `\qquad` are also great alternatives to provide typographically sound spacing

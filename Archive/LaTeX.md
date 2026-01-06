
---

# 🧮 LaTeX Complete Cheat Sheet

A concise yet comprehensive reference for writing documents in LaTeX — from basics to advanced IEEE/academic formatting.

---

## 🏗️ 1. Basic Structure

```latex
\documentclass[options]{class}

\usepackage{package1}
\usepackage{package2}

\begin{document}

Your content here.

\end{document}
````

**Examples:**

```latex
\documentclass{article}
\documentclass[conference]{IEEEtran}
\documentclass[a4paper,12pt]{report}
```


## 📦 2. Common Packages

|Package|Purpose|
|---|---|
|`amsmath`, `amssymb`, `amsfonts`|Math symbols and fonts|
|`graphicx`|Insert images|
|`xcolor`|Color support|
|`geometry`|Page margins|
|`hyperref`|Clickable links and references|
|`caption`, `subcaption`|Better control over captions and sub-figures|
|`booktabs`|Professional-looking tables|
|`algorithmic`, `algorithm`|Write algorithms/pseudocode|
|`biblatex` or `natbib`|Bibliography management|
|`tcolorbox`|Colored boxes for notes or code|

---

## 🧾 3. Title, Author, and Date

```latex
\title{My First LaTeX Document}
\author{John Doe}
\date{\today} % or leave empty {}
\maketitle
```

In **IEEE papers**:

```latex
\title{Paper Title}
\author{\IEEEauthorblockN{Author Name}
\IEEEauthorblockA{\textit{Affiliation} \\ Email}}
\maketitle
```

---

## ✍️ 4. Text Formatting

|Command|Effect|
|---|---|
|`\textbf{bold}`|**bold**|
|`\textit{italic}`|_italic_|
|`\underline{text}`|underline|
|`\emph{text}`|emphasized text (contextual italic)|
|`\\`|new line|
|`\par`|new paragraph|
|`\textcolor{red}{text}`|colored text|
|`\LaTeX`|prints the LaTeX logo|

---

## 📚 5. Document Structure

```latex
\section{Main Section}
\subsection{Sub Section}
\subsubsection{Sub-subsection}
\paragraph{Paragraph Title} Text...
```

LaTeX automatically numbers sections.

To remove numbering:

```latex
\section*{Unnumbered Section}
```

---

## 📋 6. Lists

### Unordered List

```latex
\begin{itemize}
\item First item
\item Second item
\end{itemize}
```

### Ordered List

```latex
\begin{enumerate}
\item Step 1
\item Step 2
\end{enumerate}
```

### Description List

```latex
\begin{description}
\item[Definition:] Explanation here.
\end{description}
```

---

## 🧮 7. Math Mode

### Inline Math

```latex
Einstein said $E = mc^2$.
```

### Display Math

```latex
\[
a^2 + b^2 = c^2
\]
```

### Numbered Equation

```latex
\begin{equation}
a + b = \gamma
\label{eq:gamma}
\end{equation}
```

Reference it: `Equation \eqref{eq:gamma}`

### Align Equations

```latex
\begin{align}
x + y &= 10 \\
x - y &= 4
\end{align}
```

---

## 📊 8. Tables

### Simple Table

```latex
\begin{table}[h]
\centering
\caption{Example Table}
\begin{tabular}{|c|c|c|}
\hline
A & B & C \\
\hline
1 & 2 & 3 \\
\hline
\end{tabular}
\label{tab:example}
\end{table}
```

**Column alignment:**

- `l` → left
    
- `c` → center
    
- `r` → right
    
- `|` → vertical line
    

**Professional style (with booktabs):**

```latex
\begin{tabular}{lcr}
\toprule
Left & Center & Right \\
\midrule
A & B & C \\
\bottomrule
\end{tabular}
```

---

## 🖼️ 9. Figures (Images)

```latex
\begin{figure}[htbp]
\centering
\includegraphics[width=0.45\textwidth]{image.png}
\caption{Example Figure}
\label{fig:example}
\end{figure}
```

Reference it:

```latex
See Fig.~\ref{fig:example}
```

**Options:**

- `width=\textwidth` → scale to page width
    
- `height=5cm` → fixed height
    
- `[htbp]` → positioning hints (here, top, bottom, page)
    

---

## 📚 10. References / Citations

### Manual References

```latex
\begin{thebibliography}{00}
\bibitem{ref1} Author, "Title," Journal, Year.
\end{thebibliography}

Cited as \cite{ref1}.
```

### With BibTeX

```latex
\bibliographystyle{IEEEtran}
\bibliography{references}
```

Then include a `references.bib` file:

```bibtex
@article{einstein1905,
  author = {Einstein, A.},
  title = {On the Electrodynamics of Moving Bodies},
  year = {1905},
  journal = {Annalen der Physik}
}
```

---

## 🧮 11. Common Symbols

|Symbol|Code|Output|
|---|---|---|
|Greek alpha|`$\alpha$`|α|
|Subscript|`$x_1$`|x₁|
|Superscript|`$x^2$`|x²|
|Fraction|`$\frac{a}{b}$`|𝑎⁄𝑏|
|Summation|`$\sum_{i=1}^n i$`|∑|
|Integral|`$\int_0^1 x dx$`|∫|
|Infinity|`$\infty$`|∞|
|Degree|`$90^\circ$`|90°|
|Approx|`$\approx$`|≈|

---

## 📦 12. Figures & Tables Side-by-Side

```latex
\begin{figure}[htbp]
\centering
\begin{minipage}{0.45\textwidth}
\includegraphics[width=\linewidth]{fig1.png}
\caption{Left figure}
\end{minipage}
\hfill
\begin{minipage}{0.45\textwidth}
\includegraphics[width=\linewidth]{fig2.png}
\caption{Right figure}
\end{minipage}
\end{figure}
```

---

## ⚙️ 13. Page Setup & Layout

```latex
\usepackage[a4paper, margin=1in]{geometry}
```

**Change line spacing:**

```latex
\usepackage{setspace}
\onehalfspacing % or \doublespacing
```

---

## 💬 14. Quotes, Code, and Notes

```latex
\begin{quote}
This is an indented quote.
\end{quote}
```

Inline code (verbatim):

```latex
\verb|\LaTeX|
```

Block code:

```latex
\begin{verbatim}
Sample text or code here.
\end{verbatim}
```

---

## 🧠 15. Cross-Referencing

Define:

```latex
\label{sec:intro}
```

Refer:

```latex
See Section~\ref{sec:intro}
```

For Figures/Tables:

```latex
Fig.~\ref{fig:example}
Table~\ref{tab:example}
```

---

## 🔢 16. Lists in Math or Text

```latex
\begin{enumerate}
\item Step 1: $x + y = z$
\item Step 2: Substitute values
\end{enumerate}
```

---

## 🧰 17. Useful Text Commands

|Command|Description|
|---|---|
|`\textsuperscript{th}`|superscript text|
|`\footnote{Text}`|adds a footnote|
|`\url{https://example.com}`|clickable URL (needs `hyperref`)|
|`\newpage`|start a new page|
|`\tableofcontents`|generate Table of Contents|
|`\listoffigures`|list of figures|
|`\listoftables`|list of tables|

---

## 🧮 18. Advanced Math Environments

### Matrix

```latex
\[
\begin{bmatrix}
1 & 2 \\
3 & 4
\end{bmatrix}
\]
```

### Piecewise Function

```latex
\[
f(x) =
\begin{cases}
x^2, & x < 0 \\
x+1, & x \ge 0
\end{cases}
\]
```

---

## 🎨 19. Colors and Boxes

```latex
\usepackage{xcolor, tcolorbox}

\begin{tcolorbox}[colback=blue!5!white,colframe=blue!75!black,title=Note]
This is a highlighted note.
\end{tcolorbox}
```

---

## 🧩 20. IEEE-Specific Notes

- Use `\documentclass[conference]{IEEEtran}`
    
- Title and author via `\IEEEauthorblockN` and `\IEEEauthorblockA`
    
- Equations, figures, tables — same as standard LaTeX
    
- References via `\bibliographystyle{IEEEtran}`
    

---

## 🧰 21. Compile Commands (CLI)

If working offline:

```bash
pdflatex myfile.tex
bibtex myfile
pdflatex myfile.tex
pdflatex myfile.tex
```

If using **Overleaf** — everything compiles automatically.

---

## ✅ 22. Tips for Clean Documents

- Use `%` for comments — they are ignored by LaTeX.
    
- Always compile twice to resolve references.
    
- Use descriptive labels: `fig:`, `tab:`, `eq:`, `sec:`.
    
- Keep figures and tables near where they are cited.
    
- Don’t manually number sections or equations.
    

---

## 🧭 23. Example Minimal Template

```latex
\documentclass{article}
\usepackage{amsmath,graphicx}
\begin{document}

\title{My First LaTeX Paper}
\author{John Doe}
\date{\today}
\maketitle

\begin{abstract}
This is a simple example of a LaTeX document.
\end{abstract}

\section{Introduction}
LaTeX is great for scientific writing.

\begin{equation}
E = mc^2
\end{equation}

\begin{figure}[h]
\centering
\includegraphics[width=0.4\textwidth]{example.png}
\caption{Example Figure}
\end{figure}

\end{document}
```

---

## 🧠 Resources to Learn More

- 📘 [Overleaf LaTeX Documentation](https://www.overleaf.com/learn)
    
- 📗 [LaTeX Wikibook](https://en.wikibooks.org/wiki/LaTeX)
    
- 📙 [IEEE Author Center: Templates](https://www.ieee.org/conferences/publishing/templates.html)
    

---

**Happy TeXing! 🚀**

```

---

Would you like me to generate this as a **ready-to-download `.md` file** (formatted with syntax highlighting and headings for Obsidian/Notion)?
```
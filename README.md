# LaTeX tips and tricks

## Tabel of contents

* [Inserting an image](#Inserting-an-image)
* [Inserting a code listing](#Inserting-a-code-listing)
  * [From a file](#From-a-file)
  * [From text](#From-text)
* [Text formatting](#Text-formatting)
  * [Bold text](#Bold-text)
  * [Italics text](#Italics-text)
  * [Underlined text](#Underlined-text)
* [Citations](#Citations)
* [Making labels](#Making-labels)

## Inserting an image

[To the top](#Tabel-of-contents)

```latex
\begin{figure}
    \centering
    \includegraphics[width=1\textwidth]{path/to/figure.png}
    \caption{The caption that appears under the image}
    \label{fig:label_of_figure}
\end{figure}
```

## Inserting a code listing

[To the top](#Tabel-of-contents)

Please note that this step requires you to have a `preamble.tex` with the following lines in it.

```latex
\usepackage{listings}
\usepackage{caption}
\DeclareCaptionFont{white}{\color{white}}
\DeclareCaptionFormat{listing}{\colorbox{gray}{\parbox{\textwidth}{#1#2#3}}}
\captionsetup[lstlisting]{format=listing,labelfont=white,textfont=white}

\lstdefinestyle{framed}
{
    frame=lrb,
    belowcaptionskip=-1pt,
    xleftmargin=8pt,
    framexleftmargin=8pt,
    framexrightmargin=5pt,
    framextopmargin=5pt,
    framexbottommargin=5pt,
    framesep=0pt,
    rulesep=0pt,
    autogobble,
    columns=fullflexible,
    showspaces=false,
    showtabs=false,
    breaklines=true,
    stepnumber=1,
    numbers=left,
    showstringspaces=false,
    breakatwhitespace=true,
    escapeinside={(*@}{@*)},
    commentstyle=\color{greencomments},
    keywordstyle=\color{bluekeywords},
    stringstyle=\color{redstrings},
    numberstyle=\color{graynumbers},
    basicstyle=\ttfamily\footnotesize,
    frame=shadowbox,
    tabsize=4,
    captionpos=b
}
```

#### From a file

[To the top](#Tabel-of-contents)

```latex
\lstinputlisting[language=c, style=framed, label=code:label_for_code,caption=Caption of the file]{path/to/file.c}
```

#### From text

[To the top](#Tabel-of-contents)

Please note that when writing code like this, in LaTeX, you must escape every caracter that is used in LaTeX, eg. `{}#\&` and so on.

```latex
\begin{lstlisting}[language=c, style=framed, label=code:label_for_code,caption=Caption of the file]

\#include <stdio.h>

/* This is a comment */

int main(void) \{
    printf("Hello World!");
    return 0;
\}

\end{lstlisting}
```

## Text formatting

[To the top](#Tabel-of-contents)

The following formatting can all be mixed.

#### Bold text

```latex
\textbf{Your text here}
```

#### Italics text

```latex
\textit{Your text here}
```

#### Underlined text

```latex
\underline{Your text here}
```

## Citations

[To the top](#Tabel-of-contents)

In order to use citations you must have a library to keep track of these. I recommend using the following line, in your preamble

```latex
\usepackage[backend=bibtex, bibencoding=utf8]{biblatex}
```

In order to link this to your `.bib` file, include it in your preamble using

```latex
\addbibresource{path/to/file.bib}
```

Here is an example of what a citation might look like in your .bib file

```bibtex
@BOOK{Mittelbach2005,
  author = {Frank Mittelbach},
  edition = {2. ed.},
  publisher = {Addison-Wesley},
  title = {The LATEX companion},
  year = 2005
}
```

Now in order to reference this citation anywhere in the code, you can use the following command

```latex
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. \cite{Mittelbach2005}
```

In case you need to point out something that needs a citation, you can include the following, in your `preamble.tex` and call `\citationneeded` whereever you need a citation

```latex
\newcommand{\citationneeded}[1][]{\color{blue} [Citation needed]\color{black}}
```

## Making labels

[To the top](#Tabel-of-contents)

Labels can be used to reference something in your document at a later time. Labels are created by doing

```latex
\label{type:name_of_label}
```

Assume we have created a label called `fig:example`. To reference this label, we type the following, in the document, where we want to reference it

```latex
\ref{fig:exmaple}
```
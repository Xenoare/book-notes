## Latex Beginner Guide

by Stefan Kottwitz

### Chapter 1: Introduction to Latex
* Latex was create by American computer scientist Leslie Lamport

### Chapter 2: Formatting Words, Lines and Paraghraph
* pg 28: Latex commands usually have this syntax `\command[optional argument] {argument}`
* pg 31: Text-formatting commands usually look like `\text**{argument}`, where ** stands for a two letter abbreviatoin like **bf** for bold face or etc
> Summarizing font commands and declarations

| **Command**      | **Declaration** | **Meaning**        |
|------------------|-----------------|--------------------|
| \textrm{...}     | \rmfamily       | roman family       |
| \textsf{...}     | \sffamily       | sans-serif familly |
| \texttt{...}     | \ttfamily       | typewriter family  |
| \textbf{...}     | \bffamily       | **bold-face**      |
| \textmd{...}     | \mdfamily       | medium             |
| \textit{...}     | \itshape        | _italic shape_     |
| \textsl{...}     | \slshape        | slanted shape      |
| \textsc{...}     | \scshape        | Small Caps shape   |
| \textup{...}     | \upshape        | upright shape      |
| \textnormal{...} | \normalfont     | default font       |

* pg 31: Standard font in Latex so-called **serif** those small decorative font shall improve readability by reader's eyes, sometimes with **sans-serif**, such font that also a good choice for screen text because of the better readability on lower res.
* pg 38: We can use the command from `\tiny` to `\Huge` to change the font size. Normally, the font size declaration are used only in def. of macros in preemble.
* pg 44: `\newcommand` is our key to introduce logical formatting. We should avoid using latex **font commands inside the docs**, try to use these comand to create styles, code, snippets and many more

`\newcommand{command} [arguments] [optional] {definition}`
---
| Syntax     | Definition                                                                          |
|------------|-------------------------------------------------------------------------------------|
| command    | The name of the new command (must not be allowed to begin with \end)                |
| arguments  | An integer from 1 - 9, the number or arguments  of the new command                  |
| optional   | If this is present, the first argument would be optional with a default value given |
| definition | Every occurence of the _command_ will be replaced by _definition_                   |
---

* pg 45: Package `\url` designed for typesetting of web addresses. This command takes an address for the argument and will print out the typewriter font.
* pg 48: `\parbox` can be used to create a column for the text, it takes the argument text and formats the ouput to fit with the specified width. [We can also use \fbox to make things better]

`\parbox[alignment] [height] [inner alightment] {width} {text}`
---
| Syntax     | Definition                                                                          |
|------------|-------------------------------------------------------------------------------------|
| alignment    | optional argument same as inner alignment, default value is vertically-center |
| height    | if this optional argument isn't given, the box will just have natural height of the text inside (use to make the box bigger / smaller) |
| inner-alignment  | if the box is natural height, then u can adjust the text postion, which consist of: c-vertically center, t-top of the box, b-bottom, s-stretch the text          |
| width   | width of the box |
| text | text u want to put into the box                   |
---

* pg 50: Environments are like declaration with a built-in scope, with `\begin` to introduces a change in properties and close by `\end`
* pg 52: We can use the **microtype** `\usepacakge{microtype}` package to introduce font expansion to tweak the justification and improve the optical appearance
* pg 54: The command `\linebreak` can be used to end a line but to keep the full justification, and it counterpart `\nolinebreak` used to prevents a line break at the current pos. Both command takes 1 argument which is number to influence the line break slightly or strongly
* pg 60: Latex provides some commands to produce a variety of accents, we can use the **inputenc** package or just manually make the character
* pg 62: We can use environment for justification for every decleration, we could have writter `\begin{centering} ... \end{centering}` to make the text center. It also applied for `ragged-right` and `ragged-left`.

### Chapter 3: Designing Pages
* pg 73: The package **lipsum** produces famous LoremIpsum text which has been used for dummy text.
* pg 75: The package **geometry** used to take care of our layout regarding the paper size, margins, and more dimensions. 
[Ref](https://ctan.org/pkg/geometry)
> Here are some key features and options provided by the geometry package:
> 1. Page size: You can set the page size using options such as a4paper, letterpaper, or specify custom dimensions. 
> 2. Margins: The margin option allows you to adjust the margins of your document. You can set the margins individually for each side (top, bottom, left, right), or use the margin option to set all margins at once.
> 3. Orientation: You can specify the orientation of your document using options like landscape or portrait.
> 4. Centering: The centering option centers the text on the page horizontally and vertically.
> 5. Binding offset: If you're preparing a document for binding, you can use the bindingoffset option to specify an extra space on the left side for binding purposes.
> 6. Header and footer: The headheight, headsep, footskip, and related options allow you to customize the header and footer areas of the page.
> 7. Paper columns: The twocolumn option allows you to create a document with two columns.
* pg 80: The package **setspace** provide the option to adjust the line spacing of the document, this command has 3 options: _singlespacing_, _onehalfspacing_, _doublespacing_, or u can choose the spacing itself by using enviroment with `\begin{spacing}{factor-spacing} ... \end{spacing`.
* pg 83: The latex base classes are **article, book, report, slides** and **letter**, the base classes have the option itself:
> 1. Paper size which have options _a4paper, a5paper, b5paper, letterpaper, legalpaper or executivepaper_. The output itself will be formatterd according to the paper size.
> 2. Font size, the size of normal text in the document; the default is ten points (10pt). The size of headings, footnotes, indexes etc. will be adjusted accordingly..
> 3. Letter format, which consist of _potrait and background_
> 4. Column Format, which consist of _onecolumn or twocolumn_. The default page will be one-column (not supported by letter class)
> 5. Printing side, the formatting for printing on one side or both of the page. The option itself is _oneside or twosside_
> 6. _openright or openany_. The first decides that chapters have to begin on a righthand page (the default for the book class), openany allows chapters to start on any page (default for the report class)
> 7. titlepage or notitlepage: The first causes a separate title page when
\maketitle is used and is the default, except for the article class.
> 8. final or draft: If draft is set, then LaTeX will mark overfull lines with a black box, which is helpful in reviewing and improving the output

* pg 86: We can shorten the table of content entries by using optional argument of the sectioning commands. Eg. `\section[Page display]{Some filler text}`, the 'Page display' will be displayed to the table of content.
* pg 94: The command `\pagebreak` cause a page break. . Like its name suggests, it causes a page break. Furthermore, the text has been stretched to fill the page down to the bottom. Afterwards, because of the obviously unpleasant whitespace between the paragraphs and the headings, we replaced \pagebreak with \newpage. This command breaks the page as well, but it doesn't stretch the text: the remaining space of the page will stay empty.
* pg 98: The command `\footnote{text}` placed a superscripted number at the current position. Further, it prints its argument text into the bottom of the page, marked by the same number. As we've seen, such notes are separated from the main text by a horizontal line. Eg. 
```
\section{A lot more filler text}
More dummy text\footnote{serving as a placeholder} will follow.
```
> The complete definition of \footnote
> \footnote[number]{text} produces a footnote marked by this optional number, an integer. If we don't give the optional number, an internal counter would be stepped and used. This would be done automatically; we don't need to worry.

* pg 98: As a rule of thumb, if a command causes an error when it's used inside an argument, like in headings, try to fix it by putting \protect right before that command. Cases where \protect would hurt instead of helping are rare.
* pg 101: The footnote line can be modified by using \renewcommand such as `\renewcommand{\footnoterule}{\noindent\smash{\rule[3pt]{\textwidth}{0.4pt}}}`. The command \rule[raising]{width}{height} draws a line, here 0.4 pt thick, and as wide as the text, raised a bit by 3 pt. Through the command \smash, we let our line pretend to have a height and a depth of zero, so it's occupying no vertical space at all.

### Chapter 4: Creating Lists
> Latex provides several packages for designing the layout:
> * geometry
> * typearea
> * fancyhdr
> * scrpage2
> * setspace

* pg 106: We can use unordered list by using environment command `\begin{itemize} ... \end{itemize}`. For the ordered list we can simply put the command `\begin{enumerate} ... \end{enumerate}` before the \begin or \item command.
* pg 110: The **paralist** package can be used to reduce the space created by using enumerate of list by simply using `\compactenum` or `\compactitem`
* pg 116: The \description environment from **paralist** package can be used to create a definition list (there are also \compactlist, \inparadesc command)
```
\begin{description}
 \item[paralist] provides compact lists and list versions that
can be used within paragraphs, helps to customize labels and
layout
\end{description}
```

### Chapter 5: Creating Tables and Insereting Pictures
* pg 126: Creating tables in Latex involves using the **tabular** environment. Furthermore, the complete definition of _tabular_ is
```
\begin{tabular}{<column specifiers>}
    <table content>
\end{tabular\begin{tabular}[position]{column specifiers}
row 1 col 1 entry & row 1 col 2 entry ... & row 1 col n entry\\
 ...
\end{tabular}
```
and one way to example it
```
\begin{tabular}{|l|c|r|p{1.7cm}|}
 \hline
left & centered & right & a fully justified paragraph cell\\
\hline
 l & c & r & p\\
 \hline
\end{tabular}
```
* pg 127: The options by the _tabular_ environment are as follows

| Options | Definition                       |
|---------|----------------------------------|
| l       | left alignment                   |
| c       | centered alignment               |
| r       | right alignment                  |
| p       | a fully justified paragraph cell |
| r       | right alignment                  |
| @{code}       |  used to customize the inter-column spacing in a table. It allows you to insert any desired content between columns, such as whitespace, vertical lines, or even custom separators. |
| l       | vertical line                  |
| *{n}{options}       | equivalent to n copies of options, where n is a positive integer and options may consist of one or more column specifiers including * as well. |

* pg 127: Column entries are separated by &, while rows are terminated by \\. Don't end the last line by \\ unless you further wish to write a line below. It's also a good idea to align the ampersands in our source code to keep it readable.

* pg 127: The **array** package use some option such as
> * m{width} is similar to\parbox{width}: the base line is at the middle
> * b{width} is like \parbox[b]{width}: the base line is at the bottom
> * !{code} can be used like | but inserts code instead of a vertical line. In contrast to @{…}, the space between columns will not be suppressed.
> * `>{code}` can be used before an l, c, r, p, m, or b option and inserts code right at the beginning of each entry of that column
> * <{code} can be used after an l, c, r, p, m, or b option and inserts code at the end of the entry of that column

* pg 129: The **booktabs** package comes to enhance the quality of your tables by replacing \hline and \cline. The defintions of each commands are these
> * \toprule[thickness] may be used to draw a horizontal line at the top of the
table. If desired, a thickness may be specified, like 1pt or 0.5mm.
> * \midrule[thickness] draws a horizontal dividing line between rows of a table.
> * \bottomrule[thickness] draws a horizontal line to finish off a table
> * \cmidrule[thickness](trim){m–n} draws a horizontal line from column m to
column n. (trim) is optional like thickness, it could be (l) or (r) to trim the line at its left or right end. Write (lr) to trim at both ends. Even adding {width}, like in (l{10pt}), is possible and specifies the trim width.

* pg 132: The command `\multicolumn` used to merge two cells, and by its definition: `\multicolumn{number of columns}{formatting options}{entry text}`
```
\multicolumn{3}{|c|}{A multiple column}
```
Will create 3 combined column into 1 column with text 'A multiple column'

* pg 135: Using the environment table, we can simply put the captions of the table. `\begin{table} ... \end{table`

* pg 139: We can use the **xcolor** package to coloring columns, rows, entries and many more. `\usepackage[table]{xcolor}`

* pg 141: We can use the **graphicx** package to inserting a picture to the paper,the most important command is `\includegraphics{path}` where we specified the file and this file would be loaded if it exists.
* pg 142: Here are the most popular options of the **graphicx** package
> * width: The graphic would be resized to this width. Example: width=0.9\textwidth.
> * height: The graphic would be resized to this height. Example: height=3cm.
> * scale: The graphic would be scaled by this factor. Example: scale=0.5.
> * angle: The graphic would be turned by this angle. Example: angle=90.

### Chapter 6: Cross-Referencing
* pg 155: We created cross-references with just three commands: `\label{<labelname>}` to marks the position, `\ref{<labelname>}` to prints the number of the element we refer to and `\pageref{<labelname>}` to prints page number of that element.
* pg 155: To avoid any problem because of a possible unsuitable positioning, a good rule of thumb is to place the \label command right after the position we would like to mark. For instance, place it directly after the corresponding \chapter or after \section—not before, of course.
* pg 157: Using a command we can make such referencing easier such as:
` \newcommand{\fullref}[1]{\ref{#1} on page~\pageref{#1}} ` Where ~ is non-nonbreaking space which prevents line breaking between page and following referencing number.
* pg 160: The package **cleverev** automatically determines the type of cross-reference and the context in which it's used. The first thing we used is the command \crefname to tell cleveref which name it should use for enumerated items. The definition of \crefname is:
`\crefname{type}{singular}{plural}` where type is may be _chapter, section, figure, etc._ and The singular version will be used for single references and vice versa. `\crefname{enumi}{position}{positions}`

* pg 162: The package **hyperref** can be used as hyperlink to your document (_Note_: The loaded order must hyperref first before claveref to ensure the references to work)

### Chapter 7: Listing Content and References
* pg 168: There are the standard sectioning commands and their so called TOC level:

| Commmand       | Level                              |
|----------------|------------------------------------|
| \part          | -1 (Book and Report class)         |
| \chapter       | 0 (not available in Article class) |
| \section       | 1                                  |
| \subsection    | 2                                  |
| \subsubsection | 3                                  |
| \paragraph     | 4                                  |
| \subparagraph  | 5                                  |
> In book and report class, Latex creates TOC entries until level 2 (section) and level 3 in article, which means in book, \subsubsection doesn't generate a TOC entry

* pg 168: There's a variable representing the level, namely, \tocdepth. It's an integer variable which we call a counter. To tell LaTeX to include subsubsections in the TOC, we would have to raise this counter. There are two basic ways to adjust a counter value:
> * \setcounter{name}{n} specifies an integer value of n for the counter name
> * \addtocounter{name}{n} adds the integer value of n to value of the counter
name. n may be negative
> * and u can also using \addcounter to raise or lower the level

* pg 169: We can add entries manually for such case as \chapter* that doesn't produce a TOC entry by this command: `\addcontentsline{file extension}{sectional unit}{text}` Where file extension may be ***toc (table of content), lof (list of figures), lot (list of tables)***
* pg 169: Or you can just directly insert with commands: `\addtocontents{file extension}{entry}` where this is more flexible than the first one. There are some options with the command also
> 1. \protect: In LaTeX, some commands are considered "fragile" and may cause issues when used in certain contexts, such as within the table of contents.
> 2. \contentsline: This command is commonly used within the <content> argument to specify the structure and formatting of the added entry. It has some commands `\contentsline{<type>}{<entry>}{<page>}`
> > * <type>: Specifies the type of the entry, such as chapter, section, subsection, figure, table, or any custom entry type you define.
> > * <entry>: Specifies the text or title of the entry.
> > * <page>: Specifies the page number associated with the entry. This argument is optional and can be left empty ({}) if you don't want to include the page number.

* A example out of this commands are
> 1. `\addtocontents{toc}{\protect\contentsline{section {\hspace{1em}\textit{Appendices}}{}}` Where adds a custom entry titled "Appendices" to the Table of Contents. The entry is indented using \hspace and formatted in italics using \textit.
> 2. `\addtocontents{toc}{\protect\enlargethispage{\baselineskip}}` extends the text height such that one additional line fits to the contents page.

* pg 170: We can use the **makeidx** package to make a index. The command itself just take one argument `\index{text}` and this is will be written to a file with a extension _.idx_
* pg 174: `\index` allows customization with symbols and macros, when u are want to add a symbol: `\index{Symbol@\textit{Symbol}}` and combine the macro and symbol to create this: 
```
\newcommand{\mypage}[1]{Page #1}
...
\index{Symbol@\textit{Symbol}!\mypage{42}}
```
where the @\ symbol: This symbol is used to create a subentry within the index and the !\ symbol: This symbol is used to create a subsubentry within the index.
 
* pg 175: We can use index cross-referencing by using symbols |, like this `\index{Term1|see{Term2}}` the Term1 is the term you are indexing, and Term2 is the related term that you want Term1 to cross-reference. When the index is generated, the entry for Term1 will include a "see" cross-reference pointing to Term2. This informs the reader that they should look up Term2 for more information related to Term1.

* pg 178: We use **thebibliography** environment to typeset the list of references with these commands:
```
\begin{thebibliography}{widest label}
\bibitem[label]{key} author, title, year etc.
\bibitem…
…
\end{thebibliography}
```
* pg 180: Or we can use external program like **BibTex** to create a _.bib_ file extension to make the bibliography. [Ref.](https://www.bibtex.org/)
```
@article{DK89,
author = "D.E. Knuth",
title = "Typesetting Concrete Mathematics",
journal = "TUGboat",
volume = 10,
number = 1,
pages = "31--36",
month = apr,
year = 1989
}
```
* pg 185: We can changing the headings content by using macro `\renewcommand\`
 
| List              | Heading Commands                                 | Default Heading                                                  |
|-------------------|--------------------------------------------------|------------------------------------------------------------------|
| Table of contents | \contentsname                                    | Contents                                                         |
| List of figure    | \listfigurename                                  | List of figures                                                  |
| List of tables    | \listtablename                                   | List of tables                                                   |
| Bibliography      | \bibname in book and report; \refname in article | **Bibliography** in book and report; **References** in article** |
| Index             | \indexname                                       | Index                                                            |
### Chapter 8: Typing Math Formulas
* pg 193: The environment **equation** used to display equations and formulas in general
* pg 194: Extracting roots can be used by using the command `\sqrt[order]{value}` where the default value of order is 2
* pg 195: For the Greek letters and omicron can be found [Here](https://www.overleaf.com/learn/latex/List_of_Greek_letters_and_math_symbols)
* pg 196: Producing an ellipsis can be done by using some commands here
> * \ldots for left dots alignement
> * \rdots for rights dots alignment
> * \ddots for diagonal dots alignement
> * \vdots for vertical dots alignment
 
* pg 200: Here's a list of the amsmath multi-line environments:
 
| Name     | Meaning                                                                                                               |
|----------|-----------------------------------------------------------------------------------------------------------------------|
| multline | First line is left-aligned, last line is right-aligned, all others are centered.                                      |
| gather   | Each line is centered.                                                                                                |
| align    | Use & to mark a symbol where the formulas shall be aligned. Use another                                               |
| flalign  | Similar to align with more than one column, but the columns are flushed to the left and the right margin, repectively |
| alignat  | Alignment at several places, each has to be marked by &.                                                              |
| split    | Similar to align, but within another math environment, thus unnumbered                                                |

* pg 206: Writing units can be done in latex by using package **siuitx** that provide most modern and comprehensive unit. [Ref.](https://ctan.org/pkg/siunitx?lang=en)
 * pg 207: Example of using building math structure
 1. Creating arrays
 ```
 \[
 A = \left(
 \begin{array}{cc}
 a_{11} & a_{12} \\
 a_{21} & a_{22}
 \end{array}
 \right)
\]
 ```
2. Writing binomial coef.
`\binom{n}{k} = \frac{n!}{k!(n-k)!}`
 
* pg 208: Formulas may become complex: we might need to put one symbol above another one or above whole expressions, or we wish to put lines, braces, or dots above symbols. There are several ways.
1. \underlining and \overlining, which put a line above / below its argument, Ex. `\overline{AB}`
2. \underbrace and \overbrace, which will create a braces between its argument, Ex. `N = \underbrace{1 + 1 + \cdots + 1}_n`
 
* pg 208: Math accents (bar, hat, acute, etc) also can be done using some commands [here](https://abstractmath.org/MM/MMOtherSymbols.htm) 
* pg 209: LaTeX provides environment for theorems, definitions, and alike. Returning to our first example in this chapter, we could define a theorem environment by:
`\newtheorem{thm}{Theorem}`
Then, we declare a definition environment, using an optional argument stating an existing environment with which we would like to share the numbering:
`\newtheorem{dfn}[thm]{Definition}`
 
### Chapter 9: Using Fonts
* pg 216: TeX Live includes only freely licensed fonts. Non-free fonts may be installed using a separate program. It's called getnonfreefonts. If it's not already installed with your version of TeX Live, you can download it from [Here.](http://www.tug.org/fonts/getnonfreefonts/)
* pg 219: The package **mathptmx** defines a Times Roman text font. Additionally, it provides math support using suitable symbols of the standard Computer Modern symbol font together with Times Roman letters and more glyphs of further fonts. It supersedes the times package.
 * pg 224: Probably the best place to browse LaTeX fonts is The LaTeX Font Catalogue. Visit [http://www.tug.dk/FontCatalogue/](http://www.tug.dk/FontCatalogue)
 
### Chapter 10: Developing Large Document  
* pg 228: Thus, while we are writing, we will be able to manage a huge project consisting of many chapters in separate files.
1. First thing first we can create a preamble.tex as our preamble template
 ```
\usepackage[english]{babel}
\usepackage[utf8]{inputenc}
\usepackage[T1]{fontenc}
\usepackage{lmodern}
\usepackage{microtype}
\usepackage{natbib}
\usepackage{tocbibind}
\usepackage{amsmath}
\usepackage{amsthm}
\newtheorem{thm}{Theorem}[chapter]
\newtheorem{lem}[thm]{Lemma}
\theoremstyle{definition}
\newtheorem{dfn}[thm]{Definition}
 ```
2. And for sake of this book, we make another document that contains the chapter _Equations_ as chapter1.tex
 ```
\chapter{Equations}
\section{Quadratic equations}
\begin{dfn}
A quadratic equation is an equation of the form
\begin{equation}
\label{quad}
ax^2 + bx + c = 0
\end{equation}
where \( a, b \) and \( c \) are constants and \( a \neq 0 \).
\end{dfn}
 ```
3. Lastly, now we shall construct the top-level document. Create another file called equations.tex. This one starts with the documentclass and lists the
preamble and the chapters for inclusion:
```
\documentclass{book}
\input{preamble}
\begin{document}
\tableofcontents
\include{chapter1}
\include{chapter2}
\end{document}
```
> * \input reads in another file, just as if it had been typed in.
> * \include also reads in an external file, but automatically inserts \clearpage
before and after. The \include implicitly starts new pages, This makes it useful for page ranges such as chapters or sections. One consequence is that you may use \include only after \begin{document}. \include cannot be nested. You could still use \input within included documents, though it might not be a good idea to complicate the structure further. Most importantly, \include supports a mechanism of choosing which parts of the document you wish to compile—so we come to another command, namely, \includeonly.
 
 * pg 232: In contrast to reports, books often begin with introductory material such as copyright information, a foreword, acknowledgements, or a dedication. This part, including the title page and the table of contents, is called the **front matter**. At the end, a book might include an afterword and supporting material like a bibliography, and an index. This part is called the **back matter**.
> The three commands \frontmatter, \mainmatter, and \backmatter are responsible.
They modified both the page and chapter numbering in the following way:
> * \frontmatter Pages are numbered with lowercase Roman numbers. Chapters generate a table of contents entry but don't get a number.
> * \mainmatter Pages are numbered with Arabic numbers. Chapters are numbered and produce a table of contents entry.
> * \backmatter Pages are numbered with Arabic numbers. Chapters generate a table of contents entry but don't get a number. 
 
 * pg 235: The titlepage environment typesets its contents on a separate page. Though this title page will be numbered like any other page, the page number won't be printed on that page. Within this environment, we used some basic LaTeX font commands to modify the font size and shape. By grouping with curly braces, we limited those commands. Line breaks like \\[.2in] just cause some more space before the following line. \vfill inserts an elastic vertical space which stretches as much as possible such that the page is filled. This way we put the last line off to the end of the page.
```
\begin{titlepage}
\raggedleft
{\Large The Author\\[1in]}
{\large The Big Book of\\}
{\Huge\scshape Equations\\[.2in]}
{\large Packed with hundreds of examples and solutions\\}
\vfill
{\itshape 2011, Publishing company}
\end{titlepage}
```
Save this as _title.tex_, and use `\input` and use `\maketitle` to display the title
 
* pg 237: You will find a collection of templates, arranged by document type such as thesis, reports, letters, and presentations, accompanied by sample output, in a template gallery at http://texblog.net/latex/templates.
 
### Chapter 11: Enhancing Your Documents Further
* pg 251: There's a huge amount of LaTeX packages. For nearly every possible task, somebody has written a package either solving or supporting it. Nearly all packages are stored on CTAN. But how can we find what we need? Let's have a look at an online catalogue. (http://texcatalogue.sarovar.org/), The TeX Catalogue is a really valuable source. Its category view is especially useful if you are looking for a package but don't know its exact name. It's also an easy way to locate and download documentation if texdoc doesn't work for you.
 
### Chapter 12: Troubleshooting
```
\documentclass{article}
\begin{document}
\Latex\ says: Hello world!
\end{document}
```
* pg 266: LaTeX commands are case-sensitive. Because we did not respect that, LaTeX had to deal with a macro called \Latex, which is just unknown. As a command is also called a control sequence, we got the error Undefined control sequence.
* pg 267: Command names might easily be misspelled or just misused. Let's check out LaTeX's common complaints.
> * Undefined control sequence: As in our example, TeX stumbled across an unknown command name. There are two possible reasons:
> * The command name might be misspelled. In that case, you just need to correct it and restart the typesetting.
> * The command name is correct, but it's defined by a package you didn't load. Add a \usepackage command to your preamble, which loads that package.
> * Environment undefined: That's similar to Undefined control sequence, but this time you began an environment which is unknown. Again, this may be caused by misspelling or by a missing package—you know how to correct it.
> * Command already defined: This happens when you create a command with a name that's already used, for example, with \newcommand or \newenvironment. Just choose a different name. If you really would like to override that command, use \renewcommand or \renewenvironment instead.
> *  Missing control sequence inserted: A control sequence has been expected but didn't appear. A common cause is using \newcommand, \renewcommand, or \providecommand, but not specifying a command name as its first argument.
> * \verb illegal in command argument: The \verb command for producing verbatim text is a delicate one; it cannot be used within arguments of commands or environments. The examplep package offers commands for using verbatim text in such places.
 
* pg 274: Many warnings deal with referencing. Common mistakes are missing label or cite keys or keys that have been used twice. Sometimes LaTeX just tells you that another typeset run is required.
> *  Label multiply defined: \label or \bibitem has been used with a label name that's already been used. Make label names unique.
> * There were multiply-defined labels: Like the previous warning, but after processing the complete document; a label has been defined by two \label commands.
> * Labels may have changed. Rerun to get cross-references right: Just typeset again to let LaTeX correct the referencing.
> * Reference ... on page ... undefined: \ref or \pageref has been used without a corresponding \label definition. Insert a \label command at a suitable place.
> *  Citation ... on page ... undefined: A \cite command did not have a corresponding \bibitem command.
> * There were undefined references or citations: Summarizing after processing any \ref or \cite command did not have a corresponding \label or \bibitem command.
 
Note: Whenever you get warnings regarding referencing, it’s a good idea to simply
rerun typesetting. Often, such warnings then disappear, because LaTeX couldn’t
resolve all references in the first run itself.
 
* pg 275: Many problems just occur because of the use of obsolete packages. For example, some that aren't maintained any more may conflict with newer packages. Often, you just need to find the recommended successor of an obsolete package and use that.
 
### Chapter 13: Using Online Resources
* pg 287: Here the few list Frequently Asked Questions (FAQ) of Latex community:
> AMS-Math FAQ http://www.ams.org/tex/amsmath-faq.html
> As you know, amsmath is the most recommended math package. There's a list of questions and answers to amsmath and AMS classes and packages on the website of the American Mathematical Society.
> tex-live http://tug.org/mailman/listinfo/tex-live
> The name says it all: it deals with the TeX Live collection. If you installed this software distribution, you might be interested in subscribing to get the latest news and to read and write about issues with it.
 
* pg 290: LaTeX distributions. Today there are two big LaTeX distributions, both very modern and comprehensive, plus some descendants:
> * TeX Live: http://tug.org/texlive/ is a cross-platform LaTeX software collection. It runs on Windows, Mac OS X, Linux, and Unix.
> * MiKTeX: http://www.miktex.org/ is a very user-friendly and popular LaTeX
distribution specifically for the Windows operating system.
> * proTeXt: http://www.tug.org/protext/ is a MiKTeX-based distribution for
Windows that especially focuses on easy installation.
> * MacTeX: http://www.tug.org/mactex/ is derived from TeX Live and has been
customized specifically for Mac OS X.

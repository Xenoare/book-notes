## Latex Beginner Guide

by Stefan Kottwitz

### Chapter 1: Introduction to Latex
* Latex was create by American computer scientist Leslie Lamport

### Chapter 2 Formatting Words, Lines and Paraghraph
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
* pg 122

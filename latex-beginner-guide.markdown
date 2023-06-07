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

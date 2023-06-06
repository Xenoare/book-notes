## The Latex Companion 2nd

by Frank Mittelbach and Michel Goossens

### Chapter 1: Introduction to Latex
* pg 2: Latex was the first widely used language for describing the logical structure of a large range of documents and hence introducing the philosophy of logical design as used in Scribe.

### Chapter 2: The Structure of a Latex Document
* pg 15: You may starting your latex file with a ```\documentclass``` commmand where this defines the avaialable logical commands and environments (for ex. ```\chapter``` in the report class).
* pg 16: Commands placed between ```\documentclass``` and ```\begin{document}``` are the so-called *document preamble*. All style parameters must be defined in this premble, either pacakge or class file before the ```\begin{document}``` command, which sets the values for some of the global parameters (like css styling) 
``` 
\documentclass[twocolumn, a4paper]{article}
\usepackage{multicol}
\usepackage[german,french]{babel}
\addtolength\textheight{3/baselineskip}
\begin{document}
```
> This document premeble defines that the class of the document is  article and > that the layout is influences by the formatting request two columng (typeset in two columns) and the option on A4 paper. The first  ```\usepackage``` declaration informs latex that this document contains commands and structures provided by the package multicol. In addition, the babel papckage with the options german and french (suppoerted by those 2 language). Finnaly the default height of the text body.

* Generally, nonstandard latex package files contain modifications, extensionsm or improvements with resprect to standard latex

* pg 22: Standard latex documents classes (i.e., artcile, report and book) contains commands and environments to define the different hierarchial structural units of a document (chapers, sections, appendices). For more information u can find more [here](https://en.wikibooks.org/wiki/LaTeX/Document_Structure#Sectioning_Commands)
* pg 23: Standard latex provides set of sectioning commands (like a dom tree) from level 0 (\chapter and \part) to level 5 (\subparagraph)
* pg 24: Numbering headings in latex uses a counter for each sectional unit and composes the heading number from the counter (we do have controlled counter named secnumdepth) which holds the highest level of numbered headings
```
\documentclasses{book}
\setcounter{secnumdepth}{-1} % for numbering all sections
\begin{document}
\part{Part 1}
This part is numbered
\chapter{Chapter 1}
This chapter is numbered
\section{Section 1.1}
This section is numbered
\end{document}
```
* 

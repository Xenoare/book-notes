## Setup Ultisnips

### First steps after installing Ultisnips, we have to configure
1. The key to trigger (expand) snippets, which set by global variable `g:UltiSnipsExpandTrigger`
2. The key to move forward through snippet's tabstop, which set by `g:UltiSnipsJumpForwardTrigger`
3. The key to move backwards through snippet's tabstops, which set by `g:UltiSnipsJumpBackwardTrigger`
```js
" Set this code in your .vimrc
let g:UltiSnipsExpandTrigger       = '<Tab>'    " use Tab to expand snippets
let g:UltiSnipsJumpForwardTrigger  = '<Tab>'    " use Tab to move forward through tabstops
let g:UltiSnipsJumpBackwardTrigger = '<S-Tab>'  " use Shift-Tab to move backward through tabstops
```

### The default folder for snippets
By default, UltiSnips store `.snippets` files inside directories named `UltiSnips`. The snippet directory name is controlled with the global variable `g:UltiSnipsSnippetDirectories`
```js
" To use both UltiSnps and MySnippets as directories
let g:UltiSnipsSnippetDirectories=["UltiSnips", "MySnippets"]
```
Then UltiSnips would load `*.snippet` files in those folder under Vim `runtimepath`.

### Snippet folders
To even organize `filetype`-specific snippets into multiple files of their own. We can target the `filetype` inside the snippets directory. UltiSnips will load all `.snippet` files inside this folder, regardless of their basename.
```
${HOME}/.vim/UltiSnips/          # Vim
${HOME}/.config/nvim/UltiSnips/  # Neovim
├── all.snippets
├── markdown.snippets
├── python.snippets
└── tex
    ├── delimiters.snippets
    ├── environments.snippets
    ├── fonts.snippets
    └── math.snippets
```

### Anatomy of UltiSnips snippet
The general form of an UltiSnips snippet is:
```yaml
snippet {trigger} ["description" ["options"]]
{snippet body}
endsnippet
```
#### Options
There are some options inside the snippet syntax, where there are some options to know:
- `A` enables automatic expansion, which will expand immedietly after `trigger` is typed. Without this, you have to press the `g:UltiSnipsExpandTrigger` key
- `r` allows the use of regular expressions in the snippet's trigger.
- `b` expands snippets only if `trigger` is typed at the beginning of a line. This is useful when writing snippets for LaTeX environment, since they usually defined at the beginnning of a line.
- `i` (for "in-word" expansion) expands snippets regardless of where `trigger` is typed.

### Tabstops
Tabstops are predifined pos within a snnipppet body to which you move by pressing `g:UltiSnipsJumpForwardTrigger` key. Here are some LaTeX snippets
```yaml
# Snippet for typewriting font
snippet tt "The \texttt{} command for typewriter-style font"
\texttt{$1}$0
endsnippet

# Snippet for fractions
snippet ff "The LaTeX \frac{}{} command"
\frac{$1}{$2}$0
endsnippet
```
![snippet example](https://www.ejmastnak.com/images/vim-latex/snippets/texttt-frac.gif)
#### Tabstop Placeholder
Use placeholders to enrich a tabstop with a description of default text. The syntax for defining placeholder text is `${1:placeholder}`.
```
snippet hr "The hyperref package's \href{}{} command (for url links)"
\href{${1:url}}{${2:display name}}$0
endsnippet
```yaml
#### Mirrored Tabstops
Just repeat the tabstop you wish to mirror. This is useful when we working with HTML tags. note how `$1` tabstop containing the environment name is mirrored in both the `\begin` and `\end` commands.
```yaml
# Snippet for creating new generic LaTeX environments
snippet env "New LaTeX environment" b
\begin{$1}
    $2
\end{$1}
$0
endsnippet
```
#### Visual Placeholder
The visual placholder lets you use text selected in Vim's visual mode inside the content of a snippet body.
```yaml
# Snippet for italic font
snippet tii "The \textit{} command for italic font"
\textit{${1:${VISUAL:}}}$0
endsnippet
```
!(visual placeholder)[https://www.ejmastnak.com/images/vim-latex/snippets/visual-placeholder.gif]

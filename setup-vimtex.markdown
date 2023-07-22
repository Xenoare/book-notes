## Setup Ultisnips

This setup in for my Windows (idk about Linux, maybe later lul)

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
```yaml
snippet hr "The hyperref package's \href{}{} command (for url links)"
\href{${1:url}}{${2:display name}}$0
endsnippet
```

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
![visual placeholder](https://www.ejmastnak.com/images/vim-latex/snippets/visual-placeholder.gif)

### Regex snippet triggers
> For a place to start on Regex, I suggest [Coray Schafer's tutorial](https://www.youtube.com/watch?v=sa-TUpSx1JA)
Here are some example use cases:
```yaml
# This snippet expand mm into $ $ (an inline math)
snippet "(^|[^a-zA-Z])mm" "Inline LaTex math" rA
`!p snip.rv = match.group(1)` \$ ${1:${VISUAL:}} \$ $0
endsnippet
```
```yaml
# This snippet easily insert Euler's number e
snippet "(^|[^a-zA-Z])ee" "e^{} superscript" rA
`!p snip.rv = match.group(1)`e^{$1:{$VISUAL:}}$0
endsnippet
```
Note that, this line `!p snip.rv = match.group(1)` can be break down into:
1. `!p` tells UltiSnips to execute in thode as Python
2. `snip.rv`. `snip` is a special object provided by UltiSnips within the embedded Python code. `snip.rv` is a property of the `snip` object that stands for "return value". It allows you to assign a value that will be used as the result of the snippet expansion. In this case, `snip.rv` is being assigned the value of `match.group(1)`.
3. `match.group(1)` is another special object provided by UltiSnips to represent the match object of the snippet trigger.

### Tip: Refreshing snippets
The function `UltiSnips#RefreshSnippets` refreshes the snippets in the current Vim instance to reflect the contents of your snippet directory. Here's a use case example:
1. Problem: you’re editing `myfile.tex` in one Vim instance, make some changes to `tex.snippets` in a separate Vim instance, and want the updates to be immediately available in `myfile.tex` without having to restart Vim.
2. Solution: call `UltiSnips#RefreshSnippets` using `:call UltiSnips#RefreshSnippets()`.
Or you can just simply put a key mapping in the `vimrc` to call this
```yaml
# Use <leader>u in normal mode to refresh UltiSnips snippets
nnoremap <leader>u <Cmd>call UltiSnips#RefreshSnippets()<CR>
```

### Tip: A snippet for writing snippets:
To use it, create the file `snippets.snippets` within `UltiSnips` directory and paste this:
```yaml
# Make it easier to create new snippets
snippet snip "A snippet for writing Ultisnips snippets" b
`!p snip.rv = "snippet"` ${1:trigger} "${2:Description}" ${3:options}
$4
`!p snip.rv = "endsnippet"`
$0
endsnippet
```
> The use of `!p snip.rv = "snippet" is to insert the literal string "snippet" in place.

### Getting started with VimTeX: doing practical stuff
1. Change and delete stuff. You can delete **surrounding environments** using `dse` command.
```yaml
\begin{quote}                 dse
Using VimTeX is lots of fun!  -->  Using VimTeX is lots of fun!
\end{quote}
```
![dse-command](https://www.ejmastnak.com/tutorials/vim-latex/vimtex/dse.gif)

2. Change surrounding environment using `cse`. Change the type of a LaTeX environent without changing the environment contents.
```yaml
\begin{equation*}   cse align   \begin{align*}
    % contents         -->          % contents 
\end{equation*}                 \end{align*}
```
![cse-command](https://www.ejmastnak.com/tutorials/vim-latex/vimtex/cse.gif)

3. Delete surrounding commands using `dsc`. Delete a LaTeX command while preserving the command's argument(s) (it is also delete parameters inside the square brackets)
```yaml
                      dsc
\textit{Hello, dsc!}  -->  Hello, dsc!
```
![dsc-image](https://www.ejmastnak.com/tutorials/vim-latex/vimtex/dsc.gif)

4. Delete surrounding delimeters by using `dsd`. Delete delimeters such as `()` ,`[]`, `{}` and their `\left \right` variants without changing its content.
```yaml
         dsd
(x + y)  -->  x + y

                    dsd
\left(X + Y\right)  -->  X + Y
```
![dsd](https://www.ejmastnak.com/tutorials/vim-latex/vimtex/dsd.gif)

5. Changing surrounding delimetrs using `csd`
```yaml
         csd [
(a + b)   -->   [b + b]
```

6. Delete surrounding math using `ds$`. Delete the environment or the `$` delimeters of the LaTeX inline math without changing the math contents.
```yaml
$ 1 + 1 = 2 $   -->  1 + 1 = 2
```

7. Changing surrounding math using `cs$`.
![cs$](https://www.ejmastnak.com/tutorials/vim-latex/vimtex/csm.gif)
```yaml
               cs$ equation
$ 1 + 1 = 2 $       -->       \begin{equation}
                                  1 + 1 = 2 
                              \end{equation}
                  cs$ $
\begin{equation}   -->  $x + y = z$
    x + y = z
\end{equation}                               
```

8. Change surrounding commands using `csc`. For example if you want to chang italic text into boldface
```yaml
                          csc textit
\textbf{Make me italic!}     -->      \textit{Make me italic!}
```
![csc](https://www.ejmastnak.com/tutorials/vim-latex/vimtex/csc.gif)

### Toggle-style mappings. You can toggle back and forth between states of various LaTeX environment and commands.
1. Toggle starred commands with `tsc` and `tse`
![tsc](https://www.ejmastnak.com/tutorials/vim-latex/vimtex/tsc-tse.gif)

2. Toggle between inline, display math and `equation` environment with `ts$`.
```yaml
              ts$  \[              ts$   \begin{equation}
$1 + 1 = 2$   -->     1 + 1 = 2    -->       x + y = z
                   \]                    \end{equation}
```
![ts$](https://www.ejmastnak.com/tutorials/vim-latex/vimtex/tsm.gif)

3. Toggle surrounding delimeters with `tsd`
![tsd](https://www.ejmastnak.com/tutorials/vim-latex/vimtex/tsd.gif)

4. Toggle surrounding fractions with `tsf`.
![img](https://www.ejmastnak.com/tutorials/vim-latex/vimtex/tsf.gif)

### Motions mappings.
1. Naviagate matching content using `%`. Move between matching delimeters, and latex environment using `%`.
![img](https://www.ejmastnak.com/tutorials/vim-latex/vimtex/move-matching.gif)

2. Navigate sections using `]]`. Jump to the beginning of `\section`, `\subsection` by using shortcut `]]` and vice versa with `[[`.
![img](https://www.ejmastnak.com/tutorials/vim-latex/vimtex/move-section.gif)

### Vimtex customization. 
You can actually make a shortcut and key binding to any `<Plug>` map, for example you can map any trigger action in this `vimtex-mapping` section (check `:h vimtex-mappping`.
```yaml
" Manually redefine only the mappings you wish to use
" --------------------------------------------- "
" Some text objects
omap ac <Plug>(vimtex-ac)
omap id <Plug>(vimtex-id)
omap ae <Plug>(vimtex-ae)
xmap ac <Plug>(vimtex-ac)
xmap id <Plug>(vimtex-id)
xmap ae <Plug>(vimtex-ae)

" Some motions
map %  <Plug>(vimtex-%)
map ]] <Plug>(vimtex-]])
map [[ <Plug>(vimtex-[[)

" A few commands
nmap <localleader>li <Plug>(vimtex-info)
nmap <localleader>ll <Plug>(vimtex-compile)
```

### Text objects.
Here's the table of VimTeX text objects
| Mapping    | Text objects                                   |
|------------|------------------------------------------------|
| `ac`, `ic` | LaTeX commands                                 |
| `ad`, `id` | Paired delimeters                              |
| `ae`, `ie` | LaTeX environment                              |
| `a$`, `i$` | Inline math                                    |
| `aP`, `iP` | Sections                                       |
| `am`, `im` | Items in `itemize` and `enumerate` environment |
> The ad and id delimiter text object covers all of (), [], {}, etc. and their \left \right, \big \big, etc. variants, which is very nice. Here is a visual mode example of the delimiter and environment text objects:

![img-text-objects](https://www.ejmastnak.com/tutorials/vim-latex/vimtex/text-objects.gif)

### Vimtex compilling and QuickFix menu
After compiling with :VimtexCompile or :VimtexCompileSS, VimTeX will automatically open the QuickFix menu if warnings or errors occurred during compilation (the QuickFix menu stays closed if compilation completes successfully). For most compilation errors, the QuickFix menu will display the error’s line number and a (hopefully) useful error message. In such cases you can use the Vim commands :cc and :cn to jump directly to the offending line (much more info at :help quickfix in the Vim docs).
![quickfix menu](https://www.ejmastnak.com/tutorials/vim-latex/compilation/quickfix-error-short.gif)

### Cross-platform concepts
1. Forward Search, the process of jumping from the current position in LaTeX source file to the corresponding pos in PDF reader displaying in the compiler doc. To to this, simpy move the cursor into the part you want to show (like `section`, `figure`, etc) and use the command `:VimtexView` or key `<leader>lv` to show in the pdf reader.
![img](https://www.ejmastnak.com/tutorials/vim-latex/pdf-reader/forward-search.gif)
Here's the configuration in `vimrc`
```yaml
Configuration: >vim
  let g:vimtex_view_general_viewer = 'SumatraPDF'
  let g:vimtex_view_general_options
      \ = '-reuse-instance -forward-search @tex @line @pdf'
```

2. Inverse search, the process of switching focus from a line in the PDF docs, into corresponding LaTeX source code.
![inverse-search](https://www.ejmastnak.com/tutorials/vim-latex/pdf-reader/inverse-search.gif)
```yaml
To configure with `VimtexInverseSearch`, use: >bash

  vim -v --not-a-term -T dumb -c "VimtexInverseSearch %l '%f'"

  nvim --headless -c "VimtexInverseSearch %l '%f'"

On Windows, the above commands may lead to an annoying command window "popup".
This may be avoided, or at least reduced, with the following variants: >bash

  cmd /c start /min "" vim -v --not-a-term -T dumb -c "VimtexInverseSearch %l '%f'"

  cmd /c start /min "" nvim --headless -c "VimtexInverseSearch %l '%f'"
```

### Key Mappings
> Another more sufficient material is here:
> - https://www.ejmastnak.com/tutorials/vim-latex/vimscript/#leader
> - https://learnvimscriptthehardway.stevelosh.com/

Vim key mappings allow you to map arbitrary logic to keyboard keys, and I would count key mappings among the fundamental Vim configuration tools. In the context of this series, key mappings are mostly used to define shortcuts for calling commands and functions that would be tedious to type out in full (similar to aliases in, say, the Bash shell). The official documentation of key mappings lives in the Key mapping chapter of the Vim documentation file map.txt, and you can access it with :help key-mapping. I will summarize here what I deem necessary for understanding the key mappings used in this series.

### Basic syntax for key mappings
```yaml
:map {lhs} {rhs}
```
Here is what’s involved in the mapping definition:
- `{lhs}` (left hand side): A (generally short and memorable) key combination you wish to map.
- `{rhs}` (right hand side): A (generally longer, tedious-to-manually-type) key combination you want the short, memorable {lhs} to trigger.
- The Vim mode you want the mapping to apply in, which you can control by replacing `:map` with `:nmap` (normal mode), `:vmap` (visual mode), `:imap` (insert mode), or a host of other related commands, listed in `:help :map-commands`.
```yaml
" Map `Y` to `y$` (copy from current cursor position to the end of the line),
" which makes Y work analogously to `D` and `C`.
" (Not vi compatible, and enabled by default on Neovim)
noremap Y y$

" Map `j` to `gj` and `k` to `gk`, which makes it easier to navigate wrapped lines.
noremap j gj
noremap k gk
```

Vim offers two types of mappings commands:
1. The *recursive* commands `map`, `nmap`, `imap` and any `*map` relatives.
2. The *non-recursive* commands `noremap`, `nnoremap` and their `*noremap`.
Both the `map {lhs} {rhs}` and `:noremap {lhs} {rhs}` will map `{lhs}` to `{rhs}`, but here's the main diff.
- `map`: If any keys in the `{rhs}` of a :map mapping have been used the `{lhs}` of a different mapping (e.g. somewhere else in your Vim config or in third-party plugin), then the second mapping will in turn be triggered as a result of the first (often with unexpected results!).
- `noremap`: Using `:noremap {lhs} {rhs}` is safer—it ensures a mapping’s `{rhs}` is interpreted literally and won’t unexpectedly trigger other mappings.

### Notion for special keys
Certain keys can be used in key mappings only if you refer them with a special keyword like `Space` -> `<Space>` or `Enter` -> `CR`. See `:help keycodes` for a full list of special keys, and `:h <>` for the rules between Vim's `<>` notation.
```yaml
" map `<Space>q` to the `:quit` command using the <Enter> and <CR> keywords
nnoremap <Space>q :quit<CR>
```

### See what shortcut that already used by Vim
You can use the Vim command `:help {key}<C-D>` (where `<C-D>` is Vim notation for `<Ctrl>d`:) to see if `{key}` is used for some built-in or plugin-defined Vim command. For example `:help s<C-D>` shows a multi-column list of all commands beginning with s (there are a lot!). You can then type out the full version of any command you see in this list and press enter to go its help page. This useful tip is tucked away at the bottom of `:help map-which-keys.`








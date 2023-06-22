## Learn Vim (the Smart Way)

by iggredible [Ref.](https://github.com/iggredible/Learn-Vim)

### Chapter 1: Starting Vim
* The vim command usually started with `:` and there are so many options you do co with it:
* Opening a file: you can open a file by typing in terminal `vim <file>`, and also vim support opening multiple windows and multiple files by simply typing `vim -o2 file1.txt file2.txt`, this is will create a 2 horizontal window and fill the first one with file1.txt and file2.txt. The argument `-o<window>` is possible to open multiple page.
* You can start coding in vim by typing `i` to switch to insert mode.
* Saving and exiting file: You can save ur file by command `:write` or `:w` and `:write <file>` if the file isn't created. For the exiting a file, you simply just type `:quit` or `:q` to quit.
* There are so many command in vim. So to help the user, vim provides help pages by this command `:help {some-command}` or `:h`.
* How can i search for relevant command in vim? Just typing some command like ` :h quit` and using `tab`, vim will display relevant keywords to work with.
* Suspending a file can be done by just using `:suspend` or `CTRL-Z` to suspend, and if u want to back to the original file. just simply type `fg` or `exit` (if it on windows) to back to the suspended file. 

### Chapter 2: Buffer, Window and Tabs
* A buffer is a temporary in-memory space where you can write / edit some text. Normally when we open a file, the data is bound to a buffer (every time we open a new vim file, we create a new buffer for that file). 
* There are several ways to traverse a buffer such as `bnext` to go to next buffer and vice versa with `bpravious`. Or with shortcut with `CTRL+O` to older position and `CTRL+I` to newew position.
* Window is a viewport on a buffer, when you can read / edit content of a file.
* You can split the window by these following command-line
> 1. vsplit filename to split window vertically
> 2. split filename to split window horizontally
> 3. new filename to create a new window
* You also can navigate through windows by these command
> 1. CTRL-W H to move the cursor to the left window
> 2. CTRL-W J to move the cursor to the window below
> 3. CTRL-W K to move the cursor to the window above
> 4. CTRL-W L to move the cursor to the right window
* Tabs is a collection of windows. Whhen you close a tab in Vim, you are only closing the tab layout, the file itself still open in their buffer. There are useful tab navigations
> 1. :tabnew file to open a file in a new tab
> 2. :tabclose to close a tab
> 3. :tabnext to go to next tab
> 4. :tabprevious to go to previous tab
> 5. :tablast to go to last tab
> 6. :tabfirst to go to first tab
* Moving between windows just like move in 2-dimensional space where the command `CTRL-W H/J/K/L` use to navigate like in X-Y axis Cartesian coordinates.
* and moving between buffers just like traveling accross Z axis where we traverse between depth of a buffer (buffer stacking to the top and we traverse it with `:bnext` and `:bprevious`).


### Chapter 3: Searching Files
* To open a file in vim, you can use either `:find` or `:path`. 
```
:edit <path> FILENAME
:find <path> FILENAME
```
Their differences is that `:find` finds file in their `path` and we can set the path to what we desire (normally is user directory).
* There are 2 ways of searching files in Vim
> 1. Internal grep (:vim or :vimgrep)
> 2. External grep (:grep)
1. The `:vim` has the following syntax:
```
:vim /pattern/ file
```
Where `/pattern/` is a regex pattern ([Reference of Vim Regex Here.](https://vimregex.com/)) and the `file` argument to search pattern inside the file argument. Similar to `:find`, you can pass it some `*` and `**` wildcards.

After running thath, you will be redirected to the first result. `vim` search command uses `quickfix` operation. To see all search result, run `:copen` to open quickfix window. Use `:h quickfix` to learn about quickfix or here are some useful quickfix command
```
:copen     Open the quickfix window
:cclose    Close the quickfix window
:cnext     Go to next find
:cprev     Go to the prev find
:cnewer    Go to the newer find
:colder    Go to the older find
```
2. External greg. By default, it uses `grep` terminal command. For example if we want to search "lunch" inside the `app/controllers` directory, you can do this:
```
:grep -R "lunch" app/controllers/
```
The ripgrep command that will come later will have no diff in the command.

* Vim is also have it's built-in file explorer such as `netrw`. One way to launch `netrw` window is to using these command:
```
:Explore    Start netrw on current file
:Sexplore   Starts netrw on split top half of the screen
:Vexplore   Starts netrw on split left half of the screen
```
There are some plugin that more advanced than netrw such as [NERDTree](https://github.com/preservim/nerdtree) or [vim-vinegar](https://github.com/tpope/vim-vinegar)

* Using FZF plugins
First thing first, we need to have fzf and ripgrep already downloaded. And then we can setup the fzf in the `bashrc_profile` or (`$profile` if windows)
```
export FZF_DEFAULT_COMMAND='rg --files'
export FZF_DEFAULT_OPTS='-m'
```
and then use the fzf.vim plugin in the `vimrc`
```
# Setup Pluggin
call plug#begin()
Plug 'junegunn/fzf.vim'
Plug 'junegunn/fzf', { 'do': { -> fzf#install() } }
call plug#end()

# Setup ripgrep to :grep command
set grepprg=rg\ --vimgrep\ --smart-case\ --follow  
```
#### Note
Using vim-gripper can very useful to invoke the fzf and rg. Any docs of ripgrep [here](https://github.com/BurntSushi/ripgrep/blob/master/GUIDE.md)

* Search and replace in Multiple Files can be done in Vim using `:grep` (remember we already invoke the :grep method to have the ripgrep).
* The first method is to replacce all matching phrases, here's what you do:
```
:grep "pizza"
:cfdo %s/pizza/donut/g | update
```
> 1. :grep "pizza" uses ripgrep to search for all instances of "pizza"
> 2. :cfdo executes any command you pass in your quickfix list (in this case %s/pizza/donut/g to replace pizza with donut). The pipe (|) is a chain operator used invoke update command saves each file after substitution.

* The second method is to search and replace in selected files.
```
# Clear the buffer first
:%bd | e# (%bd deletes all the buffer and e# opens the file you were just on)
```
Run `:Files` (or Ctrl + F) to select the files. And then
```
:bufdo %s/pizza/donut/g | update (substituting all buffer entries with "donut")
```

### Chapter 4: Vim Grammar
* There is only one grammar rule in vim Language:
```
verb + noun
```
* Nouns are vim motions (motions are used to move around within vim)
```
# Below is list of motion in vim
h    left
j    down
k    up
l    right
w    move to next begining letter word's
}    jump to next paragraph
$    go to end of a line
0    go to the start of a line
...
and many more 
```
* Verb are vim operators (there are 16 operators in Vim), there are some of them:
```
y    tank text (copy)
d    delete text and save into register
c    delete text, save to register and start insert mode
```
Since we know the verb and nouns in vim, let's apply the grammar rule. Suppose you have these expression:
```
const text = "Hello word"
```
1. Suppose the cursor in at const, to `yank` to the end of the line: `y$`
2. To delete the next word: `dw`
3. To change the name of `const text`, just type `c2w`
* If the texts are structured (let's say HTML tags), we can also edit the content inside of it. For example we have these expression:
```
const hello = function() {
  console.log("Hello Vim");
  return true;
}
```
1. To delete the "Hello Vim" text we can put the cursor at H and `di(` (delete in "(" paramter )

Or these HTML tags:
```
<div>
  <h1>Header1</h1>
  <p>Paragraph1</p>
  <p>Paragraph2</p>
</div>
```
1. If we want to delete the content inside the <div>, put the cursor at "div" just type `dit` (delete in tag).

Text objects are powerful since we can target different objects from one location. we can delete the objects inside parantheses, function block etc. 
Here's a list of common text objects (you can learn more in `:h text-objects)`:
```
w         A word
p         A paragraph
s         A sentence
( or )    A pair of ( )
{ or }    A pair of { }
[ or ]    A pair of [ ]
< or >    A pair of < >
t         XML tags
"         A pair of " "
'         A Pair of ' '
`         A pair of ` `
```

* Vim can invoke set of general commands to perform a complex command (compasability)
* Motions and operators are extendable. You can create custom motions and operators to add into your vim. The [vim-textobj-user](https://github.com/kana/vim-textobj-user) plugin allows you to create your own text objects.

### Chapter 5: Moving in file
* Relative numbering in vim is useful when you've got a situation where you need to target some lines but don't know how much (like `d12j` to delete 12 line below)
* There are 2 types of word navigation unit: `word` and `WORD` where their difference are that word is a sequence of character containing *only* `a-zA-Z0-9_` and WORD is a sequence of all character *except* white space (space, tab, EOL). Let's say we have these expression:
```
const hello = "world";
```
1. It takes 21 key press with 'l'
2. Using 'w', it will take 6 and
3. Using 'W', it only take 4

* These are their definition
```
w     Move forward to the beginning of the next word
W     Move forward to the beginning of the next WORD
e     Move forward one word to the end of the next word
E     Move forward one word to the end of the next WORD
b     Move backward to beginning of the previous word
B     Move backward to beginning of the previous WORD
ge    Move backward to end of the previous word
gE    Move backward to end of the previous WORD
```

* You can do current line search with `f` and `t`. The difference is that `f` takes you to the first letter of the match and `t` takes you before the first match letter.
```
f    Search forward for a match in the same line
F    Search backward for a match in the same line
t    Search forward for a match in the same line, stopping before match
T    Search backward for a match in the same line, stopping before match
;    Repeat the last search in the same line using the same direction
,    Repeat the last search in the same line using the opposite direction
```

* Sentence and paragraph navigation can be done using these:
```
(    Jump to the previous sentence
)    Jump to the next sentence
{    Jump to the previous paragraph
}    Jump to the next paragraph
```
You also can do window navigation by these:
```
H     Go to top of screen
M     Go to medium screen
L     Go to bottom of screen
nH    Go n line from top
nL    Go n line from bottom
```

* Scrolling in Vim also can be done using this
```
Ctrl-E    Scroll down a line
Ctrl-D    Scroll down half screen
Ctrl-F    Scroll down whole screen
Ctrl-Y    Scroll up a line
Ctrl-U    Scroll up half screen
Ctrl-B    Scroll up whole screen
```

* Marking position to save your current pos and return to this pos later (like bookmark). you can set with a mark `mx` where `x` can be any alphabet.
```
ma    Mark position with mark "a"
`a    Jump to line and column "a"
'a    Jump to line "a"
```
To view all marks, use `:marks` where there are somme other marks
```
''    Jump back to the last line in current buffer before jump
``    Jump back to the last position in current buffer before jump
`[    Jump to beginning of previously changed / yanked text
`]    Jump to the ending of previously changed / yanked text
`<    Jump to the beginning of last visual selection
`>    Jump to the ending of last visual selection
`0    Jump back to the last edited file when exiting vim
```

* Summary, any motion that moves farther than a word is a jump (motion before this are jump). You can keep track where you've been when move around and see this list inside `:jumps`
```
'       Go to the marked line
`       Go to the marked position
G       Go to the line
/       Search forward
?       Search backward
n       Repeat the last search, same direction
N       Repeat the last search, opposite direction
%       Find match
(       Go to the last sentence
)       Go to the next sentence
{       Go to the last paragraph
}       Go to the next paragraph
L       Go to the the last line of displayed window
M       Go to the middle line of displayed window
H       Go to the top line of displayed window
[[      Go to the previous section
]]      Go to the next section
:s      Substitute
:tag    Jump to tag definition
```

# Useful References
Nickjj's Pluggins: https://github.com/nickjj/dotfiles/blob/master/.vimrc

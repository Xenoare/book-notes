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

### Chapter 6: Insert Mode
* There are many ways to get into insert mode
```
i      Insert text before the cursor
I      Insert text before the first character of the line
a      Append text after cursor
A      Append text at the end of a line
o      Starts new line below the cursor
O      Starts new line above the cursor
s      Delete the character under the cursor and insert text
S      Delete the line and insert text
gi     Insert text in the same pos where the last insert mode end
gI     Insert text at the start of line
```
* There are also different ways to exit insert mode
```
<Esc>      Exits insert mode and enter normal mode
Ctrl - [   
Ctrl - C   
```
* Deleting chunks is also possible in insert mode rather than in normal mode / using <Backspace>
```
Ctrl-h      Delete one character
Ctrl-w      Delete one word
Ctrl-u      Delete the entire line
```
* Vim register can store word for future use (it's using register to save the current word and paste it later), type `Ctrl-R` + register symbol (for now just register (a-z) ). To see in action, first we need to yank a word to register by this
```
"ayiw
```
1. Where `"a` is put the target of next action to the register a
2. and "yiw" is yank inner word to yank the word into register a
3. Now while in insert mode, to paste the stored word in register a, just type
```
Ctrl - R a
```

* Autocompletion in vim can be done using `Ctrl-X` to enter the sub-mode, Here are some useful autocomplete commands
```
Ctrl-X Ctrl-L    Insert a whole line
Ctrl-X Ctrl-N    Insert a text from current file
Ctrl-X Ctrl-I    Insert a text from included files
Ctrl-X Ctrl-F    Insert a file name
```
In general, Vim looks at the text in all available buffers for autocompletion source. If you have an open buffer with a line that says "Chocolate donuts are the best":
1. When you type "Choco" and do Ctrl-X Ctrl-L, it will match and print the entire line.
2. When you type "Choco" and do Ctrl-P, it will match and print the word "Chocolate".
Autocomplete is a vast topic in Vim. This is just the tip of the iceberg. To learn more, check out :h ins-completion.

* Executing normal mode command also can be done in insert mode if you're press `Ctrl-O` you'll be in `insert-normal sub-mode` (one sign to see it is the insert mode changes to `-- (insert) --`.
Here's some example:
```
Ctrl-O zz       Center window
Ctrl-O H/M/L    Jump to top/middle/bottom window
Ctrl-O 'a       Jump to mark a
```

### Chapter 7: Dot Command
* In general, you should try to avoid re-doing stuff possible. Using dot command we can redo the previous command for repetitions.
* Dot command as it's name used by pressing the dot key (`.`). For example, let's say we've got these expression:
```
let one = "1";
let two = "2";
let three = "3";
```
If we want to change "let" with "const", we can do these following things
1. Search with `/let` to find the first match
2. Change the `let` with `cw` and type `const` and escape with <Esc>
3. Navigate with `n` to find next match
4. Repeat the last command with dot command (`.`)

* Any time you update (add, modify, or delete) the content of the current buffer, you are making a **change**. Let' say you want to delete the textext from the start of the line to the next occurrence of a comma.
```
pancake, potatoes, fruit-juice,
```
1. First thing we can do is to delete the first word with `df,` and then repeat with `..` for the rest of 2 words.
> Dot command works to the previous command, the df command is going to delete the word until it found comma (it count as 1 changes). If you want to delete the comma, then the command `f,x..` will not work since the last change is x to delete the character after the cursor. To make this work just type `;` to find another match for comma and use the dot command to delete the character.

* Multi-line repeat also can be done in Vim, let say we have these expression:
```
let one = "1";
let two = "2";
let three = "3";
const foo = "bar';
let four = "4";
let five = "5";
let six = "6";
let seven = "7";
let eight = "8";
let nine = "9";
```
To remove all lines except the "foo" lines
1. First we can delete the first three lines with 'd2j'
2. Move the cursor below the foo lines with 'j'
3. Redo the changes before with `. .` 

* Including a motion in a change, we can use the `cgn` motion rather than `cw` since `gn` search for the last search pattern and automatically does a visual highlight. And to replace the next occurrence, just type (. .) rather than traverse with (n . n .)

* When you are editing, always be on the lookout for the motions that can do several things at once such as `gn` whenever possible.

### Chapter 8: Registers
* To use registers, you need to store them with operators (usually operators `y`, `c`, `d`) and to paste a text from register, you can use:
```
p     Paste the text after the cursor
P     Paste the text before the cursor
```
**There are 10 Vim register types:**
1. The unnamed register, where it stores the last text you yanked, changed, or deleted. To get the text from this register, do `""p` (default is `p`)
2. The numbered register, this register will fill themselves up in ascending order. There are 2 different numbered registers: the yanked register `0` and the numbered registers `1-9`
> The yanked registers, if you yank entire line (yy), Vim actually store that in two registers: The unnamed register (p) and the yanked registers ("0p) where the any other operation after yank will be stored in the (p) register and the yank is still in the yanked register
> The non-zero numbered registers, when you change or delete a text that is one line long, that text will be stored in 1-9 registers sorted by the most recent. To paste from this registers, do ("1p) to paste from the numbered regsiter 1 and (.) to the next register
3. The small delete register, changes or deletions taht less than one line (word example) stored in this register ("-)
4. The named register, it store the edit into registers (a-z). To yank a word into register a, you can do it with `"ayiw` where `"a` is a target for register a, and the `yiw` is yanks the word. and to get the text from this register, do `"ap`
> Sometimes you may want to add to your existing named register. In this case, you can append your text instead of starting all over. To do that, you can use the uppercase version of that register. For example, suppose you have the word "Hello " already stored in register a. If you want to add "world" into register a, you can find the text "world" and yank it using A register ("Ayiw).
5. The read-only registers, Vim has three read-only registers:
```
.    Stores the last inserted text
:    Stores the last executed command-line
%    Stores the name of current file
```
6. The expression register, uses `"=` to evaluate expression. Let's say to evalaute mathematical expressions `1+1`.
```
"=1+1<Enter>p
#or you can do in insert mode
Ctrl-R =1-1
```
> You also can get the values from any register via the expression regsiter when appended with `@`. if you with to get text from register a
```
"=@a <Enter> p
```
7. The selection registers, you can copy from external programs (like chrome) and paste in vim, and vice versa with `quotestar` (`"*`) and `quoteplus` (`"p`). Like for example to copy text from chrome and paste it to vim by `"*p` and to copy text from vim to clipboard by `*yiw` to copy a word (or `*yy` to copy an entire line to the clipboard)
8. The black hole register, You can use the black hole register ("_). To delete a line and not have Vim store the deleted line into any register, use "_dd.
9. The last search, To paste your last search (/ or ?), you can use the last search pattern register ("/). To paste the last search term, use "/p.
10. Viewing the registers, To view all your registers, use the :register command. To view only registers "a, "1, and "-, use :register a 1 -.


### Chapter 9: Macros
* Here's the basic syntax of Vim macro:
```
qa                     Start recording a macro in register a
q (while recording)    Stop recording macro
```
and Here's how you can execute a macro
```
@a    Execute macro from register a
@@    Execute the last execute macros
```
* Let's say you have these line and want to uppercase everything on each line
```
hello
vim
macros
are
awesome
```
With your cursor at the start of the first line, run:
```
qa0gU$jq
```
Where `qa` starts recording a macro in a register, `0` goes to beginning of the line, `gU$` to uppercase the text from current loc. to end of the line, `j` to goes one line down and `q` to stop recording.
To replay it, run `@a` (it support motions like `3@a` to exec 3 times)

* You also can execute this macro via command line by `:normal` command, this command accepts range as arguemnts such as if you want your macro between lines 2 and 3, you can run: `:2,3 normal @a`
  
* You can recursilvely exec. a macro by calling the same macro over and over. Suppose you have this list
```
a. chocolate donut
b. mochi donut
c. powdered sugar donut
d. plain donut
```
To make the first character is Uppercase. Run
```
qaqqa0W~j@aq
```
Where `qaq` records an empty maccro (it is imporatant since it will run whatever is in that register). `qa` starts recording on register a, `0` goes to the first character in the current line, `W` goes to next WORD, `~` to toggle the charcter under the cursor, `j` goes down one line, `@a` to executes the macro a. and q to step recording.
This thing goes recursively until there are on the last line where it tried to run `j`, it stop the macro.

* To append a macro, you can do by using capital letter of the register like `qA` to append to the register a.

Note: This macro module is kinda to complex, i need to learn it more in the future

### Chapter 10: Undo
* To perform a basic undo and redo, you can use `u` or `:undo` for undo and `Ctrl + R` or `:redo` to redo 

* You can make an undo breakpoint to mark the undo by `<Ctrl-G u>`, like for example `ione<Ctrl-G u> two<Esc>` to seperate one and two from undo.

* Undo tree is not easy to visualize. I find [vim-mundo](https://github.com/simnalamburt/vim-mundo) plugin to be very useful to help visualize Vim's undo tree. Give it some time to play around with it.

* Persistent undo, you can rollover to the last editing session by preserving undo history with `:wundo {my-undo-file}` and to recover it by `:rundo {undo-file}.undo`
* You can set the automatic undo persistence in `vimrc` config
```
set undodir=~/.vim/undo_dir
set undofile
```
The setting above will put all the undofile in one centralized directory, the ~/.vim directory. The name undo_dir is arbitrary. set undofile tells Vim to turn on undofile feature because it is off by default. Now whenever you save, Vim automatically creates and updates the relevant file inside the undo_dir directory (make sure that you create the actual undo_dir directory inside ~/.vim directory before running this).

* The `:earlier <time>` can be used to travel to a text state in the past. Like `:earlier 10s` will bring you back to the 10 seconds ago state.

### Chapter 11: Visual Mode 
* There are three ways to open a visual modes.
```
v                    Character-wise visual mode
V                    Line-wise visual mode
Ctrl-V Or Ctrl-Q     Block-wise visual mode
```
* Visual mode shares many operations with normal mode, let's say delete command or replace command
```
Chapter One
Chapter One 
```
You can replace the second line with visual mode `V` and type 'r=` to replace with `=========`

* You also can selectively apply command-lines on a highlighted block. Lets say you have these expressions:
```
const one = "one"
const two = "two"
const three = "three"
```
you can substitute the first two lines with any visual mode and run these substitute command `:s/const/let/g`

* Incrementing number is also possible in vim
```
<div id="app-1"></div>
<div id="app-1"></div>
<div id="app-1"></div>
<div id="app-1"></div>
<div id="app-1"></div>
```
It is a bad practice to have several ids having the same name, so let's increment them to make them unique:
1. Move your cursor to the "1" on the second line.
2. Start block-wise visual mode and go down 3 lines (`Ctrl-V 3j`). This highlights the remaining "1"s. Now all "1" should be highlighted (except the first line).
3. Run `g Ctrl-A`. (`g Ctrl-A` increments numbers on multiple lines)

* You can selecting the last visual mode by using `gv` to quickly highlight the last visual mode, or you can use these command marks
```
`<    Go to the first place of the previous visual mode highlight
`>    Go to the last place of the previous visual mode highlight
```

### Chapter 12: Search and Subtitute
* You can filter to match the first and last character in line using `^` and `$`. For example, if you want to target the first "hello" in line, use `/^hello` and vice versa. 
* You also can repeat the previous search with `//`, and to see all your search history, you can run with `:history /`

* Using regex to match any search. If you wanted to search either one or two character in a text, you can use the `|` operator, like
```
\hello\|hola     # This will search hello or hola
\vhello|hola     # This method is also work using magic `v` button rather than \|
```

* You can search any digit or alfabet by using some regex, `/[0-9]` to search any digit number, or `/[a-zA-Z]` to search for any upper/lower alphabet (You also can combine both, let's say for hex searching pattern `/[0-9a-fA-F]`)

* And you also can do a negative search by using `^` inside the bracket ( `/[^0-9]` this will search for a non-digit)

* You can also search for any repeating character like `11` or `111` by these regex, `count` command has these syntax `{n,m}` where this command has 4 variations:
1. {n} is an exact match. /[0-9]\{2\} matches the two digit numbers: "11" and the "11" in "111".
2. {n,m} is a range match. /[0-9]\{2,3\} matches between 2 and 3 digit numbers: "11" and "111".
3. {,m} is an up-to match. /[0-9]\{,3\} matches up to 3 digit numbers: "1", "11", and "111".
4. {n,} is an at-least match. /[0-9]\{2,\} matches at least a 2 or more digit numbers: "11" and "111".

* There are some predifired character ranges
```
\d    Digit [0-9]
\D    Non-digit [^0-9]
\s    Whitespace character (space and tab)
\S    Non-whitespace character (everything except space and tab)
\w    Word character [0-9A-Za-z_]
\l    Lowercase alphas [a-z]
\u    Uppercase character [A-Z]
```

* Below is any search example of text using regex
1. Let's say you want to search a phrase surrounded by a pair of double quotes
```
"Vim is awesome!"
# Run this
/"[^"]\+" or
/\v"[^"]+"
```
2. Or when you want to capture a phone number
```
123-456-789
# Run this
/\v\d{3}-\d{3}-\d{3}
```

* The substitution syntax are:
```
:[range #usually (x,y) or % for entire file]s/{old-pattern}/{new-pattern}/[substitution flag]
```

* You also can do substitution based on a pattern matching.
1. let's say you have these expressions:
```
let one = 1;
let two = 2;
let three = 3;
let four = 4;
let five = 5;
```
To add a pair of double quoutes around the digits:
```
:s/\v\d/"\0"/
# Where \0 is a special character flap representating the entire macthed pattern.
```
2. Or this situation where you want to swap the variable names
```
one let = "1";
two let = "2";
three let = "3";
four let = "4";
five let = "5";
```
You can do this:
```
%s/\v(\w+) (\w+)/\2 \1/
# Where \w+ is used as a group match where this takes ranges of a word character more than one
# \2 \1 used to capture the group in a reversed order
```
* There are some useful substtituion flag (or you can check `:h s_flags`).
```
&    Reuse the flags from the previous substitute command.
g    Replace all matches in the line.
c    Ask for substitution confirmation.
e    Prevent error message from displaying when substitution fails.
i    Perform case insensitive substitution.
I    Perform case sensitive substitution.
```

* You also can do special replace (like `\U` or check `:h sub-replace-special)`). Let's say you want to uppercase this word
```
vim is the greatest text editor in the whole galaxy
```
You can run
```
:s/\<./\U&/g
# Where \<  match the start of a word and . to match andy character, so it will match the first character of any word. \U& uppercases the subsequent symbol where & represent the whole match
```

* You can also need to match for multiple pattern, ley's say ou have these expressions
```
hello vim
hola vim
salve vim
bonjour vim
```
To substitute the word "vim" with "friend", but only on the lines contain the word "hello" or "hola" you can do this
```
:%s/\v(hello|hola) vim/\1 friend/g
# Where \1 is the first group, which is either text "hello" or "hola"
```

* You can substitute the n-th match in a line with this
```
One Mississippi, two Mississippi, three Mississippi, four Mississippi, five Mississippi.
```
```
:s/\v(.{-}\zsMississippi){3}/Arkansas/g
# Where . is a single repeat and {-} performs non-greedy match of 0 or more of the preceding atom, where (...){3} is looking for the third match.
```
The `{-}` finds the shortest match of the given pattern, contrast with `*` finds the longest match

* Alternatively you can also run substitute command accross multiple files with macros
```
:args *.txt
qq
:%s/dog/chicken/g
:wnext
q
99@q

# Where wnext saves the file and go to the next file on the args list
```

### Chapter 13: Global Command
* The global command has the following syntax:
```
:g/pattern/command
```
Lets say you have these expressions:
```
const one = 1;
console.log("one: ", one);

const two = 2;
console.log("two: ", two);

const three = 3;
console.log("three: ", three);
```
To remove all lines containing "console", you can run:
```
:g/console/d
```

* You can run command for the inverse match by using this
```
:g!/patter/command
or
:v/patter/command
```
* You can pass a range before the `g` command
1. `:1,5g/console/d` matches the string "console" between lines 1 and 5 and deletes them.
2. `:,5g/console/d` if there is no address before the comma, then it starts from the current line. It looks for the string "console" between the current line and line 5 and deletes them.
3. `:3,g/console/d` if there is no address after the comma, then it ends at the current line. It looks for the string "console" between line 3 and the current line and deletes them.
4. `:3g/console/d` if you only pass one address without a comma, it executes the command only on line 3. It looks on line 3 and deletes it if has the string "console".
> In addition to numbers, you can also use these symbols are range.
> * . means the current line. A range of .,3 means between the current line and line 3.
> * $ means the last line in the file. 3,$ range means between line 3 and the last line.
> * +n means n lines after the current line. You can use it with . or without. 3,+1 or 3,.+1 means between line 3 and the line after the current line.

* You also can use macro with the global command. let say you to add a `;` in a lines with "const", then you have to do this:
```
:g/const/normal @a
``` 

* You also can recursively use global command as a type of command-line. let say you want to delete the second `console.log` statement:
```
const one = 1;
console.log("one: ", one);

const two = 2;
console.log("two: ", two);

const three = 3;
console.log("three: ", three);
```
You can run
```
:g/console/g/two/d
# Where the first g is looking for "console" pattern and the second g is looking for the "two" pattern.
```

* To reverse the entire buffer, run
```
:g/^/m 0
# The ^ to match all lines, including empty lines. and m is to moves the lines to the given destination, in this case the range is "^" and the destination is "0".
```

* You can also pass a range to limit the command
```
:5,10g/^/m 0
# This is to reverse the line between line 5 and 10
```

* When coding, sometimes i would write TODOs in the file that i'm editing
```
const one = 1;
console.log("one: ", one);
// TODO: feed the puppy

const two = 2;
// TODO: feed the puppy automatically
console.log("two: ", two);

const three = 3;
console.log("three: ", three);
// TODO: create a startup selling an automatic puppy feeder
```
You can keep track of the created TODOs by using `:t`(copy) or `:m`(move) method
```
:g/TODO/t $
or 
:g/TODO/m $
# Both lines search for pattern TODO and copy or move to the end of the buffer
```

* Recall from the register chapter that deleted texts are stored inside the numbered registers (granted they are sufficiently large ). Whenever you run :g/console/d, Vim stores the deleted lines in the numbered registers. If you delete many lines, you can quickly fill up all the numbered registers. To avoid this, you can always use the black hole register ("_) to not store your deleted lines into the registers. Run:
```
:g/console/d_
```
By passing _ after d, Vim won't use up your scratch registers.

* You can also run the global command with this form
```
g/pattern1/,/pattern2/command
```
Let's say you want to reduce the empty lines into one empty line with:
```
:g/^$/,/./-1j
# Where the first pattern ^$ is represents for an empty line. , separates the range. In this case, it specifies a range from the matched empty line (/^$/) to the next line containing any content (/./). This range encompasses consecutive empty lines.
The -1 means offset that subtraccts one from the ending line, and the j is the commmand used to join lines.
```

* Vim has `:sort` command to sort the lines within a range. If you need to sort the elements inside the arrays, you can run this:
```
:g/\[/+1,/\]/-1sort
# Where /\[ is meaning the left bracket and +1 refers line below it. /\] is meaning the right bracket and -1 refers the line above it.
```
The conclusion is that `/\[/+1,/\]/-1 then refers to any lines between "[" and "]".

### Chapter 14: External Commands
* The bang command (`!`) can do three things:
1. Read the STDOUT of an external command into the current buffer. Let's say you want to STDOUT the entire directory, you can do this:
```
:r !dir
# Where :r is Vim's read command.
```
2. Write the content of your buffer as the STDIN to an external command.
3. Execute an external command from inside Vim. Let's say you want to open a cmd in vim, you can do this instead:
```
:!cmd
```

### Chapter 15: Command-line Mode
* There are 4 different commands to enter the command-line mode:
1. Search patterns (`/`, `?`)
2. Command-line commands (`:`)
3. External commands (`!`)

* You also can repeat the previous command by using `@: `

* You can use open command-line history by using `:his :` (you can check more on `:h :his`) and the output should be like this
```
## Cmd history
2  e file1.txt
3  g/foo/d
4  s/foo/bar/g
```
There's also some shortcut to open history mode by pressing `q:`

* Vim has hundreds of built-in commands. To see all the commands Vim have, check out :h ex-cmd-index or :h :index.

### Chapter 16: Tags
> Ref. Here: https://courses.cs.washington.edu/courses/cse451/10au/tutorials/tutorial_ctags.html

* Usually tag item is composed fo four componenents such as a `tagname`, a `tagfile`, a `tagaddress` and a tag options.
```
1.  {tagname} {TAB} {tagfile} {TAB} {tagaddress}
2.  {tagname} {TAB} {tagfile} {TAB} {tagaddress} {term} {field} ..
```

* You also can exclude some module since it will take long time (let's say node_module)
```
ctags -R --exclude=node_modules .
```

* Beside of using `CTRL-]`, you also can use command `:tag {tag-name}` to jump.

* There are some tag priority if vim is presented with duplicate item names
```
A fully matched static tag in the current file.
A fully matched global tag in the current file.
A fully matched global tag in a different file.
A fully matched static tag in another file.
A case-insensitively matched static tag in the current file.
A case-insensitively matched global tag in the current file.
A case-insensitively matched global tag in the a different file.
A case-insensitively matched static tag in the current file.
```

### Chapter 17: Fold
* The fold operator `z` hide some line text. Remember the fold operator `zf` can used with a motion of text object. 
```
+-- 2 lines: Fold me -----
```

* You can open a folded text with `zo` and `zc` to close the fold. There are some many more folding commands in `:h fold-commands`

* There are six different folding method (you can change the fold by `:set foldmethod={mode}` where the default is `manual`). You can check the ref [here](https://github.com/iggredible/Learn-Vim/blob/master/ch17_fold.md)
```
1. Manual
2. Indent
3. Expressions
4. Syntax
5. Diff
6. Marker
```

### Chapter 18: Git
* `vimdiff` command can be used to show the differences between multiple files

* You can move from one diff to another with `]c` to next diff and `[c` to prev diff.

* Another useful vim pluggins for git is `vim-fugitive` (you can checkmore in `:h fugitive`) 
> Here's the link vidio reference: https://www.youtube.com/watch?v=uUrKrYCAl1Y

### Chapter 19: Compile
You can use `:make` commmand [u must create a file named `makefile` in current directory] (this is only working in linux with gnu engine).

* When you run `:make`, vim actually runs whatever command in the `makeprg` option. If u run `:set makeprg?`
```
makeprg=make (this is the default value)
```
> For more information, check out `:h :compiler` and `:h write-compiler-plugin` 

* You also can use auto-compiler on every save by using vim `autocmd` to trigger automatic actions based on certain events. Let's say we want to automatically compiler `.cpp` files, we can add this in .vimrc
```
autocmd BufWritePost *.cpp make
```

* You can switch a compiler to executes whatever the commands is assigned to `makeprg` (default is `make`).
```
:compiler ruby
```
This will run the $VIMRUNTIME/compiler script and changes the  `makeprg` to use the `ruby` command.

### Chapter 20: Views, Sessions and Viminfo
* View is a collection of settings for one window. U can preservve the maps and folds by using view
```
# Let's say we have some .txt file that folded and has no rel. number

+-- 5 lines: foo1 -----
foo6
foo7
foo8
foo9
foo10
```
We can save the view by using this
```
:mkview
```
this will create a view file indside the `viewdir` (check `:h viewdir` for more information) path.


* You can load the view by open the file and run:
```
:loadview
```

* As defaults, vim save 9 numbered views (1-9), here's the example
```
# To save a view 1
:mkview 1

# To load a view 1
:loadview 1
```

* Session saves the information of all windows (including the layout). Suppose you have project with three files `foo.txt`, `bar.txt`, `bar.txt` and you split your windows with `:split` and `:vsplit`. You can preserve the session by
```
:mksession
```
> mksession saves a session file (`Session.vim`) in the current directory

* To load a session, run:
```
:source Session.vim
```

* You also can configure any attributes such as tab, buffers, etc, to check the attribute that being saved, run:
```
:set sessionoptions?
```
> Here are some attributes that sessionoptions can store:
> * blank stores empty windows
> * buffers stores buffers
> * folds stores folds
> * globals stores global variables (must start with an uppercase letter and contain at least one lowercase letter)
> * options stores options and mappings
> * resize stores window lines and columns
> * winpos stores window position
> * winsize stores window sizes
> * tabpages stores tabs
> * unix stores files in Unix format
For more complete list, check `:h 'sessionoptions'`

* Viminfo save the internal attributes such as register, mark, macros and many more.

* Make sure that you have nocompatible option set (set nocompatible), otherwise your Viminfo will not work.

### Chapter 21: Multiple File Operations
* Vim has eight ways to execute command accross multiple files:
1. arg list (`argdo`)
The most basic list, first you can create a list 
```
:args file1 file2 file3

# and then you can do a run with argdo (let's say we want to change donut with banana)
:argdo %s/donut/banana/g | update 
```

2. buffer list (`bufdo`)
Buffer list created when you edit a files, since every file opened is stored in a buffer. You can traverse the buffer by using command `:buffers` or `:bnext`, `:bprev`

3. window list (`windo`)
4. tab list (`tabdo`)
These two things same as buffers, the difference is their syntax
```
For example, if you have three windows opened (you can open new windows with Ctrl-W v for a vertical window and Ctrl-W s for a horizontal window) and you run :windo 0put ='hello' . @%, Vim will output "hello" + filename to all open windows.

```
5. quickfix list (`cdo`)
6. quickfix list filewise (`cfdo`)
7. location list (`ldo`)
8. location list filewise (`lfdo`)

### Chapter 22: Vimrc
* In the nutshell, a vimrc is a collection of:
1. Plugins
2. Settings
3. Custom Functions
4. Custom Commands
5. Mappings

* Vimrc is a good place for custom function. You can create a custom Command-line with `command`. Let's say we create a basic command `GimmeDate` to display today's date
```
:command! GimmeDate echo call("strftime", ["%F"])
```

* The nnoremap command used above can be broken down into three parts:
1. n represents the normal mode.
2. nore means non-recursive.
3. map is the map command.

* You can organizing vimrc by splitting vimrc into some file. You are going to split it into four components:
1. Third-party plugins (~/.vim/settings/plugins.vim).
2. General settings (~/.vim/settings/configs.vim).
3. Custom functions (~/.vim/settings/functions.vim).
4. Key mappings (~/.vim/settings/mappings.vim) .
```
# Inside ~/.vimrc
source $HOME/.vim/settings/plugins.vim
source $HOME/.vim/settings/configs.vim
source $HOME/.vim/settings/functions.vim
source $HOME/.vim/settings/mappings.vim
```

### Chapter 23: Vim Packages
* Vim has it's built-in plugin manager called *packages*
```
.vim/pack/{name-folder}/{start|opt}
or 
vimfiles/pack/{name-folder}/{start|opt} 
```

* There are two types of Loading packages mechanisms
1. Automatic loading
To load plugins when Vim starts, you need to put them in the `start/` directory
```
vimfiles/pack/{name-folder}/{start} 
```
2. Manual Loading
To load plugin manually when Vim starts, you need to put them into the `opt/` directory
```
vimfiles/pack/{name-folder}/{opt}
```
Every time you need the plugin, you have to load the pluggin first
```
:packadd {pluggin-folder}
```

* You can organize the packages to group your pluggins based on categories such as:
```
~/.vim/pack/colors/
~/.vim/pack/syntax/
~/.vim/pack/games/
```

### Chapter 24: Vim Runtime
* Vim has a plugin runtime path (In the ~/.vim/plugin) that executes any script in this directory one each time Vim starts. Let's say in this file `~/.vim/plugin/donut.vim`
```
echo "donut!"
```
Now, every time you start Vim, you will see both "donut!" echoed before get in into the vim.

* Vim knows how to detect "common" file types (Ruby, Python, Javascript, etc). But what if you have a custom file? You need to teach Vim to detect and assign it with the correct file type.

* There are two methods of detection using file name and file content. 
1. File name detection
File name detection detects a file type using the name of that file. Let's say when you open the hello.rb, Vim knows it is a Ruby file from the `.rb` extension.

* There are two ways to do file name detection
1. Using `ftdetect/`
This method using a directory named `ftdetect/` in the runtime `~/.vim/`. Let's say you have an weird file `hello.banana`, u can create a file name inside the file.
`~/.vim/ftdetect/banana.vim` and add:
```
autocmd BufNewFile,BufRead *.banana set filetype=banana
```
Where `BufNewFile` and `BufRead` are triggered whenever you create a new buffer and open a buffer. `*.banana` means that this event will only be triggered if the openned buffer has a `.banana` filename extension. Finnaly `set filetype=banana` command sets the file type to be a banana file.

2. Using filetype.vim
The second file detection requires you to create a `filetype.vim` in the root directory (`~/.vim/filetype.vim`). Let's say you have `hello.plaindonut` file, you can add this:
```
if exists("did_load_filetypes")
  finish
endif

augroup donutfiletypedetection
  
  # Below here to add a new file extension
  autocmd! BufRead,BufNewFile *.plaindonut setfiletype plaindonut

augroup END
```

2. File typescript
* If you want to detect and assign a file based on the file content.  if you have some unknown file and want to assign these files to a `donut`, you can make these files and add a line contains (for example in this case `donutify`).Then in the runtime root path, add a `scripts.vim` file (`~/.vim/scripts.vim`). Inside it, add these:
```
if did_filetype()
  finish
endif

if getline(1) =~ '^\\<donutify\\>'
  setfiletype donut
endif
```
The function `getline(1)` returns the text on the first line. It checks if the first line starts with the word "donutify". The function did_filetype() is a Vim built-in function. It will return true when a file type related event is triggered at least once. It is used as a guard to stop re-running file type event.

* Note that `scripts.vim` is only run when Vim opens a file with an unknown file type. If Vim opens a file with a known file type, `scripts.vim` won't run.

* Vim has an indent runtime path that works similar to ftplugin, where Vim looks for a file named the same as the opened file type. The purpose of these indent runtime paths is to store indent-related codes. If you have the file `~/.vim/indent/chocodonut.vim`, it will be executed only when you open a chocodonut file type. You can store indent-related codes for chocodonut files here.

* Vim has a colors runtime path (`~/.vim/colors`) to store color schemes. Any file that goes inside the directory will be displayed in the `:color` command line command. If you want to check out the color schemes other people made, a good place to visit is [vimcolors](https://vimcolors.com/).

* Vim also has a syntax runtime path (`~/.vim/syntax`) to define sytax highlighting. The [vim-polyglot](https://github.com/sheerun/vim-polyglot) plugin is a great plugin that provides highlights for many popular programming languages.

* Vim have a doc runtime, if u have created a plugin and need a documentation. Let's try to create a file (`~/.vim/doc/donut.txt`). Add these inside:
```
*chocodonut* Delicious chocolate donut

*plaindonut* No choco goodness but still delicious nonetheless
```
* If you try to search for chocodonut and plaindonut (:h chocodonut and :h plaindonut), you won't find anything.

* First, you need to run :helptags to generate new help entries. Run :helptags ~/.vim/doc/

* Now if you run :h chocodonut and :h plaindonut, you will find these new help entries. Notice that the file is now read-only and has a "help" file type.

* The function naming convention for the autoload feature is:
```
function fileName#functionName()
  ...
endfunction
```

* To invoke a function, you need the call command. Let's call that function with `:call tasty#donut()`.

* Vim has an after runtime path (`~/.vim/after/`) that mirrors the structure of `~/.vim/`. Anything in this path is executed last, so developers usually use these paths for script overrides.

* For example, if you want to overwrite the scripts from `plugin/chocolate.vim`, you can create `~/.vim/after/plugin/chocolate.vim` to put the override scripts. Vim will run the `~/.vim/after/plugin/chocolate.vim` after `~/.vim/plugin/chocolate.vim`.

### Chapter 25: Vimscript Basic Data Types
* Vim has Ex-mode like an extended command-line version. To enter the Ex-mode, you simply can type `Q` or `gQ` in normal mode.

* The `:echo` or `:echom` prints the evaluated expressions you give, but the `:echom` stores the result in the message history

* You can view the message
```
:message

# And here's to clear your message
:message clear
```

* Vim has 4 different number types:
1. Decimal
2. Hexadecimal, starts with `0x` or `0X`
3. Binary, starts with `0b` or `0B`
4. Octal, starts with `0`, `0o` and `0O`

* There are two ways represent the floating number. The `dot notation` (like 31.4) and `exponent` (like 3.14e1), `ex` is like `10^x`.
```
:echo +123.4
" returns 123.4

:echo -1.234e2
" returns -123.4

:echo 0.25
" returns 0.25

:echo 2.5e-1
" returns 0.25
```

* There are few string operation that you can do
1. String Concatenation
To concatenate a string in Vim, use the . operator.
```
:echo "Hello" . " world"
" returns "Hello world"
```
2. String Arithmetic
When you run arithmetic operators (+ - * /) with a number and a string, Vim coerces the string into a number.
```
:echo "12 donuts" + 3
" returns 15
```
Remember, for this string-to-number to work, the number character needs to be the `first character in the string`.

* There are some difference between single and double quotes in string, double quotes can accept special character which is `\` like `\n` to acts as a newline or `\"` to behaves like a literal `"`.
> For a list of other special charaters, check out `"h expr-quote`.

* There are also many other string procedures, you can check out on `:h string-functions`

* Vimscript list is like an Array in Javascript or List in Python (If you have already understand that it's good then).

* For more list function operation, check `:h list-functions`

* You can unpact a list and assign variables to the list items:
```
:let favoriteFlavor = ["chocolate", "glazed", "plain"]
:let [flavor1, flavor2, flavor3] = favoriteFlavor

:echo flavor1
" returns "chocolate"

:echo flavor2
" returns "glazed"

# To assign the rest of the item you can use ; followed by a variable name
:let favoriteFruits = ["apple", "banana", "lemon", "blueberry", "raspberry"]
:let [fruit1, fruit2; restFruits] = favoriteFruits
```

* A Vimscript dictionary is an associative, unordered list. A non-empty dictionary consists of at least a key-value pair.
```
{"breakfast": "waffles", "lunch": "pancakes"}
{"meal": ["breakfast", "second breakfast", "third breakfast"]}
{"dinner": 1, "dessert": 2}
```

* To convert a dictionary into a list of lists, use `items()`
```
:let mealPlans = #{breakfast: "waffles", lunch: "pancakes", dinner: "donuts"}

:echo items(mealPlans)
" returns [['lunch', 'pancakes'], ['breakfast', 'waffles'], ['dinner', 'donuts']]
```

* Vim has some special primitives:
1. `v:true` which is equivalent of `true` or a non-0 value.
2. `v:false` which is equivalent of `false`
3. `v:none` which is equal to `null`
4. `v:null`

### Chapter 26: Vimscript Conditionals and Loops 
* Vim has some relational operators for comparing strings:
```
# First is =~ to performs a regex match against given string
a =~ b

# Second is !~ is the inverse of !~
a !~ b
```

* You can always match the case by using some suffix `#` at the end
```
set ignorecase
echo str =~# "hearty"
" returns true

echo str =~# "HearTY"
" returns false

set noignorecase
echo str =~# "hearty"
" true

echo str =~# "HearTY"
" false

echo str !~# "HearTY"
" true
```

* The if-conditional operator, has these syntax
```
if {clause}
  {some expression}
endif
```

* The for looop is commonly used with the list data type
```
let meals = [["breakfast", "pancakes"], ["lunch", "fish"], ["dinner", "pasta"]]

for [meal_type, food] in meals
  echo "I am having " . food . " for " . meal_type
endfor
```
* For error handling, vim has `try`, `finally and catch` to handle errors. To simulate an error, you can use the `throw` command.
```
try
  echo "Try"
  throw "Nope"
catch
  echo "Caught it"
finally
  echo "Finally"
endtry
```
This time Vim displays both "Caught it" and "Finally". No error is displayed because Vim caught it.

* The difference between catch and finally is that finally is always run, error or not, where a catch is only run when your code gets an error.

### Chapter 27: Vimscript Variable Scopes

# Useful References
Nickjj's Pluggins: https://github.com/nickjj/dotfiles/blob/master/.vimrc
Idiomatic-vimrc: https://github.com/romainl/idiomatic-vimrc/blob/master/README.md#defaultsvim

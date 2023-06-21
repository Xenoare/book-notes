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

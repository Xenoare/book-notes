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

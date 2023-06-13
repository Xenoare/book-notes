## Learn Vim (the Smart Way)

by iggredible [Ref.](https://github.com/iggredible/Learn-Vim)

### Chapter 1: Starting Vim
* The vim command usually started with `:` and there are so many options you do co with it:
* Opening a file: you can open a file by typing in terminal `vim <file>`, and also vim support opening multiple windows and multiple files by simply typing `vim -o2 file1.txt file2.txt`, this is will create a 2 horizontal window and fill the first one with file1.txt and file2.txt. The argument `-o<window>` is possible to open multiple page.
* You can start coding in vim by typing `i` to switch to insert mode.
* Saving and exiting file: You can save ur file by command `:write` or `:w` and `:write <file>` if the file isn't created. For the exiting a file, you simply just type `:quit` or `:q` to quit.
* There are so many command in vim. So to help the user, vim provides help pages by this command `:help {some-command}` or `:h`.
* How can i search for relevant command in vim? Just typing some command like `:h quit` and using `tab`, vim will display relevant keywords to work with.
* Suspending a file can be done by just using `:suspend` or `CTRL-Z` to suspend, and if u want to back to the original file. just simply type `fg` or `exit` (if it on windows) to back to the suspended file. 

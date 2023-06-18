## Vimtutor

### Lesson 1
* **To move the cursor, press the h, j, k, l keys are indicated**
```
      ^
      k           Hint: The h keys is at the left and moves left
< h       l >           The l keys is at the right and moves right
      j                 The j keys look like a down arrow
      v
``` 
* Vim can be started from shell by prompt type: `vim FILENAME <ENTER>`
* To exit vim type:
```
<ESC> :q! <ENTER> to trash all changes
<ESC> :wq <ENTER> to save all changes and quit
```
* You can insert or append text type by:
```
i to insert before the cursor / I to insert at the beginning of a line
a to append after the cursor / A to append after the line
```
* To delete the character at the cursor type: `x`

### Lesson 2
* The format for a change command is:
```
    operator [number] motion
```
where:
> * operator - is what to do such as `d` for delete
> * [number] - is an optional count to repeat the motion
> * motion - moves over the text to operate on, such as **w** (word), **e** (end of word), **$** (end of the line), etc
* To move to the start of a line use a zero `0`
* To undo previous actions, type:         u (lowercase u)
* To undo all changes on a line, type:    U (capital U)
* To redo, type:                          CTRL-R

### Lesson 3
* To put back the text that just beenn deleted, type `p`. This put the deleted text (or line) after the cursor (or below the cursor if deleted)
* To replace a character under a cursor, type `r$` where `$` is the character u want to have there.
* Or you can replace a word by using motion, like `ce` or `cw` used to change a word or just simply use `R (capital r)` to enter replace mode and replace the word in it.
* The format for change is:
```
c [number] motion
```

### Lesson 4
* CTRL-G displays your location in the file and the file status.
* To moves between lines in the files:
```
G used to moves to the end of the file
gg moves to the first line
[number] G used to that line number, 4G to line 4
```
* To search a phrase, type `/\v` in normal mode and type any phrase that u want to search.
* After a search type, type `n` to find the next occurrence and `N` in the opposite direction. You can traverse back and forth by using `CTRL-O` to prev positions and `CTRL-I` to newer positions.
* To substitute new for the first old in a line type :s/old/new
* To substitute new for all 'old's on a line type : s/old/new/g
* To substitute phrases between two line #'s type :#,#s/old/new/g
* To substitute all occurrences in the file type :%s/old/new/g
* To ask for confirmation each time add 'c' :%s/old/new/gc

### Lesson 5
* !command executes an external command
* `:w FILENAME` writes the current vim file
* `v (enter visual mode) [motion] :w FILENAME` saves the visually selected lines in the file, ex `v 2w :w test.txt`
* `:r FILENAME` retrieves disk file and puts it below the cursor position.
* `:r !dir` reads the output of the dir command and puts it belows the cursor positions.

### Lesson 6
* The `y` operator yanks (copies) text, and `p` puts (pastes) it.
* Typing `:set xxx` sets the options `xxx`. Some options are:
> * 'ic' or 'ignorecase' ignore upper/lowercase when searching
> * 'is' or 'incsearch' show partial matches for a search phrase
> * 'hls' or 'hlserach' highlight all matching phrases




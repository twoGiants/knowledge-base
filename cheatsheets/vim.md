# Vim

All commands are from vimtutor.

## Insert Append Open

- `a   `: append after the cursor
- `A   `: append at line end
- `i   `: insert before the cursor
- `o   `: insert below current line
- `O   `: insert above current line

## Delete

- `x   `: delete character
- `dw  `: delete word
- `2dw `: delete 2 words
- `d2w `: same
- `d$  `: delete from cursor till end of line
- `dd  `: delete line
- `3dd `: delete 3 lines

## Move by Word

- `w   `: move word by word, starting with first letter
- `0   `: move to start of the line
- `e   `: move word by word, starting with last letter

## Undo Redo

- `u   `: undo
- `U   `: undo line
- `C-r `: redo

## Copy Paste Replace

- `y   `: copy selection after you selected some with `v`
- `yw  `: copy word
- `y2w `: copy two words
- `yy  `: copy line
- `y$  `: copy from cursor till end of line
- `p   `: paste, from `y` also from `dd`
- `r{c}`: replace character
- `R   `: replace more than one char
- `ce  `: deletes word and places you in INSERT mode
- `cc  `: same for the whole line
- `c2e `: deletes 2 words and places you in INSERT mode

## Jump to Lines

- `C-g `: show status and line where you are
- `G   `: go to end of the file
- `gg  `: go to start of the file
- `{n}G`: go to line n, e.g. `103G` goes to line 103

## Navigate

- `C-o `: go back
- `C-i `: go forward

## Find Words

- `/{w}`: search forward for this w=word
- `?{w}`: search backward for this w=word
- `n   `: go to next search result
- `N   `: go to prev search result

## Find Parenthesis

- `%   `: push on a parenthesis and it will jump to the closing/opening one

## Substitute

- `:s/old/new     `: substitute 'old' word with 'new'
- `:s/old/new/g   `: substitute old word with new in whole line
- `:#,#s/old/new/g`: substitute old word with new between #'s whole line
- `:%s/old/new/g  `: substitute old word with new in whole file
- `:%s/old/new/gc `: promt whether to substitute old word with new in whole file

## Execute Shell Commands:

- `:!{shc}  `: execute any shell command and show output
- `:!ls -la `: e.g. `ls -la`

## Writing Files

- `:w file.txt  `: save the current file under `file.txt`
- `:!rm file.txt`: remove the file `file.txt`

## Select

- `v            `: enter select mode
- `C-v          `: enter select block mode
- `S-v          `: enter select line mode
- `v :w file.txt`: enter select mode, then save selection to `file.txt`

## Merge

- `:r file.txt`: puts content of `file.txt` below cursor
- `:r !ls     `: puts output of `ls` shell command below cursor

## Some Options

- `:set ic  `: ignore upper/lower case when searching
- `:set hls `: highlight search findings
- `:set nu  `: line numbers
- `:set noic`: turn off `ic`

## Command Completion and Help

- `:e C-d `: shows possible completions for `e`
- `:help  `: opens help
- `:q     `: closes help
- `C-w C-w`: jump to another window
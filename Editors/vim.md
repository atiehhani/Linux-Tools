# Vim


## Arrow keys mixed with numbers

| Command | Description |
|---------|-------------|
| `j` / `4j` | Move cursor **down** (4 lines with `4j`) |
| `k` / `6k` | Move cursor **up** (6 lines with `6k`) |
| `l` / `2l` | Move cursor **right** (2 characters with `2l`) |
| `h` / `5h` | Move cursor **left** (5 characters with `5h`) |



## For word 

| Command | Description |
|---------|------------|
| `w`     | Move to the beginning of next word |
| `3w`    | Move forward 3 words (to the beginning of each word) |
| `e`     | Move to the end of next word |
| `5e`    | Move forward 5 word-ends |
| `b`     | Move back to the beginning of previous word |


##  For file 

| Command | Description                     |
|---------|---------------------------------|
| `gg`    | Go to the first line of file    |
| `5gg`   | Go to line 5 of file            |
| `G`       | Go to the last line of file  |
| `Shift+g` | Same as `G` (go to last line)|


## For line

| Command | Description                |
|---------|----------------------------|
| `i`     | Insert before cursor       |
| `a`     | Insert after cursor        |            |
| `0`     | Move to beginning of line      |
| `^`     | Move to first non‑blank char   |
| `I`     | Go to first non‑blank char & insert |
| `$`     | Move to end of line    |
| `A`     | Go to end of line & insert                   |
| `o`          | Open new line below & enter insert mode          |
| `10o + Esc`  | Open 10 new lines below                          |
| `O`     | Open new line above & enter insert mode      |


## Cut / Delete Commands


| Command | Description                         |
|---------|-------------------------------------|
| `x`     | Delete one character under cursor   |
| `5x`    | Delete 5 characters                 |
| `dw`    | Delete one word                     |
| `5dw`   | Delete 5 words                      |
| `d^`    | Delete from cursor to first non‑blank char |
| `d$`    | Delete from cursor to end of line         |
| `D`     | Same as `d$` (delete until end of line)   |
| `dd`    | Delete current line              |
| `5dd`   | Delete 5 lines                   |
| `dap`   | Delete around paragraph (whole paragraph) |


## Copy & Paste (lines)

| Command | Description                |
|---------|----------------------------|
| `yy`    | Copy (yank) current line   |
| `p`     | Paste after current line   |
| `2yy`   | Copy (yank) 2 lines starting from current    |
| `p`     | Paste copied lines *after* current line      |


## Visual Block (Edit multiple lines)

| Command | Description |
|--------|-------------|
| `Ctrl + v` | Enter **Visual Block** mode to select a vertical block of text |
| `j` / `↓` | Extend the selection down across multiple lines |
| `Shift + i` | Insert text at the beginning of all selected lines |
| `Esc` | Apply the inserted text to every selected line |

**Example workflow**

1. Press `Ctrl + v` to enter Visual Block mode.  
2. Use `j` or `↓` to select multiple lines.  
3. Press `Shift + i`.  
4. Type a comment like `#` or `//`.  
5. Press `Esc` → the text is inserted at the start of all selected lines.


## Search in File 

| Command | Description |
|---------|-------------|
| `:/word` | Search for a word from cursor downward |
| `n`     | Repeat search (next match, downwards) |
| `Shift + n` | Repeat search (previous match, upwards) |

---

### Replace first occurrence of a word (in current line)

| Command | Description |
|---------|-------------|
| `:s/pattern/replace` | Replace first match in current line |

Example:  
`:s/used/LINUX`

---

### Replace all occurrences in current line

| Command | Description |
|---------|-------------|
| `:s/pattern/replace/g` | Replace all matches in the current line |

Example:  
`:s/used/LINUX/g`

---

### Replace all occurrences in the whole file

| Command | Description |
|---------|-------------|
| `:%s/pattern/replace/g` | Replace all matches in the entire file |

Example:  
`:%s/used/LINUX/g`

---

### Replace all with confirmation

| Command | Description |
|---------|-------------|
| `:%s/pattern/replace/gc` | Replace all matches with confirmation (c = confirm) |

Example:  
`:%s/used/LINUX/gc`

---

### Replace all (case‑insensitive)

| Command | Description |
|---------|-------------|
| `:%s/pattern/replace/gi` | Replace all matches, ignore case |
| `:%s/pattern/replace/gic` | Replace all, ignore case + confirm |

Example:  
`:%s/used/LINUX/gi`



## Save the file
###  just save
command line enviroment 
:w = save
:w new name = save az
:w /var/test for give location 
```bash
:w
:w new
: /tmp/tst
```
### save and quit
:wq == ZZ == :x save and quit
:q! == ZQ quit without save
:wq! = save and quit but if have not permissin just quit
```bash
:wq
:q!
:wq!
```
### just reload file 
:e! = before saveing, read the file from disk and reload
```bash
:e!
```

## Tab in vim
### tab
```bash
:tabnew
:tabnext
:tabprevious
:new /PATH/TO/filename
```

## Diff in vim
### diffrence two file
ctrl + ww = switch between files
```bash
vimdiff file1.txt file2.txt
```
### get and put between two files
dependence your cursor location
```bash
vimdiff file1 file2
diffput
diffget
```
## more switch in vim in search
### for disable case sensitive in search vim 
after save and quit all of them be cancel  
:set ic + Enter  
:set noic + Enter = cancel ic and turn to before one  
```bash
:set noic
```
### for high light the word in search
after save and quit all of them be cancel  
:set hls  
:set nohls = cancel hls  
```bash
:set hls
```
### for show number lines in search
after save and quit all of them be cancel  
:set number  
:set nonumber = cancel number  
```bash
:set number
```
## configure your vim (.vimrc)
for saving some configuration in vim:  
```bash
vim .vimrc = vim ~/.vimrc 
:set hls
:set number
```
## install plugin for vim in linux
vim-plug  
https://github.com/junegunn/vim-plug  
for Unix:  
curl -fLo ~/.vim/autoload/plug.vim --create-dirs \  
    https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim  
Usage:
Add a vim-plug section to your ~/.vimrc (or ~/.config/nvim/init.vim for Neovim)

    Begin the section with call plug#begin()
    List the plugins with Plug commands
    End the section with call plug#end()
For example:
call plug#begin()

" List your plugins here
Plug 'tpope/vim-sensible'

call plug#end()
Reload the file or restart Vim, then you can,

    :PlugInstall to install the plugins
    :PlugUpdate to install or update the plugins
    :PlugDiff to review the changes from the last update
    :PlugClean to remove plugins no longer in the list
then:
Open vim environment > :PlugInstall > Enter


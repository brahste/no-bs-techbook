# My Vim and Terminal Commands 

# Terminator

- `Alt-\` - Split terminal vertically
- `Alt--` - Split terminal horizontally
- `Ctrl-Shft-w` - Close current terminal window
- `Crtl-Shft-q` - Close terminal (all windows)

# Vim

## Changing Modes

- `A` - Enter INSERT mode at end of line
- `a` - Enter INSERT mode at end of character
- `I` - Enter INSERT mode at start of line
- `i` - Enter INSERT mode at start of character
- `o` - Enter INSERT mode on new line below
- `O` - Enter INSERT mode on new line above
 
- `v` - Enter VISUAL mode
- `Ctrl-v` - Enter VISUAL BLOCK mode
- `Shft-v` - Enter VISUAL-LINE mode and highlight current line

## Editing Text

- `y` - Yank/copy current selection
- `p` - Paste content at end of character
- `P` - Paste content at beginning of character
- `u` - Undo command
- `Ctrl-r` - Redo command
- `x` - Delete current character
- In VISUAL mode:
    - `u` - Convert all characters to lowercase
    - `U` - Convert all characters to uppercase
    - `~` - Switch captialization of all characters
--- 
- `dw` - Delete word from cursor to end of word
- `diw` - Delete whole word with cursor on any character
- `b` - Go to beggining or word
- `e` - Go to end of word
- `gg` - Go to first line
- `Shft-g` - Go to last line
---
- `/<expression>` - Search current document for `<expression>`

- `:%s/<expression>/<replace>/<option>` - Replaces all occurances of `<expression>` with `<replace>`
    - `<option> = c` - Require confirmation before replacing

## Managing Code

- `gcc` - Comment current line (from `vim-commentary`)
- `gc` - Comment current selection (from `vim-commentary`)
- `gd` - Go to definition (from `Coc`)
- `gy` - Go to type definition (from `Coc`)
- `gi` - Go to implementation (from `Coc`)
- `gr` - Go to reference (from `Coc`)
    - Opens window showing references/occurances of the object
- `Ctrl-o` - Move backwards in the jumplist (useful for exiting go to commands)
- `Ctrl-i` - Move forwards in the jumplist 

---
- `zo` - Open current fold
- `zc` - Close current fold
- `zR` - Open all folds
- `zM` - Close all folds

## Managing Files, Windows, and Tabs

- `F2` - Open tree file explorer (or `:NERDTree`)
- `\ff` - Open _Telescope_ file finder (or `:Telescope file_finder`)
- `\fg` - Open _Telescope_ live grep (or `:Telescope live_grep`) 
---
- `Ctrl-w` - Enter window adjustment mode
    - `s` - Horizontal split
    - `v` - Vertical split
    - `q` - Close active window
    - `w` - Go to next window
    - `j`/`k`/`h`/`l` - Move to window in direction
---
- `:sp` - Splits horizontally
- `:vsp` - Splits vertically
- `:so <file>` - Sources the file


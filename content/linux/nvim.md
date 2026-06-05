---
weight: 4
---
# nvim

## this is NOT even close to complete and is a mess

In Vim, you can jump to a matching parenthesis by pressing the `%` key when your cursor is on an opening or closing parenthesis. This feature works for various types of brackets, including parentheses, square brackets, and curly braces

---
new things i learned from primes course on fem:
open manual docs
```
:h usr<tab>
```

shift I inserts at the beginning

zz centers the page on the cursor

ctrl w then the hjkl for window selection instead of ctrl ww

Vex vertical Ex, Sex slit Ex, or ctrl w s or v

ctrl o to close all other splits, one window

marks are set with the m key then a upper or lowercase letter
	lower case are file specific marks upper case are global marks

ctrl 6 is previous file

ctrl o cicles back the jumplist
	ctrl i forward
	:jumps
	:h jumplist

shift d deletes the line after the cursor, basically d$ 

quickfix list
```vim
:grep <term to serch> **/*.c
```

```
**/** is a hacky way to say search everything? this example is everything that ends in .c
```

```vim
:copen
:cnext
:cprev
:cdo
```

Lua version of get quickfistlist, plugins are easy in lua
`vim.fn.getqflist()`

incremental serch?

:set hls ic
:nohls


find and replace
- :%s/
	- % is whole file
- :s/
	- is single line
- :'<,'>s/
	- is visual region, can hit : for shortcut
- this search and replace searches each line separately
	- /g flag at the end is for global change, default is first match on line only
- `/gc` will step through and ask permission
- you can also do regex
	- research regex capture groups
-

`_` will go to the first nonwhitespace character of the line

`ctrl a` increments a number 9

" is how you access registers
	you can yank into a register
	you can grab the macro register register paste it, edit it, yank it into a register and play it as a macro with @, 

```
"a y
```
In normal and visual modes, "xp pastes the contents of the register x.


---


f and t are similar, t stops short
	, and ; will cycle through the matches
F and T are the same but backwards


```lua
vnoremap J :m '>+1<CR>gv=gv
vnoremap K :m '<-2<CeR>gv=gv
```

```bash
:buffers
```






---

```Bash
# install nvim with kickstart
# https://github.com/nvim-lua/kickstart.nvim
sudo add-apt-repository ppa:neovim-ppa/unstable -y
sudo apt update
sudo apt install make gcc ripgrep unzip git xclip neovim
git clone https://github.com/nvim-lua/kickstart.nvim.git "${XDG_CONFIG_HOME:-$HOME/.config}"/nvim
```

```
sudo apt install make gcc ripgrep unzip git xclip
git clone https://github.com/nvim-lua/kickstart.nvim.git "${XDG_CONFIG_HOME:-$HOME/.config}"/nvim
```

```lua
require('telescope').setup{ 
  defaults = { 
    file_ignore_patterns = { 
      "node_modules" 
    }
  }
}
```

```Lua
vim.keymap.set('i', 'kj', '<ESC>')
vim.keymap.set('n',';', ':')
--vim.keymap.set('n','"','2f"i')
```

```
set filetype=lisp
set filetype=lisp

```

```
set linebreak wrap
```

```
set linebreak nowrap
```


- commenting is not built into neovim
	- highlight the text with shift v
	`gcc`

- sets the cursor to be in the middle of the screen always
	`set scrolloff=999`


`zz` moves current line to middle of the screen
```
-- vertical split
:vsplit

-- increase window
[num] ctrl w >
[num] ctrl w +

-- switch window
ctrl w
```

find and replace
```
:%s/foo/bar/g     # Replace all 'foo' with 'bar'
:%s/\<foo\>/bar/g # Replace only whole word 'foo' with 'bar'
:%s/foo/bar/gi    # Replace all 'foo' with 'bar', ignore case
```
%s but in a visual range
```
    v (or V or ctrl+v) to visually select an area

    :, which then gives me :'<,'>

    and then adding my search command, say I want to replace - with a space only within that range like :'<,'>s/-/ /g (and then hit enter)

```

tricking treesitter to think ejs is html, put this at the top of the file
```
<!-- <!DOCTYPE html> -->
<!-- <html lang="en"> -->
```

vertical bar color
```
	:highlight VertSplit gui=reverse guifg=Black
```

```
And the answer is, the keymap was changed in the recent rewrite from <enter> to <c-y> so ctrl-y to confirm a autocomplete selection. Try if that works.
```

---

In Neovim, recording allows you to save a sequence of commands to a register for later playback, which can help automate repetitive tasks. To start recording, press `q` followed by a letter (a-z) to designate the register, perform your commands, and then press `q` again to stop recording; you can replay the commands using `@` followed by the register letter.

---




go back and write the plugin from primes vim course, would be useful for coverting md vault to html links by exporting the dir ls into the buffer and adding the paths
this line is used to source vim plugins from the init.lua
```
vim.cmd.source(vim.fn.stdpath("config") .. "/plugin.vim")   

```
## set up neovim properly from scratch
- [ ] lsp
	- [ ] markdown_oxide?
	- [ ] codebook?
	- [ ] denols
	- [ ] dprint?
	- [ ] htmx

- [X] highlighting
- [X] autopairs?

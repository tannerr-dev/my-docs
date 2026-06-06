---
title: "nvim"
weight: 4
---
# nvim
---
## source
https://neovim.io/doc/install/
<br>
https://github.com/nvim-lua/kickstart.nvim

---

# Neovim Configuration
readme from my [repo](https://github.com/tannerr-dev/neovim-config).

A single-file Neovim configuration using [lazy.nvim](https://github.com/folke/lazy.nvim) for plugin management. This setup includes fuzzy finding, file tree navigation, syntax highlighting, LSP support, and autocompletion.

---

## Plugins

| Plugin | Purpose |
|--------|---------|
| `tokyonight.nvim` | Colorscheme (currently using `habamax`) |
| `neo-tree.nvim` | File tree explorer |
| `telescope.nvim` | Fuzzy finder for files, grep, buffers, keymaps, etc. |
| `harpoon` | Quick file navigation and bookmarking |
| `which-key.nvim` | Popup showing pending keybinds |
| `todo-comments.nvim` | Highlight TODOs and notes in comments |
| `nvim-highlight-colors` | Show color previews inline |
| `smear-cursor.nvim` | Smooth cursor animation |
| `nvim-autopairs` | Automatically close brackets and quotes |
| `nvim-treesitter` | Syntax highlighting and indentation (archived, see below) |
| `mason.nvim` | Package manager for LSP servers, linters, and formatters |
| `mason-lspconfig.nvim` | Bridge between Mason and nvim-lspconfig |
| `nvim-lspconfig` | Official LSP client configurations |
| `fidget.nvim` | LSP progress UI |
| `lazydev.nvim` | Enhanced Lua LSP for Neovim config development |
| `nvim-cmp` | Autocompletion engine |
| `cmp-nvim-lsp` | LSP completion source for nvim-cmp |
| `cmp-buffer` | Buffer text completion source |
| `cmp-path` | Path completion source |
| `cmp-cmdline` | Command-line completion (`:` and `/`) |
| `LuaSnip` | Snippet engine |
| `friendly-snippets` | VS Code-style snippet collection |

---

## Keymaps

### General

| Key | Action |
|-----|--------|
| `<Space>` | Leader key |
| `;` | Enter command mode (`:`) |
| `<leader>nt` | Toggle Neo-tree file explorer |
| `<leader>p` | Paste without overwriting register (visual mode) |
| `<leader>y` | Yank to system clipboard (visual mode) |
| `<leader>Y` | Yank entire file to system clipboard |
| `J` / `K` | Move selected text down/up (visual mode) |

### Telescope (Search)

| Key | Action |
|-----|--------|
| `<leader>sh` | Search Help |
| `<leader>sk` | Search Keymaps |
| `<leader>sf` | Search Files |
| `<leader>ss` | Search Select (Telescope built-ins) |
| `<leader>sw` | Search current Word |
| `<leader>sg` | Search by Grep |
| `<leader>sd` | Search Diagnostics |
| `<leader>sr` | Search Resume (previous search) |
| `<leader>s.` | Search Recent Files |
| `<leader><leader>` | Find existing buffers |
| `<leader>/` | Fuzzily search in current buffer |
| `<leader>s/` | Live Grep in Open Files |
| `<leader>sn` | Search Neovim config files |

### Harpoon (File Marks)

| Key | Action |
|-----|--------|
| `<leader>h` | Add current file to Harpoon |
| `<C-h>` | Toggle Harpoon quick menu |
| `<C-1>` through `<C-7>` | Jump to Harpoon file 1–7 |
| `<C-S-P>` | Previous Harpoon file |
| `<C-S-N>` | Next Harpoon file |
| `<C-e>` | Open Harpoon window in Telescope |

### LSP (Language Server Protocol)

These keymaps are active when an LSP server is attached to the current buffer.

| Key | Action |
|-----|--------|
| `gd` | Go to Definition |
| `gr` | Find References |
| `gI` | Go to Implementation |
| `<leader>D` | Type Definition |
| `K` | Hover Documentation |
| `<leader>rn` | Rename Symbol |
| `<leader>ca` | Code Action |
| `<leader>f` | Format Buffer (manual) |
| `<leader>ds` | Document Symbols |
| `[d` / `]d` | Jump to previous/next diagnostic |

### Autocomplete (nvim-cmp)

| Key | Action |
|-----|--------|
| `<C-n>` | Next completion item |
| `<C-p>` | Previous completion item |
| `<C-b>` | Scroll documentation up |
| `<C-f>` | Scroll documentation down |
| `<C-y>` | Confirm selection |
| `<C-Space>` | Trigger completion manually |
| `<Tab>` | Expand snippet or jump forward |
| `<S-Tab>` | Jump snippet backward |

---

## LSP Servers

Managed automatically via [Mason](https://github.com/williamboman/mason.nvim). The following servers are configured to auto-install:

| Server | Language |
|--------|----------|
| `pyright` | Python |
| `ts_ls` | JavaScript / TypeScript |
| `gopls` | Go |
| `rust_analyzer` | Rust |
| `clangd` | C / C++ |
| `html` | HTML |
| `cssls` | CSS |
| `lua_ls` | Lua |

### Managing LSP Servers

Open the Mason UI:
```vim
:Mason
```

Install a new server:
```vim
:MasonInstall <server-name>
```

Update all installed packages:
```vim
:MasonUpdate
```

---

## Treesitter Parsers

These parsers are automatically installed on first launch:

- `python`
- `go`
- `javascript`
- `typescript`
- `rust`
- `c`
- `html`
- `css`
- `lua`
- `vim`
- `vimdoc`
- `query`
- `markdown`

Additional parsers for new filetypes are installed automatically (`auto_install = true`).

---

## Treesitter Status & Future Upgrade Path

> **Note:** The [`nvim-treesitter`](https://github.com/nvim-treesitter/nvim-treesitter) plugin repository was archived by its owner on **April 3, 2026** and is now read-only. It is pinned to the `master` branch in this config, which remains stable and functional.

### Why keep it?

- The `master` branch is mature, stable, and continues to work with Neovim 0.12.
- Lazy.nvim installs from archived repositories without issues.
- It provides convenient parser management (`:TSInstall`, `ensure_installed`, `auto_install`) that Neovim does not natively handle.

### Future upgrade paths

When you're ready to move away from the archived plugin, you have two options:

**Option 1: Go fully native (Neovim 0.12+)**
Remove `nvim-treesitter` and use Neovim's built-in treesitter support:
- Highlighting: `vim.treesitter.start()` is built-in.
- Indentation: `vim.bo.indentexpr = "v:lua.vim.treesitter.query.get_indent()"`
- **Trade-off:** You lose automatic parser installation. You must install parsers manually via your OS package manager (e.g., `tree-sitter-lua`) or compile them with `tree-sitter-cli`.

**Option 2: Switch to a community fork**
If a well-maintained community fork emerges, update the plugin spec in `init.lua`:
```lua
{ 'username/nvim-treesitter-fork', branch = 'main', build = ':TSUpdate' }
```

**Option 3: Keep using the archived plugin**
There is no immediate need to change anything. The plugin will continue to work as long as the parsers compile and Neovim's treesitter API remains compatible.

---

## Settings

| Option | Value | Description |
|--------|-------|-------------|
| `relativenumber` | `true` | Relative line numbers |
| `number` | `true` | Absolute line number on current line |
| `scrolloff` | `12` | Keep 12 lines visible above/below cursor |
| `tabstop` / `shiftwidth` / `softtabstop` | `4` | 4-space indentation |
| `expandtab` | `true` | Use spaces instead of tabs |
| `mouse` | `a` | Enable mouse in all modes |
| `termguicolors` | `true` | True color support |
| `clipboard` | `unnamedplus` | Use system clipboard |
| `signcolumn` | `yes` | Always show sign column |
| `cursorline` | `true` | Highlight current line |
| `splitright` / `splitbelow` | `true` | Split windows to right/bottom |
| `undofile` | `true` | Persistent undo history |
| `ignorecase` / `smartcase` | `true` | Case-insensitive search (unless uppercase used) |
| `inccommand` | `split` | Live preview for `:s` substitutions |
| `updatetime` | `250` | Faster completion and diagnostics |
| `timeoutlen` | `300` | Faster which-key popup |
| `showmode` | `false` | Hide mode indicator (shown in statusline) |

---

## Filetype-specific Settings

### `.tmpl` files
HTML comment syntax (`<!-- -->`) is used for comments in `.tmpl` template files.

---

## Installation / Setup

1. **Ensure dependencies are installed:**
   - Neovim 0.12+ (check with `nvim --version`)
   - `git`
   - `make` (for `telescope-fzf-native`)
   - A C compiler (`gcc` or `clang`) for building Treesitter parsers
   - A [Nerd Font](https://www.nerdfonts.com/) for icons (optional but recommended)

2. **Open Neovim:**
   ```bash
   nvim
   ```

3. **Install plugins:**
   ```vim
   :Lazy sync
   ```

4. **Install LSP servers and Treesitter parsers:**
   - LSP servers are installed automatically by Mason on first launch.
   - Treesitter parsers will compile on first startup (may take 10–30 seconds).

5. **Restart Neovim** after everything is installed.

---

## Troubleshooting

### Treesitter parsers failing to build
Make sure you have a C compiler installed:
```bash
# Ubuntu/Debian
sudo apt install build-essential

# macOS
xcode-select --install

# Arch
sudo pacman -S base-devel
```

### LSP server not found
Check if the server is installed via Mason:
```vim
:Mason
```
If missing, install it manually:
```vim
:MasonInstall <server-name>
```

### Colors not showing correctly
Ensure your terminal supports true color and you have a Nerd Font selected.

---

## File Structure

```
~/.config/nvim/
├── init.lua          # Main configuration file (single file setup)
├── lazy-lock.json    # Plugin version lockfile
└── archive/          # Previous config iterations
```

---

## Useful Commands

| Command | Description |
|---------|-------------|
| `:Lazy` | Open lazy.nvim plugin manager UI |
| `:Lazy sync` | Install/update all plugins |
| `:Mason` | Open Mason LSP package manager |
| `:TSUpdate` | Update all Treesitter parsers |
| `:checkhealth` | Run Neovim health check |
| `:LspInfo` | Show active LSP clients for current buffer |
| `:LspRestart` | Restart LSP client for current buffer |
| `:Telescope` | Open Telescope picker |

## my commands and notes

`%`  jump to a matching parenthesis: `[]`,`{}`,`()`

---
new things i learned from primes course on fem:
open manual docs
```
:h usr<tab>
```

- shift I inserts at the beginning


- `zz` centers the page on the cursor

- `ctrl w` then the hjkl for window selection instead of ctrl ww

- `Vex` vertical `Ex`, `Sex` slit `Ex`, or `ctrl w s or v

`ctrl o` to close all other splits, one window

marks are set with the m key then a upper or lowercase letter
	lower case are file specific marks upper case are global marks

ctrl 6 is previous file

`ctrl o` cicles back the jumplist
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

### Install neovim
```
brew install neovim
```

### Lua
This is used to configure nvim. Auto gets loaded as its in /.config/nvim (entire folder auto loads)
1. Create a file at ~./.config/nvim/init.lua


### Lazy Vim
https://lazy.folke.io/installation
This is the package manager that nvim will use for plugins
1. We need to add the following to init.lua
```
local lazypath = vim.fn.stdpath("data") .. "/lazy/lazy.nvim"
if not (vim.uv or vim.loop).fs_stat(lazypath) then
  local lazyrepo = "https://github.com/folke/lazy.nvim.git"
  local out = vim.fn.system({ "git", "clone", "--filter=blob:none", "--branch=stable", lazyrepo, lazypath })
  if vim.v.shell_error ~= 0 then
    vim.api.nvim_echo({
      { "Failed to clone lazy.nvim:\n", "ErrorMsg" },
      { out, "WarningMsg" },
      { "\nPress any key to exit..." },
    }, true, {})
    vim.fn.getchar()
    os.exit(1)
  end
end
vim.opt.rtp:prepend(lazypath)

local plugins = {}
local opts = {}

require("lazy").setup(plugins, opts)
```

2. Install Cappucin (Theme) into local plugins
```
{ "catppuccin/nvim", name = "catppuccin", priority = 1000 }}
```




### Telescope
Enables you to FZF & Grep through files
1. Add to plugins
```
'nvim-telescope/telescope.nvim', tag = '0.1.5',
    dependencies = { 'nvim-lua/plenary.nvim' }
```
2. Initialize Telescope
```
local builtin = require("telescope.buildint")
vim.keympa.set('n', '<C-p>', builtin.find_file, {})
```

I should now be able to hit Ctrl (Cmd on Mac) + P to open up the FZF search while in nvim

### Live Grep
1. Add this global variable
```
vim.g.mapleader = " "
```
2. Add this to init.lua
```
vim.keymap.set('n', '<leader>fg', builtin.live_grep, {})
```

I now will be able to do space + fg to open live grep within nvim


### Tree-Sitter
Used to parse through text and highlight
1. Add this to init.lua plugins
```
  {"nvim-treesitter/nvim-treesitter", build = ":TSUpdate}
```
2. Then add the requirement
```
local config = require("nvim-treesitter.configs")
config.setup({
  ensure_installed = {"lua", "javascript"},
  highlight = { enable = true },
  indent = { enable = true },
})
```


### Neo-tree
This gives you a File Explorer type plugin
REQUIRED: NerdFont as it uses icons
1. Add to plugin:
```
{   
  "nvim-neo-tree/neo-tree.nvim",
  branch = "v3.x",
  dependencies = {
    "nvim-lua/plenary.nvim",
    "nvim-tree/nvim-web-devicons",
    "MunifTanjim/nui.nvim",
  },
}
```
2. Add elsewhere to map 'Ctrl (CMD on Mac) + n' to open file explorer

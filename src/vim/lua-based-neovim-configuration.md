# Lua Based Neovim Configuration

Start with a the file `~/.config/nvim/init.lua`


Key bindings set with `vim.api.nvim_set_keymap({mode}, {keymap}, {mapped_to}, {options})
Use `local keymap = vim.api.nvim_set_keymap`, then just use `keymap(...)`

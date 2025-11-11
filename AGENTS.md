# Agent Guidelines for markdown-toc.nvim

## Build/Test/Lint
- No test suite exists yet (see TODO in README.md)
- No build process required (pure Lua Neovim plugin)
- Manual testing: Load in Neovim with `:luafile lua/mtoc/init.lua`, use `:Mtoc` commands
- Documentation generation: GitHub workflow uses panvimdoc (see .github/workflows/panvimdoc.yml)

## Code Style
- **Language**: Pure Lua (100%), Neovim API focused
- **Module structure**: Use `local M = {}` pattern, return M at end
- **Imports**: Require at top of file with `local name = require('mtoc/submodule')`
- **Types**: Use EmmyLua annotations (`---@class`, `---@field`, `---@param`, `---@return`) - see lua/mtoc/types/mtoc.lua
- **Naming**: snake_case for functions/variables, PascalCase for classes, UPPERCASE for constants
- **API**: Prefer vim.api over vim.fn when possible (e.g., `vim.api.nvim_buf_get_lines`)
- **Error handling**: Use `vim.notify(message, vim.log.levels.ERROR)` for user-facing errors
- **Functions**: Document public functions with EmmyLua, internal helpers can be prefixed with `_`
- **Config**: Deep merge user opts with defaults using `vim.tbl_deep_extend('force', ...)`
- **Line numbers**: Lua 1-indexed, but nvim_buf_* APIs are 0-indexed (be careful with conversions)

## Project Specifics
- Plugin prefix: `mtoc` (not `markdown-toc`)
- Core modules: init.lua (commands/setup), config.lua (options), toc.lua (TOC generation), utils.lua (helpers)
- Fences: HTML comments `<!-- mtoc-start -->` and `<!-- mtoc-end -->` wrap generated TOC
- Link format: GitHub Flavored Markdown by default (see M.link_formatters.gfm in toc.lua)

# Setup

When nvim starts up, it initializes default options, including `runtimepath`. nvim startup automatically runs:

- init.lua
- plugin/**
- after/plugin/**
- ftdetect/**

nvim startup does not automatically load files under `lua/` folders. This happens when a startup file calls a function like

```lua
require("config.options")
```

in this case, lua will search each directory in `runtimepath` and match the first file in the following order:

1. package.loaded["config.options"] - lua packages already loaded
2. ~/.config/nvim/lua/config/options.lua - first path in the `runtimepath`
3. ~/.config/nvim/lua/config/options/init.lua - check init.lua under the config/options/ subdir after confirming config/options.lua doesn't exist
4. etc.

# runtimepath

Similar to the unix env variable `PATH`, `runtimepath` is a list of directories that nvim will search for to define behavior for filetypes, syntax highlighting, indentation, colors, LSP defaults, etc.

## Useful Docs
- General: `:h runtimepath`
- See the set runtimepath: `:set runetimepath?` 

# Runtime directories

Here are the different runtime directories and when they are executed

## Useful Docs
- `:h runtimepath`


# lua/ Directory

This directory should contain all useful lua modules that you want to be loaded on startup, like plugin specs, as well as runtime files (like ftplugin) with configurations that don't need to be applied at the very end of the event. This is different from the [[nvim#after/ Directory|after Directory]], which should only contain runtime files with configurations that need to be applied at the very end of the event.

# after/ Directory

The `after/` directory is part of Neovim's runtimepath system. Files under `after/` are sourced after their counterpart runtime files from the normal runtimepath. 

Use `after/` for late overrides or additions to Neovim runtime behavior, such as filetype-specific settings, plugin tweaks, or native LSP config overrides. 

For more info on type of files in the `after/` directory, see [[nvim#Runtime directories|Runtime directories]].

## Examples
- `after/ftplugin/*.lua`: run buffer-local filetype setup, such as `vim.opt_local` or buffer-local keymaps.
- `after/lsp/*.lua`: return a server config table when using Neovim's native LSP config system.
- `after/plugin/*.lua`: run setup code after normal plugin runtime files have loaded.


# lazy.nvim

lazy.nvim is a modern plugin manager for nvim. It has two main jobs:

1. Install, updated and configure plugins
2. Decide when each plugin should be added to Neovim's path

A plugin 

## Useful Docs:
- Plugin specs: `:h lazy.nvim-🔌-plugin-spec`
- Plugin spec examples: `:h lazy.nvim-🔌-plugin-spec-examples`
- lazy.vim config defaults: `:h lazy.nvim-⚙️-configuration`
- Loading order: `:h lazy.nvim-🚀-usage`
- Profiling & Debugging: `:h lazy.nvim-🚀-usage-⚡-profiling-&-debug`

## Example

A typical Lazy plugin file looks like this:

```lua
return {
    {
        "authors/plugin-name.nvim",
        event = {},
        opts = {
            -- plugin-specific options
        }
    }
}
```

# Useful Tips

Here are tips for using nvim

## Debugging/Troubleshooting

- Documentation: `:h {subject}`, use `<TAB>` to autofill when you can't remember exact names of docs


# Pending Tasks

- [ ] Add a special characters section (e.g. what is <C-s>?)
- [ ] Add a section about folding

# Completed Tasks


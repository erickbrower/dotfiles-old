dotfiles
========

My development environment config for tmux, zsh, and vim.

### Installation

1. `git clone git@github.com:erickbrower/dotfiles.git`

2. `cd dotfiles && rake`

This just installs the VIM plugins and configs. If you'd like to install other configs, check out the other rake tasks:



```
$ rake -T
rake default         # Initializes/updates vim plugins and config files
rake tmux:configure  # Configures tmux
rake vim:configure   # Configures vim with custom rc and bundles
rake vim:init        # Initializes/updates vim bundle plugins
rake zsh:configure   # Configures zsh
```


---
tags:
  - tmux
  - devtool
  - unix
---
similar:: [[fuzzy finder]]
The idea here is the have a script run `find` through to `fzf` then once a directory is selected it will check if a session already exists with that directory name. If yes it will switch the client over to that session. If one does not exist then it will create a new session at that working directory. - [see example](https://github.com/ThePrimeagen/.dotfiles/blob/602019e902634188ab06ea31251c01c1a43d1621/bin/.local/scripts/tmux-sessionizer)

This handles the session creation next is needing to bind this script to a key so that I don't need to type the command to trigger the switch. Along with this I can bind common projects to a key themselves so that I don't have to fuzzy find them.
	Binding the key in `.zsh_profile`
	> `bindkey -s ^f "tmux-sessionizer\n"`

The only thing I have to be away of is that I must connect to tmux before the bindings kick in. If I run `^F` while not in tmux it will fail.

In `.zshrc` I have a bind key where I bind `C-f` to the tmux-sessionizer. Though since this will be called from outside of tmux to start I switched the commend to be `tmux attach-session` so that it will work both within and without tmux.
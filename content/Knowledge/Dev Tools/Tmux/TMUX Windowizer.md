---
tags:
  - tmux
  - unix
  - devtool
---
Things to handle
- [ ] Git worktree binding in vim similar to git files search that allows me to quickly search current worktrees
	- [x] This is reliant upon some vim plugins to make git worktrees integrated into telescope - updated in `after/plugins/telescope.lua` bound to `<leader>gw`
	- [ ] Currently opening the worktree is using the current window instead of using windowizer will need to see how to make it use windowizer
- [x] Added the `tmux-windowizer` script to path in `~/.local/bin/scripts`

The idea behind windowizer is to be able to send commands to a window but have the window persist. If you use `tmux neww` to create new window and run a command the window would close after the command completes.
Parent:: [[i3]]

[[Spotify]] didn't property set the window name until post startup and window mapping. Thus wouldn't be placed correctly sometimes. The solution is to use `for_window` which then allowed me to activate a command when the window changes

`for_window [class="spotify"] move to workspace 1`
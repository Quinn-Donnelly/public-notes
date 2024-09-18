---
tags: []
---
Parent:: [[i3]] [[Dev Tool]]

[Watching guide to get started](https://www.youtube.com/watch?v=77-tuFE_pGc&ab_channel=TheLinuxCast)
in the video he sets up a wall paper using [[nitrogen]]
i think I would like to keep the gnome way I have for now.

trying to get multiple monitors working in i3 - [documentation link](https://i3wm.org/docs/userguide.html#multi_monitor)

Using `apt install arandr` allowed me to run `arandr` and visually arrange the monitors so I don't need to guess positions. This creates a script which I can then run in my config.
The script is in `~/.screenlayout/monitor.sh`

the above worked

next I'd really like to get a background working here but first I will try to get the workspace names to what I want them to be.

[Following the guide here to get gnome working](https://zork.net/~st/jottings/gnome-i3.html)
-- This didn't work

I will now just use [[Nitrogen]] as a package that can manage backgrounds for multiple desktops

The background is working but doesn't load when applications are on that workspace. I might be able to look into people who customize gaps to find out how they set up the background.

[User docs for i3](https://i3wm.org/docs/userguide.html#multi_monitor)
Going to start setting up apps that just auto launch and assign them a workspace.

1. entertainment / music / sound things / [[Discord]] 
2. messaging? - [[Discord]] maybe
3. Web browser
4. terminal / IDE
5. [[Obsidian]] 

for my side monitor i have left a 9 and right as 0. I will likely mostly throw references and maybe some videos that are entertainment there.

I'll try to auto launch the above

The above worked as intended `exec` will only run on start up `exec-always` will run any time even restarts of [[i3]]

I am able to assign workspace to programs using criteria which can map of window properties see `xprop`

Pushed work up will call it an inital setup here main thing I need to fix is the [[i3 doesn't work with transparent background]]
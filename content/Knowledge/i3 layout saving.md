Parent:: [[i3]]
supports:: [[i3 automatically use layout split screen horizontally when on main display]]
# Summary 
The idea is to put the containers where you would like on a workspace and then you can save them to json file and reference them for startup.
# Body
On the [i3 documentation](https://i3wm.org/docs/layout-saving.html) they give the following command
```sh
i3-save-tree --workspace 1 > ~/.i3/workspace-1.json
```

> [!NOTE] Not Useful by default
> The important note is that you have to manually modify the file since they don't know what window attribute to match on for that so they give you the current window's attributes commented out

For editing the layout file see [docs](https://i3wm.org/docs/layout-saving.html#EditingLayoutFiles)
```sh
# From a terminal or script:
i3-msg "workspace 1; append_layout /home/michael/.i3/workspace-1.json"

# In your i3 configuration file, you can autostart i3-msg like this:
# (Note that those lines will quickly become long, so typically you would store
#  them in a script with proper indentation.)
exec --no-startup-id "i3-msg 'workspace 1; append_layout /home/michael/.i3/workspace-1.json'"
```
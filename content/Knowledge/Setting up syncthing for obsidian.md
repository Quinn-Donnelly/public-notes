Parent:: [[Syncthing]]
supports:: [[Obsidian]]

# Summary
[[Syncthing]] will now be an app on my phone as well as a process that [[i3]] starts up on login. This app is configured to sync specified folders of which I have enabled my [[Obsidian Vault]] folder to be synced. This enables two way syncing.

# Body
Download and install [[Syncthing]] on ubuntu using `apt`. Ensure binary is on path in `/usr/bin`. Configured [[i3]] startup command to run `syncthing serve` with some args that allow it to get started.

[[Syncthing]] has a web ui in `localhost:8384` where I add the folders I want to sync. Then I download the andriod app and hit add device. Click show QR on PC then take picture with phone. Configured names. then shared the folder vola.

# References
https://www.youtube.com/watch?v=t3cy132eeUU&ab_channel=DJLensing
https://www.youtube.com/watch?v=6q2W0aPOWbc&ab_channel=DannyTalksTech
https://www.reddit.com/r/ObsidianMD/comments/kw0l91/does_there_exist_selfhosting_solutions/
https://github.com/MaggieAppleton/digital-gardeners
https://docs.syncthing.net/intro/getting-started.html
https://apt.syncthing.net/
https://127.0.0.1:8384/#
https://127.0.0.1:8384/
https://docs.syncthing.net/users/autostart.html#linux
https://docs.syncthing.net/users/config.html
https://forum.syncthing.net/t/reset-user-name-and-password-windows/18935/5
https://localhost:8384/
https://unix.stackexchange.com/questions/256929/autostarting-desktop-application-at-startup-not-working
https://www.google.com/search?channel=fs&client=ubuntu-sn&q=i3+autostart
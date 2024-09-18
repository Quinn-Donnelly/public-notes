---
tags:
  - unix
  - devtool
---
`rm` with undo ability
https://github.com/nivekuil/rip

Installed with Ansible setup. Rip will mv files to the graveyard which by default is `/tmp/graveyard-{user}` there is a `.record` file in the root of the graveyard which will keep a log of deletions. 

Conflicts in the graveyard are resolved by appending a `~<number>` 

`rip` doesn't need the `-r` flag for directories and can undo deletions with `rip -u` which will return the last deleted item. 

`rip -s` lists all deleted files that came from directory. you can then combine this flag with `-u` to undo all deletions in current directory. `rip -su` 
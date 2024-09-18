---
tags:
  - git
---
[[Git]]

[Git worktree documentation](https://git-scm.com/docs/git-worktree)

>This new worktree is called a "linked worktree" as opposed to the "main worktree" prepared by [git-init[1]](https://git-scm.com/docs/git-init) or [git-clone[1]](https://git-scm.com/docs/git-clone). A repository has one main worktree (if it’s not a bare repository) and zero or more linked worktrees. When you are done with a linked worktree, remove it with `git worktree remove`.

Why:
A worktree will allow you to have multiple branches checked out at the same time. 

What:
A worktree is a working tree (the repo at that state in time, commit, ref, etc) along with the metadata which is used to differentiate the working tree in the repo

`git worktree add <path>` will create a new branch whose name is the final component of `<path>` it will be checked out on the file path located at `<path>`. If this folder is ever deleted the management files, metadata, will be retained until either `git worktree remove` or the `gc.worktreePruneExpire` runs which is a time configured in `.gitconfig`. If you would like to prevent pruning of the management files you can do so with the git worktree lock command. Cases where this would be useful is a remote file system or connected device.

The "metadata" files are located in the `.git` directory under the `worktree` sub directory.
## Commands
`add <path> [commit-ish]`
Create a worktree at `<path>` and checkout `<commit-ish>`. Using the 

You can make the worktree [[bare]] with "-" which is same as `@{-1}`

`remove <>`
Will remove the worktree but only if it is `clean` otherwise command will fail unless `-f` was passed

there is also `repair` who's primary usecase is if you move the repo on the filesystem and the worktrees can no longer locate the main worktree repair will use the main worktree to re-establish connection to linked worktrees.

# Conclusion
Having the different branches on separate file system paths will allow my untracked build tool files to not compete with one another when two branches are standing in opposition, *I'm looking at you `node_modules`*. This will allow me to jump around different work items folks want me to look out without worrying about `git stash`.
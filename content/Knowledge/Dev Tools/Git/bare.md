---
tags:
  - git
  - devtool
---
[Bare Guide](https://www.theserverside.com/blog/Coffee-Talk-Java-News-Stories-and-Opinions/What-is-a-bare-git-repository)

A bare repo will not have `index`, `logs`, `refs`, `COMMIT_EDITMG` it will only have the other files for the management of the git repo.

I disagree with the statement here about `bare` repos not being used for local development. I think the bare repo might be a good use case as a main folder for you to then do development in directories using git worktrees.

Initializing a bare repo will give a file structure like the following image![[Pasted image 20231216003248.png]] Currently there is no remote configured for that repo. I'll point to a new repository in github and test the interactions.

Adding a remote works the same way as a repo with a main worktree created through normal `git init`

It seems like the common pattern of using a bare repo is hooking up to one that already exists since currently my bare repo doesn't have a commit thus `HEAD` is unset and can't create a work tree off of it. Although due to my default settings `HEAD` is set to `refs/heads/trunk` and that ref doesn't exist.

Creating the remote repo and having the a commit on it allowed me to `git fetch <remote>` then using `git worktree add trunk origin/trunk` set up a worktree that would be checked out to that branch without upstream configured.

The child worktree is aware of the parent if you are in the child and run `git worktree list` you will see the parent listed.
![[Pasted image 20231216005405.png]]

Creating a new branch locally named trunk allowed my bare repos ref to point to an actual commit since my default points to the trunk ref and now trunk is resolvable.

Then doing a `git worktree add <path>` allowed a new worktree to be created
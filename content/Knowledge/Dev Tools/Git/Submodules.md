---
tags:
  - git
---
To add a submodule run `git submodule add <repo link>` this will by default add it to a folder matching the repo link's name. 

When cloning a project that uses submodules you will need to run two commands `git submodules init` and `git submodules update` which will setup the local submodules config and pull the slubmodule info respectively. If using `git clone` you can add `--recurrsive-submodules` to have it do those steps for you.
>git submodule update --init --recursive

this command combo is fool proof as it will init and update and handle any further submodules when pulled.

Status of the submodules internal directory will be the commit the parent points to you can also use `git submodule update --remote` to get updates from the remote without moving to that directory. See [Gotcha](#Gotcha) for a quirk with `git pull`.
## Good note on managing others configs with submodules
This command will by default assume that you want to update the checkout to the default branch of the remote submodule repository (the one pointed to by `HEAD` on the remote). You can, however, set this to something different if you want. For example, if you want to have the `DbConnector` submodule track that repository’s “stable” branch, you can set it in either your `.gitmodules` file (so everyone else also tracks it), or just in your local `.git/config` file. Let’s set it in the `.gitmodules` file:

```console
$ git config -f .gitmodules submodule.DbConnector.branch stable

$ git submodule update --remote
remote: Counting objects: 4, done.
remote: Compressing objects: 100% (2/2), done.
remote: Total 4 (delta 2), reused 4 (delta 2)
Unpacking objects: 100% (4/4), done.
From https://github.com/chaconinc/DbConnector
   27cf5d3..c87d55d  stable -> origin/stable
Submodule path 'DbConnector': checked out 'c87d55d4c6d4b05ee34fbc8cb6f7bf4585ae6687'
```

If you leave off the `-f .gitmodules` it will only make the change for you, but it probably makes more sense to track that information with the repository so everyone else does as well.

## Settings recommended
```console
git config status.submodulesummary 1
```
this will allow `git status` to give you some info about changes to submodules

```console
On branch master
Your branch is up-to-date with 'origin/master'.

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

	modified:   .gitmodules
	modified:   DbConnector (new commits)

Submodules changed but not updated:

* DbConnector c3f01dc...c87d55d (4):
  > catch non-null terminated lines
```

Here are some aliases that might be useful as well
```console
$ git config alias.sdiff '!'"git diff && git submodule foreach 'git diff'"
$ git config alias.spush 'push --recurse-submodules=on-demand'
$ git config alias.supdate 'submodule update --remote --merge'
```
## Gotcha
The state of the submodules is the directory but if you pull it will not update the status of the submodules to finish checking in the changes you will need to run `git submodule update` just using `git pull` will not be enough to get the updates pushed.

When you wish to update a repo's submodule don't forget to go to the commit for the submodule then go to the parent and `git add` then you run `git submodule update` if you run update first it will just jump back to the original SHA for that submodule.
## Working on a submodule
The submodule will be pulled and each update will have it in a detached head state so to be able to work on it you would need to have a branch checked out which will then be reset each time you update unless you specify the `--merge` or `--rebase` flags.
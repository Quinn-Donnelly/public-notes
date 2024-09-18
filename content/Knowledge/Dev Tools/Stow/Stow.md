---
tags:
  - unix
  - devtool
---
Dotfile management using stow
https://github.com/ThePrimeagen/dev-productivity/blob/main/lessons/dotfile-management.md

A tool to set up symlinks on a machine called a symlink farm manager.

[Stow](https://www.gnu.org/software/stow/manual/stow.html#Introduction)

## Terminology

A _package_ is a related collection of files and directories that you wish to administer as a unit — e.g., Perl or Emacs — and that needs to be installed in a particular directory structure — e.g., with bin, lib, and man subdirectories.

A _target directory_ is the root of a tree in which one or more packages wish to _appear_ to be installed. A common, but by no means the only such location is /usr/local. The examples in this manual will use /usr/local as the target directory.

A _stow directory_ is the root of a tree containing separate packages in private subtrees. When Stow runs, it uses the current directory as the default stow directory. The examples in this manual will use /usr/local/stow as the stow directory, so that individual packages will be, for example, /usr/local/stow/perl and /usr/local/stow/emacs.

An _installation image_ is the layout of files and directories required by a package, relative to the target directory. Thus, the installation image for Perl includes: a bin directory containing perl and a2p (among others); an info directory containing Texinfo documentation; a lib/perl directory containing Perl libraries; and a man/man1 directory containing man pages.

A _package directory_ is the root of a tree containing the installation image for a particular package. Each package directory must reside in a stow directory — e.g., the package directory /usr/local/stow/perl must reside in the stow directory /usr/local/stow. The _name_ of a package is the name of its directory within the stow directory — e.g., perl.

Thus, the Perl executable might reside in /usr/local/stow/perl/bin/perl, where /usr/local is the target directory, /usr/local/stow is the stow directory, /usr/local/stow/perl is the package directory, and bin/perl within is part of the installation image.

A _symlink_ is a symbolic link. A symlink can be _relative_ or _absolute_. An absolute symlink names a full path; that is, one starting from /. A relative symlink names a relative path; that is, one not starting from /. The target of a relative symlink is computed starting from the symlink’s own directory. Stow only creates relative symlinks.


## Testing
Stow will default the stow directory to the current dir and the target as the parent of the current. For this reason many people have the dotfile repo in their home dir so that the defaults will work as is and no flags need to be passed. I would personally prefer my setup of 
`$HOME/git/dotfiles` -> this will be the Ansible + stow directory *Still need to think if I want them to be the same repo or separate repo*
`$HOME` and `$HOME/.config` will contain most of the targets thus `$HOME` will be target directory.

Running `stow -t $HOME <package>` will work but since I will share this repo with ansible and stow I will likely have the stow dir nested in the repo. So the command would be the following if the current directory is the base of the repo. 
`stow -t $HOME -d dotfiles/`
this would then stow my dotfiles
/ <git repo>
	.git
	<ansible setup tbd on structure>
	/dotfiles
		/zsh
			.zshrc
			.zsh_profile
		fonts/
			/.config
				/fonts

Helpful note that using the `-vv` and `--simulate` you can test out the affect stow would have if run without making modifications.
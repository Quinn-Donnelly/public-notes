---
tags:
  - devtool
  - automate-setup
---
Looking into [[Ansible]] as a tool that will manage my downloads and setup process. The ideal state is that I can get onto one computer download my setup script or something then just fire away. Everything from there is automated.

- [x] Will [[Ansible]] be able to solve the orchestration problem
	- [x] Installation of software and tooling
		- [x] git - *Might already be installed since I will likely source this setup from git*
		- [x] various command line tools
		- [x] obsidian
		- [x] browser
		- [x] stow setup - *If stow solves the dotfile management issue*
		- [x] ubuntu setup specific tasks
		- [x] windows setup specific tasks
		- [x] mac setup specific tasks
		- [x] Will I be able to have a work setup and personal set up that play nice
- [x] Will [[Dev Tools/To be looked at/Stow|Stow]] be able to solve the script and dotfiles setup
	- [x] will I be able to have work and personal specific configs for stow
		- [x] scripts for work that are sourced from one repo and scripts for personal that are sourced from another - *likely going to pull submodules here*
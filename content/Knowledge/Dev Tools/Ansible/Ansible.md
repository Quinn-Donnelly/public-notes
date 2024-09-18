---
tags:
  - devtool
---
# Learning Log
Going to walk through this tutorial to get feet wet - [Tutorial]()

## Tutorial
- Don't believe what the internet tells you I don't need to manage `pip` installs I can manage through `apt` 
  
```bash
sudo apt update
sudo apt install software-properties-common
sudo add-apt-repository --yes --update ppa:ansible/ansible
sudo apt install ansible
```

If I have to do the above just to run my local setup then we are certainly deviating from one click. I would need to have a script that sets up the download of Ansible which will be different for each OS I use.

on to the demo

```text
├── inventory -------------> Mapping of hostname to group name
├── roles
│   ├── development
│   │   ├── files
│   │   │   └── tmux.conf -> A file used by the role
│   │   └── tasks
│   │       └── main.yml --> Tasks for the role development
└── site.yml --------------> Mapping of group name to role
```

- `inventory` maps hostname (in our case localhost), with a group name (in our case `laptop`)
- `site.yml` maps group names (laptop here) to roles (here we have one role: development.
- `roles/development` is a role, it defines the actual operations that Ansible will run 

As we said the `inventory` maps hostnames to group names. Update the content of `inventory` with:

```text
[laptop]
localhost
```

This means that we declare a group "laptop" that contains one host: "localhost".

Next let's look at the main entry point: `site.yml`, it maps group names to roles and is called a `playbook`. Update the content of `site.yml` to associate the group `laptop` with the role `development` :

```yaml
- hosts: laptop
  roles:
    - development
```

Finally let's add some code to `main.yml` at `roles/development/main.yml` to write `Hello ansible` to the file `/tmp/log` :

```yaml
- name: Hello ansible
  shell: echo "Hello ansible" >> /tmp/log
```

You can run this playbook with:

```shell
ansible-playbook -i inventory site.yml -c local
```

`-c local` tells Ansible not to try to connect through ssh but rather run the playbook (site.yml) locally.

The run should have created a file `/tmp/log` containing `Hello ansible`.

The above worked and created the log file I get the rough structure. I'm currently thinking inventory is my OS setups / personal / work :thinking: then my groups are the tasks that are needed for each of those, windows doesn't need Intellij but my mac and Ubuntu will etc. so then a task would be setting up code editors which would apply to the development machine group which applies to the personal Ubuntu host or something like that. 

Next part of the tutorial uses `homebrew` to install packages I don't think I'm interested I may see if I can do the same with `apt` since I'm on my ubuntu machine currently.

Based on ignoring [this entire manual page](https://docs.ansible.com/ansible/latest/collections/ansible/builtin/apt_module.html) and scrolling to the example it seems `apt` is built in and can be done many ways. This one peaks my interest
```
- name: Install a list of packages
  ansible.builtin.apt:
    pkg:
    - foo
    - foo-tools
```

I set it to install `git` given I already installed `git` I was curious what would happen. 
![[Pasted image 20231220020225.png]]
Much stateful such wow.

Ok so now for some tooling already setup on this computer to start working backwards from where I am so that I have an ansible script that would set up my computer as it currently is.

tutorial? - *what tutorial*

Obsidian is sourced from `snap` based on [docs](https://docs.ansible.com/ansible/latest/collections/community/general/snap_module.html) it was a module but not already built in. It seems I need to run a command - `ansible-galaxy collection install community.general` this will also need to be added to whatever glue script I make to manage my local machine setup ansible so that Ansible can setup machine. :thinking: once again wondering if I can't just bash this to death with a little `stow` action. But stateful is nice we shall see.

I ran the install commnad above and Ansible tells me I already have it so maybe I don't need to worry about the above.

Once again stateful cool ![[Pasted image 20231220021029.png]]
Now I am taking notes in Obsidian so I won't uninstall that but I will check what happens if I uninstall `git` and run again
![[Pasted image 20231220021201.png]]
The first casualty in the war of config management. Knowing nothing of ansible I'm going to take a blind guess on process management and assume that it is using my sessions permissions to preform it's actions when I specify the `--local` flag. Given I didn't run Ansible with root-ish permissions I don't think it would be able install. I will rerun with `sudo`

Bingo pass go collect 200 dollars
![[Pasted image 20231220021524.png]]
Weird error on my first sudo run the file in the tutorial failed to create I think because technically running as a diff user it didn't want to change permissions or something maybe a flag on that task would have had to been specified. unsure deleted file ran again worked moving on. I do not plan on doing much in the way of changing users for my setup it will all need to be permission-ed to install things though `stow` will def need to create under my user permissions and not root so maybe I'll care later but not now.

`neovim` added with absolutely no pain. This is going well. On to something more challenging like my terminal set up. Lets get some `zsh` action.

Looks like the whole permission thing / switching user will come back to bite me here but lets find out. Installing `zsh` is easy that's an `apt` like others I've already done but configuring the shell for a user is either a direct write to a file or running `` 
I'll just execute command it's idempotent anyway.

There seems to be a pattern of using `become` and `become_user` that will control how a task is run. I think the default of `become: true` is to become root user. I will try to change install commands to `become:true` and have my command not sudo anymore.

`become: true` does in fact change that task to root though I am failing to change my default shell. Maybe user doesn't have permission to do that and it's a root operation since it does basically modify the `/etc/passwd` file which is owned by root. I will change to run as root and specify the user. Based on reading docs `ansible_user_id` holds the user that ran the ansible command but only if `gather_facets` is true for that playbook, it is true by default so I should have it. Note Ansible syntax for variable is {{ }}. That worked.

now setting up oh-my-zsh which I also need to install some fonts I could likely do some fancy Ansible here but for now just cmd with wget and stuff and chaining commands quick and dirty refactor later if it's actually an issue.

oh-my-zsh will fail on reruns since the `.oh-my-zsh` dir already exists. Ansible can aparently use a `creates` command to track what it creates file wise and only run that task if that file or dir doesn't exist. Will try much excite. creates goes under the task under `args`

loose testing of it with the dir existing and not existing seems to indicate that it is in fact working.

interesting note that for `become: true` to work the session would have already needed to have root password / already have sudo once before so that the session can auth as root. You can send `--ask-become-pass` and Ansible will prompt you for the password instead of failing out.

For now that will conclude my search of ansible

Things to do next 
- [x] check out stow
	- [x] get stow to handle .zshrc and .zsh_profile
	- [x] get stow to handle my bash scripts
- [ ] Find a way to automate gpg keys for github as well as access token creation
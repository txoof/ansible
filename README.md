# Ansible Playbooks

## Quick Start

Run one of the playbooks against a host:
`$ ansible-playbook basic_install.yml -i hosts -e host=raspberrypi.local`

### Explanation:
`-i` Inventory file that contains all known hosts (update as needed)
`-e, --extra-var` Specify extra variables that will be used when running playbook
`host=host-name.whatever` Specify the hostname to run against

## Play Books

**rpi_basic_install**
Basic setup of a raspberry pi

Command: `ansible-playbook rpi_basic_install.yml -i hosts -e host=rasbperrypi.local --ask-pass`

### Tasks Executed

* install local public ssh key on remote
* update apt cache
* upgrade apt packages
* install apt:
  - tmux
  - vim
  - git
  - python3
  - python3-pip
  - zsh
* install python packages:
  - dotfiles
* create a public/private keypair
* prompt user to add deploy key to git repo for ssh keys
* scan and register keys from github
* clone dotfiles repo
* set shell to zsh
* clone oh-my-zh repo
* configure dotfiles
* link dotfiles



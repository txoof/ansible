# Ansible Playbooks

## Quick Start

Run one of the playbooks against a host:
`$ ansible-playbook basic_install.yml -i hosts -e host=raspberrypi.local`

### Explanation:
`-i` Inventory file that contains all known hosts (update as needed)
`-e, --extra-var` Specify extra variables that will be used when running playbook
`host=host-name.whatever` Specify the hostname to run against

## Rasperry Pi Play Books
### rpi_000_wifi_ssh_setup.yml**
Setup wifi and ssh when writing a new image.
`$ ansible-playbook rpi_wifi_ssh_setup.yml -i hosts -e host=localhost`

#### Tasks Executed:

  * collect SSID name
  * collect WPA key
  * collect country code
  * create network block and set country code


### rpi_001_basic_install
Basic setup of a raspberry pi

This playbook requires `sshpass` is installed

Command: `ansible-playbook --ask-pass rpi_001_basic_install.yml -i hosts -e host=raspberrypi.local`

#### Tasks Executed

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

### rpi_002_hifi_berry

Setup HiFi Berry Cards

Command: `ansible-playbook rpi_hifi_berry.yml -i hosts -e host=newpi`

#### Tasks Executed

  * find any attached HiFi Berry devices
  * ask user to install hifiberry device
  * add hifiberry device to /boot/config.txt
  * set force_eeprom_read=0 when kernel version is >= 5.4
  * reboot
  * check for hifiberry card in aplay output

### rpi_003_check_hifiberry
verify hifi berry is installed properly

#### Tasks Executed

  * check card is installed and loaded properly


### rpi_004_audio_applications
install audio applications

#### Tasks Completed

  * install raspotify and rename display name
  * install squeezelite

### rpi_005_rename_host

#### Tasks Completed
  * change host name
  * reboot

### rpi_development_environment
Setup basic development environment

#### Tasks Executed
  * update apt cache
  * upgrade any apt packages
  * install development & GPIO packages 
    - tmux, vim, git, p ython3, python3-pip, zsh, python3-gpiozero
  * install numpy dependencies from apt
    - python3-numpy, libopenjp2, libtiff5, libatlas-base-dev
  * install jupyter packages
    - jupyter, jupyterthemes
  * update numpy from PyPi (takes care of version incompatability issues)
  * clones development tools from github

### rpi_jivelite
Install jivelite and configure for R. Pi touch screen

#### Tasks Executed
  * update cache
  * install squeezelite and dependencies for building jivelite
  * install luajit
  * setup build environment
  * clone jivelite repo
  * make, build and install jivelite
  * create launch scripts 
  * add X menu items
  * configure X menus to accomodate JiveLite in psuedo full-screen mode on Rasberry pi
 
### rpi_jupyter
Install jupyter and pipenv

#### Tasks Excuted
* Pip install
 - Jupyter
 - pipenv
 
### rpi_led_control
Turn off status lights

#### Tasks Executed
* set LEDs to off in `/boot/config.txt`
* Copy led_ctl script
* Create & install led_ctl unit file for systemctl
* switch off LEDs

### rpi_shtudown_button
set up a shut down/power on switch

This is specifically designed for a three position momentary toggle switch with a common pole. Connect the common pole to ground (physical pin 6) and positon A to physical pin 11 (GPIO-17) for shutdown and position B to physical pin 5 (GPIO-3) wake from shtudown.

#### Tasks Executed
* add line to `/boot/config.txt`

### rpi_spi_on
Enable SPI

#### Tasks Executed
* set spi on in `/boot/config.txt`
* remove spi from blacklist
* reboot

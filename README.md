# Arch Linux Package Installation with Ansible

This repository contains multiple Ansible playbooks to automate installation of essential packages and other utilities on a fresh Arch Linux system.

## Prerequisites
Before running this playbook, ensure you have run the following steps:
1. CPU microcode updates
```bash
# run as root
# on AMD systems
pacman -S amd-ucode

# on Intel systems
pacman -S intel-ucode
```
2. The following utilities installed on your system
> Restart the system after this step
```bash
# run as root
pacman -S linux-firmware man sudo nvim git openssh networkmanager reflector zsh
reboot
```
3. Update mirror list
```bash
# run as root
reflector -c India --sort rate > /etc/pacman.d/mirrorlist
```
4. Create a user
```bash
# run as root
useradd -m -G wheel -s /usr/bin/zsh vijay

# set a password
passwd vijay
```
5. Switch to the newly created user
```bash
su vijay
```

6. Install Ansible
```bash
sudo pacman -S ansible
```

7. Clone this repository
```bash
git clone git@github.com:vijayboopathy/arch-setup.git
cd arch-setup
```
8. Install the required Ansible collections
```bash
ansible-galaxy collection install community.general
ansible-galaxy collection install -r requirements.yml
```


## Install the core packages
These packages can be installed on all the systems irrespective of their processor(`x86_64` only), DE preferences, etc.,
```bash
ansible-playbook core-packages.yml
```

## Install Hyperland packages
1. If you have Nvidia graphics card installed in your system, then it is [recommended](https://update.link) to install the following packages.
```bash
sudo pacman -S nvidia-dkms nvidia-utils egl-wayland
```
2. Install Hyprland packages
```bash
ansible-playbook hyprland-packages.yml
```

## Install application packages
```bash
ansible-playbook application-packages.yml
```

## Dotfiles set up
1. Clone the dotfiles repo
```bash
git clone https://github.com/vijayboopathy/dotfiles.git
cd dotfiles
```
2. Stow Hyprland cofigurations
```bash
# --no-folding option creates directories, if they don't exist
stow --no-folding -vt ~ hypr
```
3. Stow Neovim configurations
```bash
stow --no-folding -vt ~ nvim
```
4. Stow Starship configurations
```bash
stow --no-folding -vt ~ starship
```
5. Stow Ghostty configurations
```bash
stow --no-folding -vt ~ ghostty
```
6. Stow Atuin configurations
```bash
stow --no-folding -vt ~ atuin
```
7. Stow Solaar configurations
```bash
stow --no-folding -vt ~ solaar
```
8. Stow Yazi configurations
```bash
stow --no-folding -vt ~ yazi
```

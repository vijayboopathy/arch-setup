# Arch Linux Package Installation with Ansible

This repository contains an Ansible playbook to automate the installation of essential packages on a fresh Arch Linux system.

## Prerequisites

Before running this playbook, ensure you have:

1. **Ansible installed** on your Arch Linux system:
   ```bash
   sudo pacman -S ansible
   ```

2. **Install the required Ansible collection**:
   ```bash
   ansible-galaxy collection install community.general
   ansible-galaxy collection install -r requirements.yml
   ```

3. **Root or sudo access** to install packages

4. **Internet connection** to download packages from the Arch repositories

## Packages to be Installed

The playbook installs the following packages, organized by category:

### System Packages
- `networkmanager` - Network connection manager
- `sudo` - Privilege escalation tool
- `which` - Command location utility
- `vim` - Text editor

### Desktop Environment
- `plasma-meta` - KDE Plasma desktop environment
- `sddm` - Simple Desktop Display Manager
- `sddm-kcm` - KDE Control Module for SDDM
- `qt5-declarative` - Qt5 declarative components

### Graphics
- `nvidia-open` - Open-source NVIDIA drivers

### Applications
- `kitty` - GPU-accelerated terminal emulator
- `firefox` - Web browser

### Bluetooth
- `bluez` - Bluetooth protocol stack
- `bluez-utils` - Bluetooth utilities

### Development & Package Management
- `flatpak` - Application sandboxing and distribution framework
- `python-pip` - Python package installer
- `python-ansible` - Ansible Python package

## Usage

### 1. Run the Playbook

Execute the playbook with:

```bash
ansible-playbook install-packages.yml
```

### 2. Run with Verbose Output (Recommended)

For detailed output and better debugging:

```bash
ansible-playbook install-packages.yml -v
```

### 3. Run with Extra Verbosity

For maximum detail:

```bash
ansible-playbook install-packages.yml -vvv
```

## What the Playbook Does

1. **Updates the package database** using `pacman -Sy`
2. **Installs packages in logical groups** to ensure dependencies are met
3. **Enables and starts essential services**:
   - NetworkManager (network management)
   - SDDM (display manager)
   - Bluetooth service
4. **Provides a summary** of installed packages and next steps

## Post-Installation Steps

After running the playbook, consider these additional steps:

### 1. Reboot the System
```bash
sudo reboot
```

### 2. Configure NetworkManager
```bash
nmtui  # Text-based network configuration
# or
nm-connection-editor  # GUI network configuration
```

### 3. Configure SDDM (if needed)
```bash
sudo systemctl enable sddm
sudo systemctl start sddm
```

### 4. Set up Bluetooth
```bash
bluetoothctl
# Follow the interactive prompts to pair devices
```

### 5. Install Flatpak Applications
```bash
flatpak install flathub org.mozilla.firefox
flatpak install flathub org.gnome.Software
```

## Troubleshooting

### Common Issues

1. **Package conflicts**: If you encounter package conflicts, try running:
   ```bash
   sudo pacman -Syu
   ```

2. **Missing dependencies**: If some packages fail to install, check for missing dependencies:
   ```bash
   sudo pacman -S --needed base-devel
   ```

3. **Service startup issues**: If services don't start properly, check their status:
   ```bash
   sudo systemctl status NetworkManager
   sudo systemctl status sddm
   sudo systemctl status bluetooth
   ```

### Logs and Debugging

- Check Ansible logs for detailed error messages
- Review system logs: `journalctl -xe`
- Check package installation logs: `pacman -Q`

## Customization

To modify the package list:

1. Edit the `vars` section in `install-packages.yml`
2. Add or remove packages from the appropriate category lists
3. Run the playbook again

## Security Notes

- This playbook requires root privileges to install system packages
- Review the package list before running to ensure it meets your security requirements
- Consider using a more restrictive sudo configuration after installation

## License

This playbook is provided as-is for educational and automation purposes. Use at your own risk and always review the packages being installed. 

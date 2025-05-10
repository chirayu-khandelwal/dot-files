# 🛠️ System Setup Guide (Post-Distro Reset)

A comprehensive guide to reconfigure your Linux system after a fresh install or reset. Tested on Debian/Ubuntu-based distributions.

---

## 🐟 Shell Setup (Fish)

```bash
sudo apt update
sudo apt install fish -y

# Add Fish to valid shells
echo /usr/bin/fish | sudo tee -a /etc/shells

# Set Fish as default shell
chsh -s /usr/bin/fish
````

---

## 🎨 Desktop & GNOME Configuration

### Install GNOME Tweaks

```bash
sudo apt install gnome-tweaks -y
```

### Load/Save GNOME Settings

```bash
# Dump current settings
dconf dump / > gnome-desktop.conf

# Load from file
dconf load / < gnome-desktop.conf

# Reset GNOME settings
dconf reset -f /
dconf reset -f /org/gnome/
```

---

## 🧰 System Tools & Utilities

### Install Essential Tools

```bash
sudo apt install btop gparted neovim unzip -y
sudo apt install git fastfetch -y
```

### Alternative fetch utility

```bash
sudo add-apt-repository ppa:zhangsongcui3371/fastfetch
sudo apt update
sudo apt install fastfetch-cli
```

---

## 🎛️ File Manager (Set Nemo as Default)

```bash
sudo apt install nemo -y
xdg-mime default nemo.desktop inode/directory application/x-gnome-saved-search
xdg-settings set default-web-file-manager nemo.desktop
gsettings set org.nemo.desktop show-desktop-icons true
gsettings set org.gnome.desktop.background show-desktop-icons false
```

---

## 🎙️ OBS Studio Installation

```bash
sudo add-apt-repository ppa:obsproject/obs-studio
sudo apt update
sudo apt install obs-studio -y
```

---

## 🧪 Package Managers & Dev Tools

### Bun

```bash
curl -fsSL https://bun.sh/install | bash
```

### Rust

```bash
sudo apt install rustc -y
```

---

## 🎵 Spotify + Spicetify Theme Setup

```bash
# Install Spotify
curl -sS https://download.spotify.com/debian/pubkey_C85668DF69375001.gpg | sudo gpg --dearmor -o /etc/apt/trusted.gpg.d/spotify.gpg
echo "deb http://repository.spotify.com stable non-free" | sudo tee /etc/apt/sources.list.d/spotify.list
sudo apt update
sudo apt install spotify-client -y

# Install Spicetify
curl -fsSL https://raw.githubusercontent.com/spicetify/cli/main/install.sh | sh

# Apply Spicetify configuration
spicetify config prefs_path ~/.var/app/com.spotify.Client/config/spotify/prefs
spicetify apply
```

---

## 📋 Espanso (Text Expander)

```bash
wget https://github.com/espanso/espanso/releases/download/v2.2.1/espanso-debian-x11-amd64.deb
sudo apt install ./espanso-debian-x11-amd64.deb
espanso service register
espanso start
```

---

## 🖱️ Mouse & Input Configs

```bash
xinput list
xinput set-prop <device-id> "libinput Scroll Method Enabled" 0 0 1
xinput set-prop <device-id> "libinput Middle Emulation Enabled" 1
dconf write /org/gnome/desktop/peripherals/mouse/middle-click-emulation true
```

---

## 🧽 System Cleanup & Optimization

```bash
sudo systemctl disable fwupd.service
sudo systemctl disable gpu-manager.service
sudo systemctl disable postgresql@14-main.service
sudo systemctl disable mysql.service
sudo systemctl disable NetworkManager-wait-online.service
sudo apt remove plymouth -y
sudo systemctl mask plymouth-quit-wait.service
```

### Analyze Boot Performance

```bash
systemd-analyze blame
```

---

## 🌐 Browser Installs

### Brave Browser

```bash
curl -fsS https://dl.brave.com/install.sh | sh
```

### Floorp Browser

```bash
curl -fsSL https://ppa.floorp.app/KEY.gpg | sudo gpg --dearmor -o /usr/share/keyrings/Floorp.gpg
sudo curl -sS --compressed -o /etc/apt/sources.list.d/Floorp.list 'https://ppa.floorp.app/Floorp.list'
sudo apt update
sudo apt install floorp -y
```

---

## 💻 Bootloader Fix (Optional - Dual Boot)

```bash
sudo mount /dev/nvme0n1p4 /mnt
sudo cp -ax /mnt/EFI/Microsoft /boot/efi/EFI
sudo os-prober
```

---

## 🧪 Optional Tools

```bash
sudo apt install topgrade -y
topgrade
```

# My quick-start archlinux installation workflow

# NOT TESTED!

Clone this repository and run commands in the project root directory.

1. First, sync mirrors and install Ansible with dependencies

```shell
sudo pacman -Syy python-passlib ansible
```

2. Second, install and update the submodules, check carefully group_vars/all file (configuration).

```shell
git submodule init && git submodule update
```

3. Run the playbook as root (playbooks will use group_vars/all configuration, including username).

```shell
# install core
sudo ansible-playbook -i localhost playbook.yaml --tags="base,gnupg,ssh"

# import gpg key
gpg --import ../gpg.asc
rm ../gpg.asc

# Add key to sshcontrol
gpg --list-keys --with-keygrip
# find key under pub section Keygrip = ...
echo '123....' >> ~/.gnupg/sshcontrol

# Enable SSH_AGENT_PID
unset SSH_AGENT_PID
if [ "${gnupg_SSH_AUTH_SOCK_by:-0}" -ne $$ ]; then
  export SSH_AUTH_SOCK="$(gpgconf --list-dirs agent-ssh-socket)"
fi

# Install dotfiles
```shell
git clone https://github.com/inomoz/dotfiles ~/Projects/dotfiles/
cd ~/Projects/suckless/
git log

# Make symlinks using gnu stow
stow --target=/home/inom */
```

# Install & configure suckless software
```shell
mkdir -p ~/Projects/suckless/
cd ~/Projects/suckless/
git clone https://github.com/inomoz/dwm
git clone https://github.com/inomoz/st
git clone https://github.com/inomoz/dwmblocks

cd dwm
makepkg -fsri

cd ../st
makepkg -fsri

cd ../dwmblocks
make
sudo make install
```

# Install other packages
sudo ansible-playbook -i localhost playbook.yaml --skip-tags="base,gnupg,ssh"
```

4. It's recommended to remove imported gpg key and reboot, to validate the installation.

```shell
reboot
```

# Info

some directories are preconfigured, you can change them if you want
for example in user.yml "/mnt/var/" used as prefix for logs

# Special thanks

- https://github.com/pigmonkey/spark

# TODO

- systemd... resolv.... ntp
- user ssh key info
- validate systemd enabled services, like reflector
- https://habr.com/ru/post/479540/
- https://venthur.de/2021-12-19-managing-dotfiles-with-stow.html

# Manual tests

ArchLinux 5.18.16-arch1-1

Some tests on complex tasks:

- [ ] android, `adb devices` - show some devices connected, if they are connected
 
- [ ] base, contains a lot of packages and require a lot of time to install
    - [ ] check pacman mirrors `sudo pacman -Syy`, must include core, extra, community, multilib
    - [ ] validate hostname `hostname -f`
    - [ ] validate group `id`
    - [ ] validate logrotate `logrotate --debug /etc/logrotate.conf`, home/...
    - [ ] run some applications: `tmux`, `git`, `ytfzf`, `ledger`, `ipython`, `sc-im`,  `bash`, `zsh`,  `krita`
      , `inkscape`, `darktable`, `blender`, `godot`, `maim`,
    - [ ] validate paccache service `systemctl status paccache.timer`

- [ ] media

- [ ] browsers:
    - w3m, lynx
    - using rofi: firefox, chromium, qutebrowser... can open url: http://acid3.acidtests.org/
      , `xdg-open http://acid3.acidtests.org/`
    - some browsers at first time require manual launch or extra configuration (tor browser)

- [ ] clipboard
- [ ] colemak-dh, vconsole works, ru layout works
- [ ] cups
- [ ] dconf
- [ ] dotfiles
- [ ] editors
- [ ] filesystems
- [ ] firejail
- [ ] fonts
- [ ] gnupg
- [ ] goesimage
- [ ] logitech
- [ ] mirrorlist
- [ ] mpv
- [ ] nettools
- [ ] office
- [ ] onlykey
- [ ] pass
- [ ] pdf
- [ ] postgresql
- [ ] pydev
- [ ] qbittorrent-nox
- [ ] ripgrep
- [ ] sound
- [ ] spell
- [ ] ssh
- [ ] sysctl
- [ ] sysmon
- [ ] systemd
- [ ] systemd-units
- [ ] udisks
- [ ] virtualenv
- [ ] visidata
- [ ] x
- [ ] zeal

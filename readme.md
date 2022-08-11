# My quick-start archlinux installation workflow
# NOT TESTED!

1. First, sync mirrors and install Ansible:

```shell
sudo pacman -Syy python-passlib ansible
```

2. Second, install and update the submodules:

```shell
git submodule init && git submodule update
```

3. Run the playbook as root (playbooks will use group_vars/all configuration, including username).

```shell
sudo ansible-playbook -i localhost playbook.yaml
```

4. It's recommended to reboot, to validate the installation.

```shell
reboot
```

# Run specific playbook

```shell
sudo ansible-playbook -i localhost playbook.yaml --tags "base"
```

# Special thanks
- https://github.com/pigmonkey/spark

# TODO
- systemd... resolv.... ntp
- user ssh key info
- validate systemd enabled services, like reflector

# Manual tests
ArchLinux 5.18.16-arch1-1 

- [ ] android, adb worked
- [ ] base
- [ ] borg, borg init (tmp), borg mount
- [ ] browsers
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
- [ ] media
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

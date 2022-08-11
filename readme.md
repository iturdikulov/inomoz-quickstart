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

# TODO tests
- browsers
- base
- colemak-dh, voconsole, etc... 

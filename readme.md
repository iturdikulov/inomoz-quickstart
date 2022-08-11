# My quick-start archlinux installation workflow
# NOT TESTED!

1. First, sync mirrors and install Ansible:

```shell
pacman -Syy python-passlib ansible
```

2. Second, install and update the submodules:

```shell
git submodule init && git submodule update
```

3. Run the playbook as root (playbooks will use group_vars/all configuration, including username).

```shell
sudo ansible-playbook -i localhost playbook.yml
```

# Special thanks
- https://github.com/pigmonkey/spark

# TODO
systemd... resolv.... ntp
user ssh key
validate systemd enabled services, like reflector

roles/nmtrust/tasks/unit.yml

ansible-playbook playbook.yml --tags "fonts,laptop"

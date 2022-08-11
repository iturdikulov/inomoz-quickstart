# My quick-start archlinux installation workflow

1. First, sync mirrors and install Ansible:

$ pacman -Syy python-passlib ansible

2. Second, install and update the submodules:

$ git submodule init && git submodule update

3. Run the playbook as root (playbooks will use group_vars/all configuration, including username).

```
# ansible-playbook -i localhost playbook.yml
```

# Special thanks
- https://github.com/pigmonkey/spark

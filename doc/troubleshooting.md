---
layout: documentation
---
# Troubeshooting Guide

## The terminal is empty when using vagrant ssh in msysgit

In case, you do not have a full blown cygwin envirnment, but rather `msysgit`, you might encounter problems with the ssh client.

By default cygwin uses the ssh client from it's msys environment
Use `VAGRANT_PREFER_SYSTEM_BIN=1 vagrant ssh` on Windows 10 to tell cygwin to use windows's ssh-client

Source: `https://github.com/hashicorp/vagrant/issues/9143#issuecomment-343311263`


## Ansible: Error connecting to host

    fatal: [atlassian1]: UNREACHABLE! => {"changed": false, "msg": "Failed to connect to the host via ssh: Permission denied (publickey,password).\r\n", "unreachable": true}

This error happens when executing the ansible-playbooks as root user.
You have to execute the playbooks as vagrant

## Minishift does not start

If you install Minishift in an environment with an AD domain it is possible, that Minishift doesn't start up.
Try to connect to your AD domain and then restart Minishift again.

## Timeouts during the execution of ansible-playbooks

Just execute the playbook again. The network is sometimes too slow.

## Issues that should no longer be relevant

### Ansible: Error finding role

    ERROR! the role '...' was not found in `/vagrant/ansible/playbooks/roles` ...

This should no happen, because the file mode was changed in the `Vagrant` file for the mounted ansible directories.

This error can happen on windows when the shared folder between windows and the vm doesn't have the right permissions. Then Ansible will ignore the ansible.cfg config-file in this folder which will cause it to use the wrong directory to search for roles.
To fix this you can modify the ansible.cfg file in /etc/ansible and change the roles_path to 
```
roles_path = /vagrant/ansible/roles
```


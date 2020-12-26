# Installing Ubuntu 20.04 LTS Server on sphinx

sphinx is a VM we run in our personal network.

This repository contains my notes and some ansible automation scripts from the installation so I can repeat it,
should I ever need to.

I MAKE NO CLAIM AS TO THE USEFULNESS OF THIS INFORMATION FOR ANY PARTICULAR PURPOSE.

USE AT YOUR OWN RISK.

## Initial installation

### Install OS

Install ubuntu server from the ISO image. We have no need for
disk encryption, so all should be easy.

Note that even if you do net set up a swap partition, the
installer will create a swap file and add an fstab entry.
The ansible playbooks will remove it again...

### Clone this repository

As root:

```
git clone https://github.com/Jumpy-Squirrel/sphinx-installation
```

### Install ansible

```
apt-get install ansible
```

in `/etc/ansible/hosts` put:

```
[sphinx]
localhost ansible_connection=local
```

### Run ansible playbooks

You can run any of the provided ansible playbooks using

```
cd sphinx-installation
ansible-playbook 10-packages.yml
ansible-playbook 15-nospam.yml
ansible-playbook 20-network-firewall.yml
ansible-playbook 30-swap-mounts.yml
ansible-playbook 40-users-ssh.yml --ask-vault-pass
ansible-playbook 50-encfs-scripts.yml --ask-vault-pass
ansible-playbook 60-smb-server.yml
ansible-playbook 70-local-mailserver.yml
```

Finally, run `smbpasswd` for each samba user. 

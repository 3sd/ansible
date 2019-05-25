# Ansible for 3SD

Ansible to manage 3SD infrastructure.

## Getting started

The following Ansible scripts are designed to be run on freshly installed Debian Buster machines which have selected the gnome desktop environment and ssh server during the installation.

### Bootstraping a control machine

If you are starting from scratch, bootstrap a control machine as follows:

As the root user:

```shell
apt install git
git clone https://github.com/3sd/ansible
mv ansible /etc
apt install ansible
chown -R /etc/ansible michael:michael # (replace with your user)
```

### Preparing hosts for ansible

`bootstrap.yml` installs sudo and allows passwordless invocation, which is necessary for ansible (and also useful for the owners of the workstations).

Note that the host will need to be accessible via ssh to run `bootstrap.yml`.

Note that the host should be accessible by ssh (which is the case if you installed the ssh server as part of the Debian installation).



The host should be accessible via ssh with a key pair.

## Initialisation

The following script can be run from a machine with ssh access to the server. Note that it

* enables passwordless sudo (necessary for Ansible)
* disables ssh connects that use passwords (good for security)

```
ansible-playbook /etc/ansible/playbooks/bootstrap.yml --ask-become-pass -e host=<HOSTNAME>
```

## Prerequisites

## Portable workstations

Portable workstations should start life with an encrypted install of the latest Debian release. Ensure that you install ssh server as part of the installation.

The ansible scripts in this repo expect passwordless sudo. If you can access the host from an ansible control machine, you can enable passwordless sudo with the following script:

# Bootstraping a workstation

If you are need to re-create a workstation and don't have access to another worstation to do this via ansible, you can do something like the following:


You should then be able to configure the rest of the workstation with:

```
ansible-playbook /etc/ansible/playbooks/workstation.yml
```

(provided your host is in ansible's `[workstation]` host group).

## Backup

All hosts with the backed-up role create local snapshots of selected directories every four hours. These backups can be collected by backup servers, which will carry out point in time (pit) backups on a four hourly, daily, weekly and yearly basis.

# Ansible for 3SD

Ansible to manage 3SD infrastructure.

The following Ansible scripts are designed to be run on Debian hosts.

# Prerequisites

The host should be accessible via ssh with a key pair.

# Initialisation

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

```
# inspired by https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html#id16
apt-get install git
git clone https://github.com/3sd/ansible /etc/ansible
echo "deb http://ppa.launchpad.net/ansible/ansible/ubuntu trusty main" > /etc/apt/sources.list.d/ansible.list
apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 93C4A3FD7BB9C367
apt-get update
apt-get install ansible
ansible-playbook /etc/ansible/playbooks/bootstrap.yml --ask-become-pass -e host=<HOSTNAME>
```

You should then be able to configure the rest of the workstation with:

```
ansible-playbook /etc/ansible/playbooks/workstation.yml
```

(provided your host is in ansible's `[workstation]` host group).

## Backup

All hosts with the backed-up role create local snapshots of selected directories every four hours. These backups can be collected by backup servers, which will carry out point in time (pit) backups on a four hourly, daily, weekly and yearly basis.

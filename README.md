# Ansible for 3SD

Ansible to

## Workstations

Everything you need to configure a workstation for Third Sector Design.

Start off with a encrypted install of the latest Debian distribution (with any  propietary drivers for your hardware installed). Log in as the root user and run the following:

```
# inspired by https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html#id16
sudo apt-get install git
git clone git@github.com:michaelmcandrew/ansible.git /etc/ansible???
echo "deb http://ppa.launchpad.net/ansible/ansible/ubuntu trusty main" > /etc/apt/sources.list.d/ansible.list
sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 93C4A3FD7BB9C367
sudo apt-get update
sudo apt-get install ansible
```

As long as your host is in ansible's `[workstation]` host group, you should then be able to configure the rest of the workstation with:

```
ansible-playbook /etc/ansible/playbooks/workstation.yml -c local
```

## Backup

All hosts with the backed-up role create local snapshots of selected directories every four hours. These backups can be collected by backup servers, which will carry out point in time (pit) backups on a four hourly, daily, weekly and yearly basis.

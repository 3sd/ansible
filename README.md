# Ansible for 3SD

Ansible to

## Workstations

Everything you need to configure a workstation for Third Sector Design.

Start off with a basic encrypted Debian (e.g. Stretch) install, log in as the root user and run the following:

```
# inspired by https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html#id16
sudo apt-get install git
git clone git@github.com:michaelmcandrew/ansible.git /etc/ansible???
echo "deb http://ppa.launchpad.net/ansible/ansible/ubuntu trusty main" > /etc/apt/sources.list.d/ansible.list
sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 93C4A3FD7BB9C367
sudo apt-get update
sudo apt-get install ansible
```

As long as your host is in the workstations host group, you should be able to configure it with

```
ansible-playbook /etc/ansible/playbooks/workstation.yml -c local
```

## Backups

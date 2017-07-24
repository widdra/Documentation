# Ansible
Simple, agentless IT automation.
<br/>
[Homepage](//www.ansible.com/) |
[Documentation](//docs.ansible.com/) |
[Github](//github.com/ansible/ansible)

## Installation
Assuming we are on an Ubuntu or ubuntu-like control machine managing other unix machines.
Installing on Windows Subsystem For Linux seems to work fine.

``` bash
sudo apt-get install software-properties-common
sudo apt-add-repository ppa:ansible/ansible
sudo apt-get update
sudo apt-get install ansible
```

## Setup Remote Machines To Control
Edit `/etc/ansible/hosts` on the control machine to include the remote machines you want to control.
You can also group them together.
Ansible will respect the ssh connection defaults in `~/.ssh/config` etc.
If these are not enough you can also add additional configuration for the ssh connections in this file [as shown here](//docs.ansible.com/ansible/intro_inventory.html).

Especially configuring the Python path can be valuable when using modern Ubuntu distributions because Ansible will try to use Python2 using the `python` command and only Python3 is preinstalled as `/usr/bin/python3`
``` ini
x1.example.com

[web]
w1.example.com
w2.example.com

[db]
d1.example.com
d2.example.com

[db:vars]
ansible_user=dbadmin
ansible_python_interpreter=/usr/bin/python3
```

On the remote machines you wish to control you have to prepare an up to date ssh.

``` bash
sudo apt-get update
sudo apt-get upgrade
sudo apt-get dist-upgrade
```

Additionally you have the option of using Python 2.7 (the default [as described here](//docs.ansible.com/ansible/latest/intro_installation.html#managed-node-requirements)) or Python 3 which requires said changes in your Inventory file but is preinstalled in Ubuntu.
``` bash
sudo apt-get install python2.7
```

## Creating Playbooks
``` yml
---
- hosts: web
  become: yes

  tasks:
  - name: Update repository cache and install nginx package
    apt:
      name: nginx
      update_cache: yes
      state: latest
  - name: Allow nginx traffic in UFW
    ufw:
      rule: allow
      name: Nginx Full
```

## Using Playbooks
To run a playbook, just execute `ansible-playbook playbook.yml` on the control machine.

If you need to specify the ssh password use the `--ask-pass` parameter.
If you use sudo/become in your tasks use the `--ask-become-pass` parameter.

The resulting call can look like `ansible-playbook playbook.yml --ask-pass --ask-become-pass`.
 
## Glossary
<dl>
 <dt>Inventory</dt>
 <dd>Configuration of machines to control, as example <code>/etc/ansible/hosts</code>.</dd>

 <dt>Playbook</dt>
 <dd>Deployment control files. Here we specify the final state our controlled machines should be changed/updated/upgraded to.</dd>
  
 <dt>Task</dt>
 <dd>A single configuration point. A playbook can have multiple tasks.</dd>
</dl>

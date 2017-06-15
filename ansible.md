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
``` ini
x1.example.com

[web]
w1.example.com
w2.example.com

[db]
d1.example.com
d2.example.com
```
 Except being able to ssh in there is no additional configuration needed on the machines you wish to control.
 
 ## Creating and Using Playbooks
 To run a playbook, just execute `ansible-playbook playbook.yml` on the control machine.
 
 ## Glossary
 <dl>
  <dt>Inventory</dt>
  <dd>Configuration of machines to control, as example <code>/etc/ansible/hosts</code>.</dd>

  <dt>Playbook</dt>
  <dd>Deployment control files. Here we specify the final state our controlled machines should be changed/updated/upgraded to.</dd>
  
  <dt>Task</dt>
  <dd>A single configuration point. A playbook can have multiple tasks.</dd>
</dl>

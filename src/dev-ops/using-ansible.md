# Using Ansible
> Links
> - [Ansible Full Course](https://www.youtube.com/watch?v=EcnqJbxBcM0)

Automates application deployment and infrastructure configuration.

Install Ansible from [this](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html) link for your OS.

Three key areas:
- IT automation
- Configuration management
- Automatic deployment

## Ansible Hosts File
The host file, located at */etc/ansible/hosts*, is where you configure your "inventory". That is, the clients and servers, their addresses, usernames, passwords, etc. 

**Example**
If you're looking to deploy an Ansible playbook locally, this is how you can configure a localhost.

*/etc/ansible/hosts*
```ini
[braden_local]
localhost ansible_connection=local ansible_user=braden
```

## Playbooks
A playbook forms one of the core components of the Ansible ecosystem; it is effectively a human readable set up instructions on what tasks should be carried out, for which hosts, and how everything should be configured. While the syntax is clear once everything has been written, the author of a playbook typically needs to conduct some research (or have some prior experience) in order to develop the playbook they envision.

**Example**
Here's a minimal example of how to create a local directory and install a package with APT.

*~/Projects/ansible-practice/example1.yml*
```yaml
---    
- name: sample playbook    
  hosts: braden_local   # Set of hosts/nodes to target in /etc/ansible/hosts        
  become: true          # Requires root elevated permissions    
  tasks:                                         
    - name: create directories                   
      file:                                   
        path: /home/{{ ansible_user }}/dev    
        state: directory                                            
    - name: install rsync                           
      apt:                                      
        update_cache: true   # Runs apt update                   
        state: latest                           
        pkg:                                    
          - rsync  
```

## Push Configuration
Ansible is a push configuration management tool

![[figs/ansible-architecture.png]]

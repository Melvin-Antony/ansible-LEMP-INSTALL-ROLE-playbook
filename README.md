Role Name
=========

This role can be used to install LEMP over Ubuntu. Clone this repository to the default role directory /etc/ansible/roles

- Features:
   - Fully configurable and compatible with AWS
   - Flexible and feature rich with easy customization of roles
   - Can be modified to support additional modules

Requirements
------------

EC2 role to deploy EC2s. A sample can be found in my other repository at https://github.com/Melvin-Antony/ansible-EC2-creation-ROLE


Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:
```
---
- name: "EC2 creation:"
  hosts: localhost
  gather_facts: False
  become: yes
  roles: 
        - ec2


  tasks:
      - name: "Aws InfraStructure Creation - Inventory Creation"
        add_host:
            groups: webservers
            name: "{{ item.public_ip }}"
            ansible_host: "{{ item.public_ip }}"
            ansible_port: 22
            ansible_user: ubuntu
            ansible_ssh_private_key_file: server-private.pem
            ansible_ssh_common_args: '-o StrictHostKeyChecking=no'
        with_items:
            - "{{ ec2_out.tagged_instances }}"



- name: "LEMP installation:"
  hosts: webservers
  gather_facts: False
  become: yes
  roles: 
        - lemp
  ```
  
  
  NOTE: Dynamic inventory creatin may not work properly within the Role. So wrote it within the playbook.

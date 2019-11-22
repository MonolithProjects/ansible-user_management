[![](https://github.com/MonolithProjects/ansible-ansible-user_management/workflows/Test%20build/badge.svg)](https://github.com/MonolithProjects/ansible-user_management/actions)  

# User Management
This Ansible role is for managing (creating, editing, deleting) Linux users.
Management includes also the ssh keys keys distribution.

#### This role can:
- create users
- delete users
- adding/removing users from the groups
- managing ssh keys

### Playbook example:
```
---
- name: User Management
  hosts: all
  user: root
  gather_facts: yes
  become: yes
  vars:
    user_management:
      - name: user1
        shell: /bin/bash
        groups:
          - sudo
          - games
          - docker
        ssh_keys:
          - 'ssh-ed25519 xxxxxx my_user_key'
          - 'ssh-rsa xxxxxx my_user_key'
      - name: user2
      - name: user3
  roles:
      - ansible-user_management
```

### License:
- MIT  

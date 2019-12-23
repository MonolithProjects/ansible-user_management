| Master branch |
|:--------------|
|[![](https://github.com/MonolithProjects/ansible-user_management/workflows/Test%20build/badge.svg?branch=master)](https://github.com/MonolithProjects/ansible-user_management/actions)|

# User Management
This Ansible role is for managing (creating, editing, deleting) Linux users.
Management includes also the ssh keys keys distribution.

**Note:** this role is using local facts on each server to store user names listed  
in `user_management`. Once you will remove the user from `user_management`  
list, the user and the home directory will be deleted from the server. The users  
not listed in the list, will remain untouched.

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
        shell: /bin/zsh
        expires: 1640991600
        groups:
          - sudo
          - games
          - docker
        ssh_keys:
          - 'ssh-ed25519 xxxxxx my_user_key'
          - 'ssh-rsa xxxxxx my_user_key'
      - name: user2
      - name: appuser
        system: yes
        create_home: no
  roles:
      - ansible-user_management
```

### License:
- MIT  

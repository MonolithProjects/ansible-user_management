# User Management

[![Last version](https://img.shields.io/github/v/release/MonolithProjects/ansible-user_management)](https://github.com/MonolithProjects/ansible-user_management)
[![Galaxy Quality](https://img.shields.io/ansible/quality/44861?style=flat&logo=ansible)](https://galaxy.ansible.com/monolithprojects/user_management)
[![Galaxy Downloads](https://img.shields.io/ansible/role/d/44861?style=flat&logo=ansible)](https://galaxy.ansible.com/monolithprojects/user_management)
[![GitHub Actions](https://github.com/MonolithProjects/ansible-user_management/workflows/molecule%20test/badge.svg?branch=master)](https://github.com/MonolithProjects/ansible-user_management/actions)

This Ansible role is for managing (creating, editing, deleting) Linux users.
Management includes also the ssh keys keys distribution.

**Note:** this role is using local facts on each server to store user names listed  
in `user_management`. Once you will remove the user from `user_management`  
list, the user and the home directory will be deleted from the server. The users  
not listed in the list, will remain untouched.

## This role is able to:

- create users
- delete users
- add/remove users from the groups
- manage ssh keys

## Playbook example:

```yaml
---
- name: User Management
  hosts: all
  user: root
  gather_facts: yes
  become: yes
  vars:
  
    user_management:
      - name: user1
        comment: My Test User
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

## License

MIT  

## Author Information

Created in 2020 by Michal Muransky

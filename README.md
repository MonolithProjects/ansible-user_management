# User Management

[![Last version](https://img.shields.io/github/v/release/MonolithProjects/ansible-user_management)](https://github.com/MonolithProjects/ansible-user_management)
[![Galaxy Quality](https://img.shields.io/ansible/quality/44861?style=flat&logo=ansible)](https://galaxy.ansible.com/monolithprojects/user_management)
[![Galaxy Downloads](https://img.shields.io/ansible/role/d/44861?style=flat&logo=ansible)](https://galaxy.ansible.com/monolithprojects/user_management)
[![GitHub Actions](https://github.com/MonolithProjects/ansible-user_management/workflows/molecule%20test/badge.svg?branch=master)](https://github.com/MonolithProjects/ansible-user_management/actions)

This Ansible role is for managing (creating, editing, deleting) Linux users.
Management includes also the ssh keys keys distribution.

## How it works

This role is using local facts on the each host to store the user names listed in `user_management`. Only these users are managed by this role. Once you will remove the user from `user_management` list, the user and the home directory will be deleted from the host. The users not listed in the `user_management` list (users not created by this Ansible Role) will remain untouched.

## This role is able to

- create users
- delete users
- edit users
- manage ssh keys

## Requirements

- Supported Linux distros:
  - CentOS/RHEL 7,8
  - Debian 9,10
  - Fedora 29,30,31,32
  - Ubuntu 16,18,20

  **Note:** These are the weekley tested Linux distributions. The Role will most likely run also on different Linux distros just fine.

## Role Variables

This is a copy from `defaults/main.yml`

```yaml
local_facts_file: linux_users.fact
local_facts_path: /etc/ansible/facts.d
user_management:
#   - name: userx                       <<< User name (Required).
#     comment: User X                   <<< (Optional) User description.
#     groups:                           <<< (Optional) List of groups user will be added to.
#       - games
#       - video
#     ssh_keys:                         <<< (Optional) List of Authorized public keys.
#       - 'ssh-ed25519 xxxx something'
#     shell: /bin/bash                  <<< (Optional) User shell (default value "/bin/bash")
#     expires: -1                       <<< (Optional) User expiration date in Epoch format (default value "-1").
#     create_home: yes                  <<< (Optional) Create home directory (default value "yes").
#     system: no                        <<< (Optional) Create a system account (default value "no").
```

## Playbook example:

In this example the Ansible will create (or eventually edit - if this is not the first run) 3 users. `user1` with comment, `zsh` as a default shell, user will expire in `1640991600` Unix epoch time, user will be added to user groups `sudo` and `docker`, and finally add two ssh public keys. `user2` will be created with defaults.`appuser` will be created as a system user.

```yaml
---
- name: User Management
  hosts: all
  user: ubuntu
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

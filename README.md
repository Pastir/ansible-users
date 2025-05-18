# Ansible Role: pastir.users

This Ansible role manages Linux users, their SSH keys, sudo privileges, and optional Git SSH configuration.

## Requirements
- Ansible >= 2.9
- Community modules: `community.general`, `ansible.posix`

## Role Variables

| Variable              | Default                                 | Description                                                                 |
|-----------------------|-----------------------------------------|-----------------------------------------------------------------------------|
| `path_files_directory`| `/etc/ansible/files/pair_key`           | Directory where user SSH key pairs are stored.                              |
| `user_names`          | `[]`                                    | List of users to manage. See below for structure.                           |

Each user in `user_names` should be a dictionary with the following keys:

- `name` (string, required): Username
- `sudo` (bool, optional): Add user to sudoers (default: false)
- `auth_key` (bool, optional): Add public key from `path_files_directory` (default: false)
- `key_pair` (bool, optional): Copy SSH key pair to user (default: false)
- `append` (string, optional): Additional groups (default: '')
- `shell` (string, optional): User shell (default: `/bin/bash`)
- `git` (bool, optional): Setup Git SSH key and config (default: false)
- `path_key_pair` (string, optional): Path to copy key pair (if needed)

## Example Playbook

```yaml
- hosts: all
  become: yes
  vars:
    path_files_directory: "/path_to_dir/authorized_key"
    user_names:
      - name: user1
        sudo: true
        auth_key: true
        key_pair: false
        append: ''
        shell: /bin/bash
        git: false
      - name: user2
        sudo: true
        auth_key: true
        key_pair: false
        append: ''
        shell: /bin/bash
        git: false
  roles:
    - pastir.users
```

## License
MIT

## Author Information
Ivan Pastir


# Ansible Role: pastir.users

This Ansible role manages Linux users, their SSH keys, sudo privileges, and optional Git SSH configuration.

## Requirements
- Ansible >= 2.9
- Community modules: `community.general`, `ansible.posix`

## Role Variables

| Variable                | Default                                 | Description                                                                 |
|-------------------------|-----------------------------------------|-----------------------------------------------------------------------------|
| `ssh_directory_users_keys`  | `/etc/ansible/files/pair_key`           | Directory where user SSH key pairs are stored.                              |
| `user_names`            | `[]`                                    | List of users to manage. See below for structure.                           |

Each user in `user_names` should be a dictionary with the following keys:

- `user` (string, required): Username
- `sudo` (bool, optional): Add user to sudoers (default: false)
- `auth_key` (bool, optional): Add public key from `directory_users_keys` (default: false)
- `key_pair` (bool, optional): Copy SSH key pair to user (default: false)
- `append` (string, optional): Additional groups (default: '')
- `shell` (string, optional): User shell (default: `/bin/bash`)
- `git` (bool, optional): Setup Git SSH key and config (default: false)
- `path_key_pair` (string, optional): Path to copy key pair (if needed)

### SSH Key Directory Structure

The `directory_users_keys` directory must have the following structure for each user:

```
<ssh_directory_users_keys>/
  └── <user_name>/
      ├── <user_name>        # Private key (no extension)
      └── <user_name>.pub    # Public key
```

For example, for user `alice`:
```
/etc/ansible/files/pair_key/alice/alice
/etc/ansible/files/pair_key/alice/alice.pub
```

## Example Playbook

```yaml
- hosts: all
  become: yes
  vars:
    ssh_directory_users_keys: "/path_to_dir/authorized_key"
    user_names:
      - user: user1
        sudo: true
        auth_key: true
        key_pair: false
        append: ''
        shell: /bin/bash
        git: false
      - user: user2
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


# ansible role - manage linux users 

### Example:

```ansible
---
- hosts: "host"
  gather_facts: yes
  remote_user: name_user
  become: yes
  become_user: root
  become_method: sudo
  
  vars:
    path_files_directory: "/path_to_dir/authorized_key"
    user_names:
   - {'name': user_name1, 'sudo': true, 'auth_key': true, 'key_pair': false, 'append': '', 'shell': '/bin/bash' }
   - {'name': user_name2, 'sudo': false, 'auth_key': true, 'key_pair': false, 'append': '', 'shell': '/bin/bash' }
  
  roles:
    - pastir.users
  ```


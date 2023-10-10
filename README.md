# Ansible Authorized Keys Playbook

This Ansible playbook sets the SSH authorized keys for specified users on target hosts.

## Playbook Structure

The playbook is designed to manage SSH authorized keys for various users. The key details and user information are fetched from an external file named `users.yml`.

Here's an overview of the playbook's structure:

```yaml
---
- hosts: all
  vars_files:
    - users.yml
  tasks:
  - name: Set authorized key taken from file
    ansible.posix.authorized_key:
      user: "{{item.username}}"
      state: "{{item.state}}"
      key: "{{ lookup('file', item.keyfile) }}"
    with_items: "{{ users }}"

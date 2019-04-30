Role : ansible-role-terraform-remove
====================================

Removes Hashicorp's Terraform by
* Deleting the terraform binary from terraform_bin_path (default: /usr/bin)
* Deleting the LXD provider from the terraform_bin_path (default: /usr/bin)
* Deleting the link to the LXD provider from the (non root) user's path
* Removing Terraform autocompletion from the (non root) user's bash configuration

Currently tested on these Operating Systems
* Ubuntu Server 18.04.2 LTS 64-bits with LXD v3.0.3 LTS (not the Snap packaged version)

Requirements
------------

* Ansible 2.5 or higher

Role Variables
--------------

defaults/main.yml
```
terraform_bin_path: "/usr/bin"							# Path to install terraform binary
```

Dependencies
------------

Requires elevated root privileges

Example Playbook
----------------

```
---

- name: Remove Hashicorp Terraform
  hosts: localhost
  become: yes
  gather_facts: no

  roles:
    - ansible-role-terraform-remove
```

License
-------

MIT License

Author Information
------------------

Adam Goldsmith & William Cocker (for LXD provider specific code)


Role : ansible-role-terraform-install
=====================================

Installs Hashicorp's Terraform by
* Downloading & unzipping terraform from Hashicorp's releases site into terraform_bin_path (default: /usr/bin)
* Downloading & unzipping the LXD Terraform provider into terraform_bin_path (default: /usr/bin)
* Creating a link to the LXD provider in the (non root) user's path
* Adding Terraform autocompletion to the (non root) user's bash configuration

Currently tested on these Operating Systems
* Ubuntu Server 18.04.2 LTS 64-bits with LXD v3.0.3 LTS (not the Snap packaged version)

Requirements
------------

* Ansible 2.5 or higher

Role Variables
--------------

defaults/main.yml
```
terraform_version: latest							# Version of terraform to download (latest unless specified)
terraform_arch: linux_amd64							# Architecture of binary to download
checkpoint_url: "https://checkpoint-api.hashicorp.com/v1/check/terraform"	# Terraform's checkpoint URL for gathering current data
terraform_dependencies:								# List of Terraform's software dependencies
  - unzip
terraform_bin_path: "/usr/bin"							# Path to install terraform binary
terraform_user: deploy								# Default (non root) Terraform user 
lxd_plugin_version: 1.1.3							# New releases can be [found here](https://github.com/sl1pm4t/terraform-provider-lxd/releases)
```

Dependencies
------------

Requires elevated root privileges

Example Playbook
----------------

```
---

- name: Install Hashicorp Terraform
  hosts: localhost
  become: yes
  gather_facts: no

  roles:
    - ansible-role-terraform-install
```

License
-------

MIT License

Author Information
------------------

Adam Goldsmith & William Cocker (for LXD provider specific code)


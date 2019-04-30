Role : ansible-role-lxd-init
=====================================

Initializes the LXD service (`lxd init`) with preseed values

This role can inspire you on automating the LXD initialisation process. It was created with a specific use-case in mind, that is to prepare LXD for [consul-vault](https://github.com/WilliamCocker/consul-vault) containers deployment using Terraform while respecting the [original project's](https://github.com/AdamGoldsmith/consul-vault) IP address plan (FYI: the original project uses Vagrant VMs and I made an LXD version that is lighter to run and still much better than the dev mode).

Currently tested on this Operating System
* Ubuntu Server 18.04.2 LTS 64-bits with LXD v3.0.3 LTS (not the Snap packaged version)

Requirements
------------

* Ansible 2.5 or higher
* The LXD service should not be already initialized (if it is, the re-initialisation might fail depending on how your storage pools, network and profiles were named)

Role Variables
--------------

defaults/main.yml
```
lxd_dependencies:									# List of LXD software dependencies (and LXD itself if not already installed)
  - btrfs-tools
  - lxd
lxd_temp_dir: /opt/lxd_temp							# Temp dir to store LXD preseed file and initialisation log output
```

Dependencies
------------

Requires elevated root privileges

Example Playbook
----------------

```
---

- name: Install and Initialize LXD
  hosts: localhost
  become: yes
  gather_facts: no

  roles:
    - ansible-role-lxd-init
```

License
-------

MIT License

Author Information
------------------

William Cocker


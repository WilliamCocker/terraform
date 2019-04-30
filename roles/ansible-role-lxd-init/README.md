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


Customization
-------------

Here is the resulting configuration using this role. At a minimum, you will probably want to customize the storage configuration, there are different sample files provided in the [templates](https://github.com/WilliamCocker/terraform/tree/master/roles/ansible-role-lxd-init/templates) directory.

- The default profile

```
config: {}
description: Default LXD profile
devices:
  eth0:
    name: eth0
    nictype: bridged
    parent: lxdbr0
    type: nic
  root:
    path: /
    pool: default
    type: disk
name: default
```

- The network bridge lxdbr0  

_Be careful to set the appropriate IPv4 address for your needs - this is the address plan used for the consul-vault use case_

```
config:
  ipv4.address: 10.1.42.1/24
  ipv4.nat: "true"
  ipv6.address: none
description: ""
name: lxdbr0
type: bridge
managed: true
status: Created
locations:
- none
```

- The default storage pool   

_Use btrfs or zfs for faster snapshot / restore operations. For the specific consul-vault use case, you won't need 200GB. The project's 10 containers + 1 snapshot each + 2 clients + 1 Ubuntu image will use a little under 50GB. So 60GB should be enough to start with._

```
config:
  size: 200GB
  source: /var/lib/lxd/disks/default.img
description: ""
name: default
driver: btrfs
status: Created
locations:
- none
```

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


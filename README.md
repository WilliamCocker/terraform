Hashicorp Terraform & LXD provider
==================================

Installs Terraform by Hashicorp (latest version & linux_amd64 architecture by default & LXD provider)
Can also initialize a fresh LXD install (see ansible-role-lxd-init)

Currently tested on these Operating Systems
* Ubuntu Server 18.04.2 LTS 64-bits with LXD v3.0.3 LTS (not the Snap packaged version)

Requirements
------------

* Ansible 2.5 or higher

Dependencies
------------

* Requires elevated root privileges

Getting the code
----------------

`git clone https://github.com/WilliamCocker/terraform.git`

Running the playbook
--------------------

__To install Terraform__

`ansible-playbook playbooks/terraform.yml --tags 'install'`

__To remove Terraform__

`ansible-playbook playbooks/terraform.yml --tags 'remove'`

__To initialize LXD__

`ansible-playbook playbooks/terraform.yml --tags 'init-lxd'`

License
-------

MIT License

Author Information
------------------

Adam Goldsmith & William Cocker (for LXD specific code)


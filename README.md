Hashicorp Terraform
===================

Installs Terraform by Hashicorp (latest version & linux_amd64 architecture by default)

Currently tested on these Operating Systems
* Oracle Linux/RHEL/CentOS 7
* Debian/Stretch64

Requirements
------------

* Ansible 2.5 or higher

Dependencies
------------

* Requires elevated root privileges

Getting the code
----------------

`git clone https://github.com/AdamGoldsmith/terraform.git`

Running the playbook
--------------------

__To install__

`ansible-playbook playbooks/terraform.yml`

__To remove__

`ansible-playbook playbooks/terraform.yml --tags 'remove'`

License
-------

MIT License

Author Information
------------------

Adam Goldsmith


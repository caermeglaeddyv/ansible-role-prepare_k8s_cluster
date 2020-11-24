Ansible role: Prepare Kubernetes Cluster
=========

This role is used to do common preparations before initializing kubernetes cluster and adding nodes to it using "caermeglaeddyv.ansible_role_k8s_control_plane" and "caermeglaeddyv.ansible_role_k8s_node" roles

For now, it does the following tasks:
- disables SELinux and reboots inventory hosts
- permanently removes swap
- enables masquerade, opens kubelet port in firewall
- adds br_netfilter kernel module if missing
- applies all necessary sysctl configurations
- adds official kubernetes repository, installs kubeadm, kubelet and kubectl, starts kubelet


Requirements
------------

This is not strict requirements and it may not work with other versions than tested ones.
Anyway. feel free to test by yourself, suggest addition of new functionality and contribute.

Role is tested with:
- Ansible version >= 2.8.6
- CentOS version >= 7.6 (1803)


Role Variables
--------------

Variables and their descriptions copied from defaults/main.yml

```bash

# Version of the kubernetes components which will be installed:
kubernetes_version: 1.14.10

```


Dependencies
------------

none


Example Playbook
----------------

```bash
---
- hosts: localhost
  gather_facts: false
  become: no
  tasks:
  - name: Check ansible version >=2.8.6
    assert:
      msg: Ansible must be v2.8.6 or higher
      that:
      - ansible_version.string is version("2.8.6", ">=")
    tags:
    - check
  vars:
    ansible_connection: local

- hosts: all
  become: yes
  tasks:
  - import_role:
      name: caermeglaeddyv.ansible_role_prepare_k8s_cluster

```

More detailed examples ( inventories, playbooks etc. ) of this and other roles can be found [here](https://github.com/caermeglaeddyv/examples/tree/dev/ansible).

It's highly recommended to start you test deploys from there, especially if you use Google Cloud Platform or VMware vCenter as your infrastructure, for now that [repository](https://github.com/caermeglaeddyv/examples) contains [Packer](https://github.com/caermeglaeddyv/examples/tree/dev/packer) and [Terraform](https://github.com/caermeglaeddyv/examples/tree/dev/terraform) examples to build templates and deploy machines on this platforms.


License
-------

[Apache 2.0](https://github.com/caermeglaeddyv/ansible-role-prepare_k8s_cluster/blob/dev/LICENSE)


Author Information
------------------

Copyright 2020 [caermeglaeddyv](https://github.com/caermeglaeddyv)

vc_vmcreate
=========

This role allows you deploy new VM or some VMs in VMWare Vcenter.
Tested with 5.5 and 6.0 - works perfect.

You can easly deploy lot's of virtual machines from template.
Also you can combine this role with your own roles for some installation on freshly created VMs.

Requirements
------------


Role Variables
--------------
Add this later, or.... doesnt' really matter

Dependencies
------------
There are no deps from Ansible Galaxy

Example Playbook
----------------
Here is the example of using:

Main file(playbook.yaml):

```yaml
---
- hosts: localhost
  gather_facts: false
  vars_files:
    - vc.yml    # file with sensitive data from vcenter
    - testvm.yml
  roles:
    - vmcreate
...
```

File with VM's info (testvm.yaml):
```yaml
---

vm_name: "testvm20170910"
vm_state: "powered_on"
vm_notes: "VM_for_testing_purposes"
vm_disk:
  disk1:
    size_gb: "10"
    type: "thin"
    datastore: "stor1.esxi.nl.data01.vv"
  disk2:
    size_gb: "5"
    type: "thin"
    datastore: "stor2.esxi.nl.data01.vv"
vm_nic:
  nic1:
    type: "vmxnet3"
    network: "vDS01-VLANXXX-Test"
    network_type: "standard"
    ip: "192.168.1.100"
    netmask: "255.255.255.0"
    gateway: "192.168.1.1"
    domain: "domain.lan"
    dns_servers:
      - "192.168.1.1"
      - "192.168.1.2"
  nic2:
    type: "vmxnet3"
    network: "vDS01-VLANXXX-Test"
    network_type: "standard"
vm_mem: "512"
vm_cpu: "1"
vm_osid: "centos64Guest"
datacenter: "BMH-DC"
target_esxi: "domain-esxi05.domain.lan"
from_template: "yes"
template_src: "testtemplate"

...
```

File with sensitive data to get access to VCenter(vc.yaml):
Please be aware that it's better to keep such data with Ansible Vault
```yaml
---
vcenter_hostname: "vcenter01.domain.lan"
vcenter_username: "ansible@domainlan"
vcenter_password: "password"
...
```
License
-------

GPL V3


Author Information
------------------

Tenhi(adm@tenhi.ru)

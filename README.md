vc_vmcreate
=========

This role allows you deploy new VM or some VMs in VMWare Vcenter.
Tested with 5.5 and 6.0 - works perfect.

You can easly deploy lot's of virtual machines from template.
Also you can combine this role with your own roles for some installation on freshly created VMs.

Requirements
------------
Add this later

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
# Name of the VM in VCenter
vm_name: "testvm20170910"

# Power it on after preparation
vm_state: "poweredon"

# Add annotation
vm_notes: "TestVM"

# Set 2 disks to VM
vm_disk: 
  disk1:
    size_gb: 10
    type: thin
    datastore: storage01
  disk2:
    size_gb: 20
    type: thin
    datastore: storage02
vm_nic:
  nic1:
    type: vmxnet3
    network: network1
    network_type: standard
  nic2:
    type: vmxnet3
    network: network2
    network_type: standard
vm_mem: 2048
vm_cpu: 2

# OSid
vm_osid: "centos64Guest"

# Name of you DC
datacenter: "MYDC"

# Certaion ESXI where VM will be hosted after powering on
target_esxi: "esxi01"

# Set that it should be cloned from gold-image
from_template: yes

# Name of the Template
template_src: centosTemplate
...
```

File with sensitive data to get access to VCenter(vc.yaml):
Please be aware that it's better to keep such data with Ansible Vault
```yaml
---
vcenter_hostname: "vcenter01.net.local"
vcenter_username: "ansible@net.local"
vcenter_password: "somepassword"
...
```
License
-------

GPL V3


Author Information
------------------

Tenhi(adm@tenhi.ru_

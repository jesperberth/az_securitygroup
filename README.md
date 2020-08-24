Az_securitygroup
=========

Creates a Resource Group in Microsoft Azure

Requirements
------------

Requires Azure SDK 

pip install 'ansible[azure]'

Role Variables
--------------

Role takes following vars

resourcegroup = name of the resource group to create
location = Azure location to create resourcegroup in
tag_owner = Create tag owner with value
tag_project = Create tag project with value
networksecuritygroup_name = Security Group Name
rulename = Name of rule
ruleprotocol = Protocol type Any/Tcp/Udp/Icmp
rulesourceaddress = Source IP for any 0.0.0.0/0
ruledestinationportrange = Target port eg. 443 for HTTPS
ruleaccess = Allow/Deny
rulepriority = Priority to other rules
ruledirection = Inbound/Outbound

Dependencies
------------

None

Example Playbook
----------------

```ansible

- hosts: localhost
  name: Create Azure Security Group
  vars:
    resourcegroup_name: resourcegroupname
    location: northeurope
    tag_owner: jesper
    tag_project: demoproject
  tasks:
    - name: Azure Security Group
      include_role:
        name: jesperberth.az_securitygroup
      vars:
        resourcegroup: "{{ resourcegroup_name }}"
        networksecuritygroup_name: SG_Network
        rulename: "AllowHTTPS"
        ruleprotocol: "Tcp"
        rulesourceaddress: 0.0.0.0/0
        ruledestinationportrange: "443"
        ruleaccess: "Allow"
        rulepriority: "101"
        ruledirection: "Inbound"
```
With Multible rules in a loop

```ansible

- hosts: localhost
  name: Create Azure Security Group
  vars:
    resourcegroup_name: resourcegroupname
    location: northeurope
    tag_owner: jesper
    tag_project: demoproject
  tasks:
    - name: Azure Security Group
      include_role:
        name: jesperberth.az_securitygroup
      vars:
        resourcegroup: "{{ resourcegroup_name }}"
        networksecuritygroup_name: "{{ item.networksecuritygroup_name }}"
        rulename: "{{ item.rulename }}"
        ruleprotocol: "{{ item.ruleprotocol }}"
        rulesourceaddress: "{{ item.rulesourceaddress }}"
        ruledestinationportrange: "{{ item.ruledestinationportrange }}"
        ruleaccess: "{{ item.ruleaccess }}"
        rulepriority: "{{ item.rulepriority }}"
        ruledirection: "{{ item.ruledirection }}"
      loop:
        - { networksecuritygroup_name: 'SG_Network', rulename: 'AllowHTTP',  ruleprotocol: 'Tcp', rulesourceaddress: '0.0.0.0/0', ruledestinationportrange: '80', ruleaccess: 'Allow', rulepriority: '102', ruledirection: 'Inbound' }
        - { networksecuritygroup_name: 'SG_Network', rulename: 'AllowHTTPS',  ruleprotocol: 'Tcp', rulesourceaddress: '0.0.0.0/0', ruledestinationportrange: '443', ruleaccess: 'Allow', rulepriority: '103', ruledirection: 'Inbound' }

```

License
-------

BSD

Author Information
------------------

Jesper Berth
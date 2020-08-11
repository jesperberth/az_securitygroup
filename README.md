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
    resourcegroup: resourcegroupname
    location: northeurope
    tag_owner: jesper
    tag_project: demoproject
  tasks:
    - name: Azure Security Group
      include_role:
        name: jesperberth.az_securitygroup
      vars:
        networksecuritygroup_name: SG_Network
        rulename: "AllowHTTPS"
        ruleprotocol: "Tcp"
        rulesourceaddress: 0.0.0.0/0
        ruledestinationportrange: "443"
        ruleaccess: "Allow"
        rulepriority: "101"
        ruledirection: "Inbound"
```

License
-------

BSD

Author Information
------------------

Jesper Berth
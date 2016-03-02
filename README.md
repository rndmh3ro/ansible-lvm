LVM Ansible role
================

Work in progress: not ready!!!!!!!!!!!

Role to manage LVM Groups/Logical Volumes. Can be used to create, extend or resize LVM Groups and volumes.

Requirements
------------

Devices/disks to be part of the LVM setup must be identified prior to using this role. Ensure that you select the correct devices/disks.

Role Variables
--------------

````
---
# defaults file for ansible-manage-lvm
lvm_groups:
  - vgname: ubuntu-vg
    disks: /dev/sda5,/dev/sdc,/dev/sdd  #for multiple disks...../dev/sdb,/dev/sdc
    create: true  #defines if VG should exist or be removed....true or false
    lvnames:
      - lvname: swap_1
        size: 5g  #define size of lvol...100%FREE, 10g, 1024 (megabytes by default)
        create: true  #defines if lvol should exist or be removed...true or false
        filesystem: swap  #defines filesystem to format lvol as
        mount: false  #defines if filesystem should be mounted
        mntp: []  #defines mountpoint for lvol
      - lvname: root
        size: 40g  #define size of lvol...100%FREE, 10g, 1024 (megabytes by default)
        create: true  #defines if lvol should exist or be removed...true or false
        filesystem: ext4  #defines filesystem to format lvol as
        mount: true
        mntp: /  #defines mountpoint for lvol

# VG whitout LV
  - vgname: test-vg
    disks: /dev/sdb  #for multiple disks...../dev/sdb,/dev/sdc
    create: true  #defines if VG should exist or be removed....true or false
    lvnames: []
lvm_apply: false  #defines if LVM will be managed by role....default is false to ensure nothing is changed by accident.
````

Dependencies
------------

None

Example Playbook
----------------

    - hosts: servers
      roles:
         - HanXHX.lvm

License
-------

BSD

Author Information
------------------

- Twitter: [@hanxhx_](https://twitter.com/hanxhx_)

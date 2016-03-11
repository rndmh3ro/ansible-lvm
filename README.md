LVM Ansible role
================

[![Ansible Galaxy](http://img.shields.io/badge/ansible--galaxy-HanXHX.lvm-blue.svg)](https://galaxy.ansible.com/HanXHX/lvm) [![Build Status](https://travis-ci.org/HanXHX/ansible-lvm.svg)](https://travis-ci.org/HanXHX/ansible-redis)

Role to manage LVM Groups/Logical Volumes. Can be used to create, extend or resize LVM Groups and volumes.

Requirements
------------

Devices/disks to be part of the LVM setup must be identified prior to using this role. Ensure that you select the correct devices/disks.

Role Variables
--------------

`lvm_groups` is a list containing vgs.

### vgs

- `vgname`: uniq name
- `disks`: add disks/partitions to vg (comma separated)
- `create`: boolean (true => creates, false => deletes)
- `lvnames`: lv list (see bellow)

### lvnames

- `lvname`: uniq name
- `size`: define size of lvol (ex: "10G", "512M"...)
- `create`: defines if lvol should exist or be removed...true or false
- `filesystem`: defines filesystem to format lvol as
- `mount`: defines if filesystem should be mounted
- `mount_point`: defines mountpoint
- `mount_options`: defines mount options (comma separated)

Dependencies
------------

None

Example Playbook
----------------

    - hosts: servers
      vars:
      - vgname: misc-vg
        disks: /dev/sda5,/dev/sdc,/dev/sdd
        create: true
        lvnames:
          - lvname: swap_1
            size: 5g
            create: true
            filesystem:
            mount: false
          - lvname: mysql
            size: 40g
            create: true
            filesystem: ext4
            mount: true
            mount_point: /var/lib/mysql
            mount_options: 'defaults,noatime'
        # VG whitout LV
      - vgname: test-vg
        disks: /dev/sdb
        create: true
        lvnames: []

      roles:
         - HanXHX.lvm

License
-------

BSD

Author Information
------------------

- Twitter: [@hanxhx_](https://twitter.com/hanxhx_)

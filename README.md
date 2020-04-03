# Ansible Role: NFS

[![Build Status](https://travis-ci.org/geerlingguy/ansible-role-nfs.svg?branch=master)](https://travis-ci.org/geerlingguy/ansible-role-nfs)

Installs NFS utilities on RedHat/CentOS or Debian/Ubuntu.

## Requirements

None.

## Role Variables

Available variables are listed below, along with default values (see `defaults/main.yml`):

    nfs_exports: []

A list of exports which will be placed in the `/etc/exports` file. See Ubuntu's simple [Network File System (NFS)](https://help.ubuntu.com/14.04/serverguide/network-file-system.html) guide for more info and examples. (Simple example: `nfs_exports: [ "/home/public    *(rw,sync,no_root_squash)" ]`).

This list can be `/etc/exports` compliant, or a list in the following form:

    nfs_exports:
      - path: "/exports/this/path"
        owner: someuser
	allow: 10.42.0.0/16
	options: "rw,sync,no_root_squash"

    nfs_owner: "root"
    nfs_group: "root"

The owner of the exported filesystem.

    nfs_rpcbind_state: started
    nfs_rpcbind_enabled: true

(RedHat/CentOS/Fedora only) The state of the `rpcbind` service, and whether it should be enabled at system boot.

    nfs_mapping:
      nobody_user: []
      nobody_group: []
      domain: []

The mapping of users and domain, placed in `/etc/idmapd.conf` file. Defaults are `nobody` for user, and `nogroup` for group. If no domain specified, it defaults to value returned by `dnsdomainname` command.

    nfs_pipefs:

Depends on distribution and version used, these pipefs located in `/etc/idmapd.conf` file may change.

## Dependencies

None.

## Example Playbook

    - hosts: db-servers
      roles:
        - { role: geerlingguy.nfs }

## License

MIT / BSD

## Author Information

This role was created in 2014 by [Jeff Geerling](https://www.jeffgeerling.com/), author of [Ansible for DevOps](https://www.ansiblefordevops.com/).

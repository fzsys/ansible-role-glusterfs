# Ansible Role: GlusterFS

[![CI](https://github.com/geerlingguy/ansible-role-glusterfs/workflows/CI/badge.svg?event=push)](https://github.com/geerlingguy/ansible-role-glusterfs/actions?query=workflow%3ACI)

Installs and configures GlusterFS on Linux.

This role is based on the original `glusterfs` role created by [geerlingguy](https://github.com/geerlingguy). Modifications have been made to extend functionality, update compatibility with newer distributions, and incorporate community feedback.

## Modifications Made
- Changed deprecated 'include' module to the 'include_tasks'
- Updated gluster version fro m7 to 10 in the defaults file

## Original Role
You can find the original role by geerlingguy here: [geerlingguy/ansible-role-glusterfs](https://github.com/geerlingguy/ansible-role-glusterfs).

## Requirements

For GlusterFS to connect between servers, TCP ports `24007`, `24008`, and `24009`/`49152`+ (that port, plus an additional incremented port for each additional server in the cluster; the latter if GlusterFS is version 3.4+), and TCP/UDP port `111` must be open. You can open these using whatever firewall you wish (this can easily be configured using the `geerlingguy.firewall` role).

This role performs basic installation and setup of Gluster, but it does not configure or mount bricks (volumes), since that step is easier to do in a series of plays in your own playbook. Ansible 1.9+ includes the [`gluster_volume`](https://docs.ansible.com/ansible/latest/collections/gluster/gluster/gluster_volume_module.html#ansible-collections-gluster-gluster-gluster-volume-module) module to ease the management of Gluster volumes.

## Role Variables

Available variables are listed below, along with default values (see `defaults/main.yml`):

    glusterfs_default_release: ""

You can specify a `default_release` for apt on Debian/Ubuntu by overriding this variable. This is helpful if you need a different package or version for the main GlusterFS packages (e.g. GlusterFS 3.5.x instead of 3.2.x with the `wheezy-backports` default release on Debian Wheezy).

    glusterfs_ppa_use: true
    glusterfs_ppa_version: "LATEST"

For Ubuntu, specify whether to use the official Gluster PPA, and which version of the PPA to use. See Gluster's [Getting Started Guide](https://docs.gluster.org/en/latest/Install-Guide/Install/) for more info.

    glusterfs_gpg_key_version: "7"
    glusterfs_deb_version: "LATEST"

For Debian, specify the version of the GPG key and apt package repository to use. See Gluster's [Getting Started Guide](https://docs.gluster.org/en/latest/Install-Guide/Install/) for more info.

## Dependencies

None.

## Example Playbook

    - hosts: server
      roles:
        - geerlingguy.glusterfs

For a real-world use example, read through [Simple GlusterFS Setup with Ansible](https://www.jeffgeerling.com/blog/simple-glusterfs-setup-ansible), a blog post by this role's author, which is included in Chapter 8 of [Ansible for DevOps](https://www.ansiblefordevops.com/).

## License

MIT / BSD

## Author Information

This role was created in 2015 by [Jeff Geerling](https://www.jeffgeerling.com/), author of [Ansible for DevOps](https://www.ansiblefordevops.com/).

# osa-designate-bind

Playbooks to set up bind containers on openstack-ansible controller nodes for designate.


This has only been tested on an ubuntu 18 train environment.  The playbooks do the following:
* Sets up "bind" containers.
* Installs bind and copies the rndc key file to the deploy box.
* Sets up the rndc key on the designate servers
* Generates /etc/openstack_deploy/user_local_designate_pools.yml
* Runs the designate playbooks to update the pool config.
* Sets up port forwarding for udp/tcp port 53 on infra primary interface to the bind containers.

## Usage (to be ran from the OSA deploy host)

```
openstack-ansible install-bind.yml
```

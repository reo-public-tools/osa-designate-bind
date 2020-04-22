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
Note: The glue records may not be pullable from the available vars depending on who sets up the delegation in dns.  Due to this, its a required variable without a default.
```
openstack-ansible create-bind-containers.yml
openstack-ansible install-bind.yml -e '{"glue_records":["ns01.somegluensrecord.com.","ns02.somegluensrecord.com.","ns03.somegluensrecord.com."]}' -e 'allow_recursion=yes' 
```

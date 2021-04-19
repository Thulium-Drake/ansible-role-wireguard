[![Build Status](https://drone.element-networks.nl/api/badges/Ansible/role-wireguard/status.svg)](https://drone.element-networks.nl/Ansible/role-wireguard)

# Wireguard
This role provides a means to configure Wireguard in the following 2 scenarios:

* many to one peer
* one to one peer

It is completely controlled via the Ansible inventory and it works like this:

* Create a new group in your inventory:
```
[wireguard_vpn_net]
wg-server.example.com
wg-client.example.com
```

* Configure each host via their ```host_vars``` (see defaults/main.yml for examples)
  * If you have multiple wireguard interfaces, do note that peer relations are determined
    based off the name of the interface. E.g. both peers will have ```wg1``` connected
    to each other.
* Run Ansible

If you have non-Ansible controlled peers, you can add the [Peer] sections for
these peers in ```/etc/wireguard/{{ interface }}.conf.d/```. All files in this directory
are assembled to form ```/etc/wireguard/{{ interface }}.conf```.

NOTE: The templates for this role rely heavily on the Ansible inventory. Therefore
the Ansible Controller _must_ know all private keys (protect them using Ansible Vault!)

It will also require wireguard-tools to render the public keys.

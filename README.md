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
* Run Ansible

If you have non-Ansible controlled peers, you can add the [Peer] sections for
these peers in ```/etc/wireguard/{{ interface }}.conf.d/```. All files in this directory
are assembled to form /etc/wireguard/{{ interface }}.conf.

NOTE: The templates for this role rely heavily on the Ansible inventory. Therefore
the Ansible Controller _must_ know all private keys (protect them using Ansible Vault!)

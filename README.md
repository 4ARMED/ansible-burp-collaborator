# Burp Collaborator Server Ansible Role

Installs [Burp Collaborator Server](https://portswigger.net/burp/) on a Ubuntu 16.04 Linux host.

## Requirements

- Debian-based Linux target
- Unix/Linux-based Ansible 2.2 machine with openssl installed
- Burp Suite Professional jar file (https://portswigger.net/burp/)

## Role Variables

`
burp_http_port: 80
burp_https_port: 443
burp_dns_port: 53
burp_metrics_path: metricated
burp_whitelist: '["127.0.0.1"]'
burp_key: burp.pk8
burp_cert: burp.crt
burp_ca_bundle: intermediate.crt
burp_server_domain: collaborator.example.com
burp_local_address: <internal IP address>
burp_public_address: <public IP address> # May be the same as above
`

If you would like Ansible to generate you a self-signed cert for use with Collaborator complete the following, otherwise set `generate_self_signed_certs` to `false`.

`
generate_self_signed_certs: true
country: GB
state: London
locality: London
organisation: 4ARMED
organisational_unit: Training
`

## Dependencies

- 4ARMED.java

## Example Playbook

```
---
- hosts: all
  become: yes
  gather_facts: False
  vars:
    - burp_server_domain: collaborator.example.com
    - burp_local_address: 138.68.191.190
    - burp_public_address: 138.68.191.190
  pre_tasks:
    - name: Burp | Install Python 2
      raw: test -e /usr/bin/python || (apt -y update && apt install -y python-minimal)

  roles:
    - { role: 4ARMED.burp-collaborator }
```

### License

MIT/BSD

### Author Information

Created by [@marcwickenden](https://twitter.com/marcwickenden) at [4ARMED](https://www.4armed.com/).

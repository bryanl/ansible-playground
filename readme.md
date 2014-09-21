# ansible playground

This is a playground for exploring ansible constructs

## Setup

### Configuring hosts

Add inventory configurations to the `hosts` file. There is an example file in the repository.

```ini
localhost ansible_connection=local

[webservers]
web01.prod.example.com

[utilservers]
util01.prod.example.com

[servers:children]
webservers
utilservers
```

## Provisioning hosts

The goal with this set of tasks is bring up new Digital Ocean Droplets.

`ansible-playbook provision.yml -i ./hosts -u root --private-key ~/.ssh/id_rsa -e "group=servers domain=example.com`

This will provision the two servers defined in the inventory file `hosts` and configure DNS using Dnsimple. The `domain` key is used to determin the DNS domain to update.

## Terminating hosts

The goal with this set of tasks is to shutdown servers that were configured before. Currently removing DNS does not work correctly.

`ansible-playbook terminate.yml -i ./hosts`

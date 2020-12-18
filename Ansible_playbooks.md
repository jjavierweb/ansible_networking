# Building playbooks

Playbooks allow to perform muliple task, which means that we can run multiple actions on a node or a group of nodes, an example of a simple playbook is gathering the facts from a device and then print it out on the screen, you can find that here:

```yaml
---

- name: Gather devices info and then show to screen
  connection: ansible.netcommon.network_cli
  gather_facts: false
  hosts: all
  tasks:
  
    - name: Get device information
      cisco.ios.ios_facts:
      gather_subset: all

    - name: Display device info
      debug:
        msg: "The node {{ansible_net_hostname}} is running OS version {{ansible_net_version}}"
```

To run this playbook we just need to perform a very simple command from our venv

```bash
$ ansible-playbook playbooks/get_device_config.yml
```

This will use the default inventory file as we defined on the ansible.cfg file and the password that we encoded inside the ansible-vault

Another way to perform this is by passing the invetory file and password, for example:

```bash
$ ansible-playbook -i inventory/hosts.yml -k playbooks/get_device_config
```

1. The -k argument here can be passed to get ansible to prompt for a password
2. The -i argument is used to specify the inventory, you can pass a host, a file or an fqdn, if you pass something other than the file, you will need to add a coma, example:

```bash
$ ansible-playbook -i leaf1-bdn1.westmancom.com, -k playboks/get_device_config
```

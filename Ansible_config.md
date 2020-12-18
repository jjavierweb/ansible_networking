# Ansible config file

Make sure to change the following configuration entries on ansible.cfg
An example of this config file can be downloaded from [Ansible Github page](https://github.com/ansible/ansible/blob/devel/examples/ansible.cfg)

```test
[defaults]
inventory = inventory/hosts.yml

vault_password_file = ansible-vault-pw-file

[paramiko_connection]
host_key_auto_add = True
```

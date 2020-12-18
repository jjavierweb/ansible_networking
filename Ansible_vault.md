# Using Ansible vault to store secrets

We are going to use ansible vault to store secret passwords, like ssh passwords or enable passwords
To do that we need to perform the following changes:

1. Inside the ansible-vault-pw-file enter a string to use as the master password
2. Create a vault secret using this file

```bash
$ ansible-vault encrypt_string [user_name]@ansible-vault-pw-file 'secret to encrypt' --name 'ansible_password'
```

3. Copy the generated encruption key and save it somewhere as we will use it later on the vars, it should look something like this:

```text
ansible_password: !vault |
       $ANSIBLE_VAULT;1.2;AES256;my_user
       66386134653765386232383236303063623663343437643766386435663632343266393064373933
       3661666132363339303639353538316662616638356631650a316338316663666439383138353032
       63393934343937373637306162366265383461316334383132626462656463363630613832313562
       3837646266663835640a313164343535316666653031353763613037656362613535633538386539
       65656439626166666363323435613131643066353762333232326232323565376635
```

More information about ansible-vault can be found at [ansible documentaiton](https://docs.ansible.com/ansible/latest/network/getting_started/first_inventory.html)
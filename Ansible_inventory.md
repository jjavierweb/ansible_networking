# Creating inventory for our hosts

We have a couple of ways to create an inventory for our devices, we can use the INI format or the yml(yaml) format. We will be using the yaml format with a hosts.yml file
Inside the file make sure there is something like this:

```yaml
---

switches:
  hosts:
    leaf1a-bdn1:
      ansible_host: [ip| fqdn]
  leaf1b-bdn1:
  ansible_host: [ip| fqdn]
    spine1-bdn1:
      ansible_host: [ip|fqdn]
  spine2-bdn1:
    ansible_host: [ip|fqdn]

spine:
  children:
    spine1-bdn1:
  spine2-bdn1:
leaf:
  children:
    leaf1a-bdn1:
    leaf1b-bdn1:

eos:
  children:
    spine:
    leaf:
  vars:
     ansible_network_os: arista.eos.eos
    ansible_user: [username]
    ansible_password: !vault |
       $ANSIBLE_VAULT;1.2;AES256;my_user
       66386134653765386232383236303063623663343437643766386435663632343266393064373933
       3661666132363339303639353538316662616638356631650a316338316663666439383138353032
       63393934343937373637306162366265383461316334383132626462656463363630613832313562
       3837646266663835640a313164343535316666653031353763613037656362613535633538386539
       65656439626166666363323435613131643066353762333232326232323565376635
```

Notice that under switches we have independant hosts, then we can agregate those hosts inside groups by using the children key, we can go further and group by an OS version and provide a group of variables that will be shared for all these devices like os, username and password, and you can see that we are using the ansible-vault to bring that password into the inventory file at the end

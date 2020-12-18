# Ansible Roles

Ansible roles are a collection of task, playbooks,files, variables and other files that help agregate, reuse and share ordered tasks. Ansible Galaxy is the place to get/share roles wiht other people.

## What is a role?

A role is like a playbook broken into a known file structure, this makes it easier to implement our Ansible workflow. Examples of roles can be found on [Ansible Galaxy](https://galaxy.ansible.com/ansible-network)

## Creating a role

Roles can be created by following the proper folder structure. This structure can be created manually or by using the <strong>ansible-galaxy</strong> command

### Role folder structure

```text
.
├── defaults
│   └── main.yml
├── files
├── handlers
│   └── main.yml
├── meta
│   └── main.yml
├── README.md
├── tasks
│   └── main.yml
├── templates
├── tests
│   ├── inventory
│   └── test.yml
└── vars
  └── main.yml
```

### Creating a role

```bash
mkdir roles
cd roles
ansible-galaxy init update_dns
```

## Moving a playbook into a role

As mentioned above, roles are basically a playbook devided into multiple files and folders. Take this playbook for example:

```yaml
---
- name: configure cisco routers
  hosts: routers
  connection: ansible.netcommon.network_cli
  gather_facts: no
  vars:
    dns: "8.8.8.8 8.8.4.4"

  tasks:
   - name: configure hostname
     cisco.ios.ios_config:
       lines: hostname {{ inventory_hostname }}

   - name: configure DNS
     cisco.ios.ios_config:
       lines: ip name-server {{dns}}
```

In the playbook we have variables and task, in roles we have the same things, they are just devided into different files, so for example, the tasks that we have defined on the playbook can be moved into the task directory and into the main, same applies to variables.

After performing this changes, we go back to the playbook and change it a bit, this time, we just need to include the role into it, and it will look like this:

```yaml
---
- name: configure cisco routers
  hosts: routers
  connection: ansible.netcommon.network_cli
  gather_facts: no

  roles:
    - dns_role
```

> **Note that if you are putting all your roles inside a folder, then you need to specify the folder in the role name**

```yaml
---
- name: configure cisco routers
  hosts: routers
  connection: ansible.netcommon.network_cli
  gather_facts: no

  roles:
    - roles/dns_role
```

Afther this change, we can just run the playbook as before, but we will see some diferences on the output of the command, you will notice that it will now show the role number

## Variable precedence
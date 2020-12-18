## Installing ansible with python-pip


1. Install the following dependencies:
   1. python3 python3-pip python3-venv
2. Create a virtual environment with python3-venv

```bash
$ python3 -m venv venv
```

3. Activate the new virtual environment

```bash
$ source venv/bin/activate
```

4. Install the ansible and paramiko libraries

```bash
$ pip install ansible paramiko
```
5. After the installation is completed, check ansible version (should return the latest version)

```bash
$ ansible --version
```

6. From here is time to perform some configuration changes to the ansible.cfg file
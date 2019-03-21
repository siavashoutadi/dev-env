# Setup a development environment

Modify the inventory file to include the hostname of the machine you want to run this playbook towards and then run the following command:

```shell
ansible-playbook site.yml -K
```
If you want to install it on your local machine then you can simply use the inventory as is and make ansible-playbook to use the local connection:

```shell
ansible-playbook site.yml --connection local -K
```

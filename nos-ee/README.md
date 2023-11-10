## Building the Execution Environment

Using [Ansible Navigator](https://ansible.readthedocs.io/projects/navigator/), execute the following command to build the Execution Environment from the root of the repository:

```shell
ansible-navigator builder build -t nos-ee
```

## Exploring the Execution Environment

Ansible Navigator can be used to explore the Execution Environment created previously. Execute the following command to navigate the contents of the Execution Environment

```shell
ansible-navigator collections --pp=missing --eei=quay.io/adetalho/nos-ee:0.0.2
```

# Raspberry Pi Management

This currently supports Ubuntu 20.04 LTS (64-bit) on Raspberry Pi 4 devices.

## Running Playbooks

Always use *syntax-check* to validate a playboks before you run it:

    ansible-playbook --syntax-check -i inventory/hosts baseline_ubuntu.yml

To carry a dry-run of a playbook, use *--check* to enable *check mode*:

    ansible-playbook --check -i inventory/hosts update_ubuntu.yml

To run a playbook:

    ansible-playbook -i inventory/hosts update_ubuntu.yml

### Playbooks

- baseline_ubuntu.yml - Standard setup for Ubuntu
- update_ubuntu.yml - Apply OS updates

## Diagnostics

To check that Ansible can successfully connect to nodes, use the *ping* module:

    ansible -m ping -i inventory/hosts all

To get the Ansible facts for nodes, use the *setup* module:

    ansible -m setup -i inventory/hosts all > all.txt

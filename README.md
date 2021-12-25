# Raspberry Pi Management

This currently supports Ubuntu 20.04 LTS (64-bit) on Raspberry Pi 4 devices.

## Setup of Controller

Install Ansible:

    pip3 --user pipx
    pipx install ansible-core

Install extra Ansible collections: 

    ansible-galaxy collection install community.general
    ansible-galaxy collection install containers.podman
    ansible-galaxy install jnv.unattended-upgrades

- [community.general](https://docs.ansible.com/ansible/latest/collections/community/general/index.html) includes *ufw*
- [containers.podman](https://docs.ansible.com/ansible/latest/collections/containers/podman/index.html) supports Podman
- [jnv.unattended-upgrades](https://galaxy.ansible.com/jnv/unattended-upgrades) for automatic updates

## Running Playbooks

Always use *syntax-check* to validate a playbook before you run it:

    ansible-playbook --syntax-check -i inventory/hosts baseline_ubuntu.yml

To carry out a dry-run of a playbook, use *--check* to enable *check mode*:

    ansible-playbook --check -i inventory/hosts update_ubuntu.yml

To run a playbook:

    ansible-playbook -i inventory/hosts update_ubuntu.yml

### Playbooks

- baseline_ubuntu.yml - Standard setup for Ubuntu
- podman_node_red.yml - Run Node-RED container
- podman_ubuntu_host.yml - Add Podman to Ubuntu
- update_ubuntu.yml - Apply OS updates

## Diagnostics

To check that Ansible can successfully connect to nodes, use the *ping* module:

    ansible -m ping -i inventory/hosts all

To get the Ansible facts for nodes, use the *setup* module:

    ansible -m setup -i inventory/hosts all > all.txt

## Resources

- [Ansible Playbook for Raspberry Pi, by Glenn K. Lockwood](https://github.com/glennklockwood/rpi-ansible)
- [Podman on Ubuntu](https://www.atlantic.net/dedicated-server-hosting/how-to-install-and-use-podman-on-ubuntu-20-04/)
- [Automate Podman with Ansible](https://www.redhat.com/sysadmin/automate-podman-ansible)

# Raspberry Pi Management

A set of Ansible playbooks to configure a Raspberry Pi. These use [Podman](https://podman.io/) for running containers on the Pi.

These playbooks currently support Ubuntu 20.04 LTS (64-bit) on Raspberry Pi 4 devices.

- **baseline_ubuntu.yml** - Standard setup for Ubuntu
- **cockpit_linux.yml** - [Cockpit](https://cockpit-project.org/) Web interface for administration
- **podman_ubuntu_host.yml** - Add [Podman](https://podman.io/) to Ubuntu
- **update_ubuntu.yml** - Apply operating system updates
- **podman_node_red.yml** - Run a [Node-RED](https://nodered.org/) container with Podman

## Setup of Controller

Use these commands to set up Ansible on the computer that will manage the Raspberry Pi devices.

Install Ansible:

    pip3 --user pipx
    pipx install ansible-core

Install extra Ansible collections: 

    ansible-galaxy collection install community.general
    ansible-galaxy collection install containers.podman
    ansible-galaxy install jnv.unattended-upgrades
    ansible-galaxy install linux-system-roles.cockpit

- [community.general](https://docs.ansible.com/ansible/latest/collections/community/general/index.html) includes support for the [ufw](https://help.ubuntu.com/community/UFW) firewall.
- [containers.podman](https://docs.ansible.com/ansible/latest/collections/containers/podman/index.html) supports Podman
- [jnv.unattended-upgrades](https://galaxy.ansible.com/jnv/unattended-upgrades) for automatic updates
- [linux-system-roles.cockpit](https://galaxy.ansible.com/linux-system-roles/cockpit) for [Cockpit](https://cockpit-project.org/)

## Running Playbooks

Always use *syntax-check* to validate a playbook before you run it:

    ansible-playbook --syntax-check -i inventory/hosts baseline_ubuntu.yml

To carry out a dry-run of a playbook, use *--check* to enable *check mode*:

    ansible-playbook --check -i inventory/hosts update_ubuntu.yml

To run a playbook:

    ansible-playbook -i inventory/hosts update_ubuntu.yml

## Diagnostics

To check that Ansible can successfully connect to nodes, use the *ping* module:

    ansible -m ping -i inventory/hosts all

To get the Ansible facts for nodes, use the *setup* module:

    ansible -m setup -i inventory/hosts all > all.txt

## Resources

- [Ansible Playbook for Raspberry Pi, by Glenn K. Lockwood](https://github.com/glennklockwood/rpi-ansible)
- [Podman on Ubuntu](https://www.atlantic.net/dedicated-server-hosting/how-to-install-and-use-podman-on-ubuntu-20-04/)
- [Automate Podman with Ansible](https://www.redhat.com/sysadmin/automate-podman-ansible)

# Ansible Playbooks

## Quick Start

Run one of the playbooks against a host:
`$ ansible-playbook basic_install.yml -i hosts -e host=raspberrypi.local`

Explanation:
`-i` Inventory file that contains all known hosts (update as needed)
`-e, --extra-var` Specify extra variables that will be used when running playbook
`host=host-name.whatever` Specify the hostname to run against


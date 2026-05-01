# Insta Setup

## Check ansible connectivity 
`ansible all -i infra/inventory/hosts.yaml -m ping`

## Configure base OS packages and env
`ansible-playbook -i infra/inventory/hosts.yaml infra/playbooks/base.yaml`
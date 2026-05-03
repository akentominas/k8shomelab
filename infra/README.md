# Insta Setup

## Check ansible connectivity 
`ansible all -i infra/inventory/hosts.yaml -m ping`

## Configure base OS packages and env
`ansible-playbook -i infra/inventory/hosts.yaml infra/playbooks/base.yaml`

## Apply basic SSH security configs
`ansible-playbook -i infra/inventory/hosts.yaml infra/playbooks/security.yaml`

## Apply system settings
- Prevent sleep when laptop screen is closed
- sysctl k8s related configs
`ansible-playbook -i infra/inventory/hosts.yaml infra/playbooks/system.yaml`

## System k8s specific settings
- Enable kernel packer forwarding (the machine will act as a router and not just a host since Pods communicate between them Pod1 (Node1) -> Node1 -> Node2 -> Pod2)
- Enable OverlayFS so container can run properly
- Enable bridge traffic to go through iptables and leverage service routing, network policies and NAT rules. `br_netfilter` enables the capability and `net.bridge.bridge-nf-call-iptables = 1` sysctl activates the behavior
`ansible-playbook -i infra/inventory/hosts.yaml infra/playbooks/k8s_prereqs.yaml`

## Install containerd
`ansible-playbook -i infra/inventory/hosts.yaml infra/playbooks/containerd.yaml`

## Install kubelet, kubeadm & kubectl

### What is included here?
- GPG key which is used to verify that packages are authentic and come with a signature
- K8S repository download
`ansible-playbook -i infra/inventory/hosts.yaml infra/playbooks/kubernetes.yaml`

### Optional - verify k8s installation
`ansible-playbook -i infra/inventory/hosts.yaml infra/playbooks/verify_k8s.yaml`

## Deploy control plane on the master node

`ansible-playbook -i infra/inventory/hosts.yaml infra/playbooks/control_plane.yaml`
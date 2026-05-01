# k8shomelab
Automating a Kubernetes cluster on repurposed hardware. Featuring a Fujitsu A514 control plane and Lenovo 330S worker nodes running Ubuntu Server.

## 💻 Laptop-Powered K8s Homelab
This repository contains the configuration, automation scripts, and documentation for my bare-metal Kubernetes cluster running on repurposed laptops.
## 🏗️ Hardware Specs
Using laptops for a homelab is a strategic choice: they come with a built-in "UPS" (the battery) and are extremely power-efficient.
Master (Control Plane) -> Fujitsu Lifebook A514 Intel Core i310GB Ubuntu Server 22.04 LTS
Worker 01 -> Lenovo Ideapad 330SIntel Core i58GBUbuntu Server 22.04 LTS
## 🛠️ The Tech Stack
Orchestration: Kubeadm.
Automation: Ansible (for OS hardening and K8s bootstrapping).
CNI: Flannel / Calico.
Load Balancer: MetalLB.
Ingress: Nginx Ingress Controller.
## 🚀 Roadmap / Implementation Steps
OS Provisioning: Minimal Ubuntu Server install on both nodes.Bootstrap: Automated SSH key distribution and system updates.Cluster Init: Initializing the Fujitsu A514 as the master node.Node Join: Connecting the Lenovo 330S to the cluster.Storage: Implementing local-path provisioner or Longhorn for persistent data.Workloads: Deploying monitoring (Grafana/Prometheus) and home automation services.

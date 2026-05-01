# SSH Setup for Kubernetes Homelab

This guide walks you through installing and configuring SSH on a server (e.g., Ubuntu) and setting up key-based authentication from your Mac for secure access.

## On the Server

### Install SSH
Update the package list and install the OpenSSH server:
```bash
sudo apt update
sudo apt install -y openssh-server
```

### Verify SSH is Running
Check the status of the SSH service:
```bash
sudo systemctl status ssh
```
Ensure it shows "active (running)".

## On Your Mac

### Generate SSH Key (if not already done)
Create a new Ed25519 key pair for the Kubernetes lab:
```bash
ssh-keygen -t ed25519 -f ~/.ssh/k8s_lab
```
Follow the prompts (you can leave the passphrase empty for simplicity, but consider security).

### Copy Public Key to Server
Transfer the public key to the server (replace `user` and `192.168.1.50` with your actual username and server IP):
```bash
ssh-copy-id -i ~/.ssh/k8s_lab.pub user@192.168.1.50
```
Enter the server's password when prompted.

### Test Login
Verify passwordless login works:
```bash
ssh -i ~/.ssh/k8s_lab user@192.168.1.50
```
You should connect without a password prompt. Type `exit` to disconnect.

This setup enables secure, automated access for further Kubernetes configurations.
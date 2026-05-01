# Set Static IP on Each Server

## 🖥️ On EACH Server

Edit the netplan config:

```bash
sudo nano /etc/netplan/01-netcfg.yaml
```

*(Your filename might differ—check `/etc/netplan/`)*

### ✏️ Example Configuration

```yaml
network:
    version: 2
    ethernets:
        enp0s31f6:   # ⚠️ Change to your interface (use `ip a`)
            dhcp4: no
            addresses:
                - 192.168.1.50/24
            routes:
                - to: default
                    via: 192.168.1.1
            nameservers:
                addresses: [8.8.8.8, 1.1.1.1]
```

### 🧠 What Each Line Means

- `dhcp4: no` → Disable router assignment
- `addresses` → Your fixed IP
- `routes` → Default gateway (router)
- `nameservers` → DNS resolution

### 🔒 Fix Permissions (Important)

```bash
sudo chmod 600 /etc/netplan/*.yaml
```

*Prevents warnings + enforces security*

### 🚀 Apply Config

```bash
sudo netplan apply
```

### ✅ Verify

```bash
ip a
ip route
```

**Expected:**

```
default via 192.168.1.1 dev enp...
```

### 🧠 Why This Matters

**Without static IP:**

- Router DHCP changes IP → Ansible breaks ❌

**With static IP:**

- Stable IP → Reliable automation ✅
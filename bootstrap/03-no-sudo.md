# Configuring Passwordless Sudo on Ubuntu Server via Ansible

This guide explains how to prevent password prompts when running `sudo` commands on an Ubuntu server using Ansible.

## Method: Using Sudoers Configuration File

Execute the following command to allow the current user to run `sudo` commands without a password:

```bash
echo "$(whoami) ALL=(ALL) NOPASSWD:ALL" | sudo tee /etc/sudoers.d/$(whoami)
```

### Breakdown:
- `echo "$(whoami) ALL=(ALL) NOPASSWD:ALL"` - Prints the sudoers rule
- `sudo tee /etc/sudoers.d/$(whoami)` - Writes the rule to a user-specific file in `/etc/sudoers.d/`

### Ansible Implementation:

```yaml
- name: Configure passwordless sudo
    lineinfile:
        path: /etc/sudoers.d/{{ ansible_user }}
        line: "{{ ansible_user }} ALL=(ALL) NOPASSWD:ALL"
        create: yes
        mode: '0440'
```

Or using the `shell` module:

```yaml
- name: Configure passwordless sudo
    shell: echo "$(whoami) ALL=(ALL) NOPASSWD:ALL" | sudo tee /etc/sudoers.d/$(whoami)
```

### Security Note:
⚠️ This configuration allows unrestricted `sudo` access without a password. Use with caution in production environments.

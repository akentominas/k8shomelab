# Install Ubuntu Server

1. Download the Ubuntu Server ISO from ubuntu.com
2. Create a bootable USB drive using balenaEtcher, Rufus, or dd
3. Boot each laptop or hardware from the USB drive
4. Follow the installer prompts:
    - choose language
    - select keyboard layout
    - configure network
    - set hostname
    - create a user account
    - set a strong password
5. Memorize or securely record the username and password for each machine
6. Repeat the process for every device you plan to use in the homelab

Notes:
- Keep credentials in a secure password manager
- Use consistent hostname naming for Kubernetes nodes
- Verify each machine boots into Ubuntu before moving on to the next step
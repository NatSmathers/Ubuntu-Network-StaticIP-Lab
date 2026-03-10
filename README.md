# Ubuntu-Network-StaticIP-Lab
Establishing a functional virtual network between two Ubuntu Linux VMs to practice static IP configuration.

# Environment & Specifications
* **Virtualization Platform**: VMware Workstation (VMnet1 Host-Only)
* **Operating System**: Ubuntu 24.04.3 LTS
* **Subnet**: 192.168.242.0/24
* **DHCP**: Disabled

---

# 1. Interface Identification
Before configuring the static IPs, I identified the active network interfaces on both virtual machines using the `ip link show` command.

* **Ubuntu-A**: ![Interface VM-A](ubuntu-a-interface-id.jpg.png)
* **Ubuntu-B**: ![Interface VM-B](ubuntu-b-interface.jpg.png)

# 2. Static IP Configuration
I edited the Netplan configuration files using `sudo nano /etc/netplan/00-installer-config.yaml` to assign static addresses.

* **Configuring VM-A (192.168.242.10)**: ![Netplan VM-A](ubuntu-a-netplan.jpg.png)
* **Configuring VM-B (192.168.242.11)**: ![Netplan VM-B](ubuntu-b-netplan-config.jpg.png)

# 3. Security Hardening
Upon applying the configuration, I received security warnings regarding loose file permissions. I restricted access to the root user only using `sudo chmod 600 /etc/netplan/*.yaml`.

* **The Conflict**: ![Security Warning](vma-netplan-security-warning.jpg.png)
* **The Fix**: ![Fixing Permissions](vma-fixing-permissions.jpg.png)

# 4. Connectivity Verification
After applying the secured Netplan configuration, I verified the local IP addresses and performed cross-network ping tests to ensure successful communication.

* **VM-A Verification**: ![VM-A Verify](ubuntu-a-verification.jpg.png)
* **VM-B Verification**: ![VM-B Verify](ubuntu-b-verification.jpg.png)
* **Ping (A to B)**: ![Ping A to B](vma-connectivity-test.jpg.png)
* **Ping (B to A)**: ![Ping B to A](vmb-connectivity-test.jpg.png)

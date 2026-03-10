# Ubuntu Linux Network & Connectivity Lab
Establishing a functional virtual network between two Ubuntu Linux VMs to practice static IP configuration.

## Environment & Specifications
* **Goal**: Establish a functional virtual network between two Ubuntu Linux VMs.
* **Platform**: VMware Workstation (VMnet1 Host-Only) using Ubuntu 24.04.3 VMs.
* **Network Type**: Host-Only (VMnet1) treated as a “sandbox” for isolation.
* **Subnet**: 192.168.242.0/24 with DHCP Disabled.

---

## 1. Interface Identification
I began by inputting the command `ip link show` to identify the active interface.

* **Ubuntu-A**: ![Interface VM-A](ubuntu-a-interface-id.jpg.png)
* **Ubuntu-B**: ![Interface VM-B](ubuntu-b-interface.jpg.png)

## 2. Static IP Configuration
I created a netplan and edited it with nano by inputting the command `sudo nano /etc/netplan/00-installer-config.yaml`.
* **VM-A**: IP Address 192.168.242.10.
* **VM-B**: IP Address 192.168.242.11.

* **Configuring VM-A**: ![Netplan VM-A](ubuntu-a-netplan.jpg.png)
* **Configuring VM-B**: ![Netplan VM-B](ubuntu-b-netplan-config.jpg.png)

## 3. Security Hardening (Problem & Solution)
I tried applying the netplan and got a warning that the permissions were too “loose” and not secure enough. The root user should be the only one with read/write permissions.

* **The Conflict**: ![Security Warning](vma-netplan-security-warning.jpg.png)

I changed the permissions by inputting `sudo chmod 600 /etc/netplan/*.yaml` and verified the correct permissions with `ls -l /etc/netplan/`.

* **The Fix**: ![Fixing Permissions](vma-fixing-permissions.jpg.png)

## 4. Connectivity Verification
I applied the netplan and verified it by inputting `ip addr` to view the correct static address. Once finished with both VMs, I pinged each one and it was a success!

* **VM-A Verification**: ![VM-A Verify](ubuntu-a-verification.jpg.png)
* **VM-B Verification**: ![VM-B Verify](ubuntu-b-verification.jpg.png)
* **Ping (A to B)**: ![Ping A to B](vma-connectivity-test.jpg.png)
* **Ping (B to A)**: ![Ping B to A](vmb-connectivity-test.jpg.png)

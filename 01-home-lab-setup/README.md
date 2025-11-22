Phase One Report — Cybersecurity Home Lab Setup

Author: Naheema Shafau  
Date: November 2025  
**Environment:** VirtualBox, Kali Linux, Metasploitable2, Windows 11 Host
---
 1. Executive Summary
This document provides a professional overview of the design, configuration, and validation of a local penetration testing lab environment. The lab simulates a realistic attacker–victim topology using Kali Linux as the offensive security platform and Metasploitable2 as the intentionally vulnerable target system.

By configuring VirtualBox networking, verifying guest connectivity, and validating host service accessibility, the lab provides a safe and isolated environment for penetration testing exercises, vulnerability research, and skill development.

---

 2. Objectives
- Deploy a **Kali Linux attacker VM**
- Deploy a **Metasploitable2 vulnerable VM**
- Configure **VirtualBox networking** correctly
- Ensure both systems are reachable and discoverable
- Validate the lab environment through connectivity and scanning

---
 3. Tools + Technologies
| Component | Purpose |
|----------|---------|
| **VirtualBox** | Hypervisor for virtual machines |
| **Kali Linux** | Attacker system (penetration testing distro) |
| **Metasploitable2** | Vulnerable target system |
| **Bridged Adapter Networking** | Places both VMs on same LAN |
| **Nmap** | Scanning & discovery |
| **Ping / ICMP** | Connectivity validation |

---

 4. Lab Topology

```
[ Windows 11 Host ]
        |
   VirtualBox
        |
-------------------------------------
|           |                      |
Kali VM  <--->  Same Network  <---> Metasploitable2 VM
-------------------------------------
```

Both VMs ultimately operated in **Bridged Adapter** mode, receiving IP addresses directly from the physical LAN, enabling:

- Ping communication  
- Nmap scanning  
- Exploitation (Phase Two)

---
5. VM Installations

5.1 Kali Linux Installation
Actions performed:
- Imported Kali ISO into VirtualBox  
- Set 4 GB RAM, 2 CPU cores  
- Created 30–40 GB virtual disk  
- Performed full graphical installation  
- Installed GRUB bootloader  
- Verified successful login into Xfce desktop environment  

5.2 Metasploitable2 Installation
Actions performed:
- Extracted `.vmdk` disk image  
- Attached disk to new VirtualBox VM  
- Allocated ~512 MB RAM  
- Disabled EFI  
- Verified Metasploitable2 terminal login screen  
- Set default credentials (`msfadmin/msfadmin`)  

---

6. Networking Configuration

6.1 Initial Issues

Early attempts using NAT and Hyper-V resulted in:
- Loopback-only IPs (`127.0.0.1`)  
- No DHCP assignment  
- No inter-VM communication  

These issues were resolved after moving **both VMs to VirtualBox Bridge Mode**.

6.2 Final Networking Mode (Working Configuration)
Adapter Mode: Bridged Adapter  
Result: Both VMs received valid LAN IPs:

- **Kali:** `192.168.1.x`  
- **Metasploitable2:** `192.168.1.141`  

---
 7. Connectivity Validation

7.1 Ping Response
Kali successfully pinged Metasploitable2:

```
ping -c 4 192.168.1.141
```

7.2 Nmap Discovery
```
nmap -sV 192.168.1.141
```

Results confirmed that the target was reachable and running multiple open ports.

This validated that the environment was ready for **Phase Two exploitation**.

---
8. Screenshots / Evidence

Recommended screenshots for GitHub:
- VirtualBox VM list  
- Network settings (Bridged mode)  
- Kali desktop after installation  
- Metasploitable2 IP address  
- Ping success  
- Nmap results  

---

 9. Conclusion
This phase successfully established a complete penetration testing environment suitable for practicing scanning, exploitation, and post-exploitation activities. The environment is isolated, stable, and designed to emulate real-world attack workflows, laying the foundation for future cybersecurity projects and professional growth.

---

*End of Report*

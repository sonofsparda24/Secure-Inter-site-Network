# Secure-Inter-site-Network
Enterprise WAN project implementing a full MPLS L3VPN architecture with MP-BGP, automatic IPsec failover, and pfSense firewall integration.

# 🚀 MPLS VPN + IPsec Failover + pfSense Firewall  
**School Project – sonofsparda**

This repository contains all configuration files, documentation, and topology resources used to build a complete enterprise-grade WAN architecture featuring:

- **MPLS L3VPN using MP-BGP**
- **CE–PE eBGP routing**
- **Automatic Failover with GRE over IPsec**
- **Firewall, NAT & DHCP using pfSense**
- **Client & Server LAN Segmentation**
- **VoIP Server (Asterisk) and FTP Server (vsftpd)**

🎯 **Goal:** Provide a scalable, secure, redundant WAN between two sites (Tunis ↔ Nabeul) using real ISP technologies.

---

## 📂 Repository Structure
- /configs-cisco → All router configs (CE / PE / Core MPLS)
- /pfsense → pfSense backup (XML)
- /documentation → Final report (PDF)
- /gns3-project → Complete GNS3 topology folder


---

# 🌐 1. Global Topology

                     +-----------------------+
                     |        Internet       |
                     +-----------+-----------+
                                 |
                           203.0.113.9
                                 |
                        +----------------+
                        |    CE-Tunis    |
                        +----------------+
                         |    |     |
                         |    |     +---- LAN Clients (pfSense LAN)
                         |    |
         MPLS CE-PE      |    +---- pfSense WAN (10.10.2.2)
                         |
                 +---------------+
                 |   PE-Tunis    |
                 +---------------+
                         |
                MPLS Backbone (OSPF + LDP)
                         |
                 +---------------+
                 |   PE-Nabeul   |
                 +---------------+
                         |
                    CE-Nabeul
                         |
               LAN Clients / Servers



---

# 🧩 2. Technologies Used

### 🔷 MPLS L3VPN (Service Provider Core)
- OSPF as IGP
- LDP for label distribution
- MP-BGP for VPNv4 routes
- VRF **HIGHTECH** for customer isolation

### 🔷 CE–PE eBGP
- CE ↔ PE link (Tunis): 172.16.1.0/30  
- CE ↔ PE link (Nabeul): 172.16.2.0/30  
- Customer routes exported into VRF via BGP

### 🔷 IPsec Failover Tunnel (GRE over IPsec)
- GRE supports routing private LANs
- IPsec encrypts GRE traffic
- Failover triggered by:
  - **IP SLA** + **Track**
  - Removes MPLS route → Activates static GRE/IPsec path

### 🔷 pfSense Firewall (Tunis Site)
- WAN: 10.10.2.2/24 (toward CE-Tunis)
- LAN-Clients: 10.50.0.0/24 (DHCP + NAT)
- LAN-Servers: 10.10.2.0/24
- DNS Forwarder
- IDS/IPS using Suricata (optional)

### 🔷 Services on Ubuntu Server
- **vsftpd** (FTP)
- **Asterisk PBX** (VoIP)

---

# 🧪 3. Verification Commands

## ✔ MPLS / LDP / OSPF
- show mpls interfaces
- show mpls forwarding-table
- show mpls ldp neighbor
- show ip ospf neighbor
- show ip route vrf HIGHTECH


## ✔ MP-BGP VPNv4
- show bgp vpnv4 unicast all
- show bgp vpnv4 unicast all summary
- show bgp vpnv4 vrf HIGHTECH


## ✔ IPsec / GRE
- show crypto isakmp sa
- show crypto ipsec sa
- show interface Tunnel10


## ✔ NAT (CE Routers)
- show ip nat translations
- show ip nat statistics
- show access-lists


---

# 🛠 4. How to Use This Project

### ✔ Import the GNS3 Topology
1. Open GNS3  
2. Import the folder `/gns3-project/`  
3. Make sure Cisco/QEMU images are correctly mapped  
4. Start routers and VMs

### ✔ Restore pfSense Configuration
pfSense → Diagnostics → Backup & Restore → Restore Config


### ✔ Start VoIP / FTP Servers
- sudo systemctl start asterisk
- sudo systemctl start vsftpd

---

# 👤 5. Author

**Youssef Nahdi (sonofsparda)**
ISET Nabeul – 2025/2026
School WAN Architecture Project  

---

# ⭐ 6. Contributing

Pull requests are welcome!  
Ideas for diagrams, scripts, automation, and improved configurations are encouraged.

---

# 📝 7. License

This project is licensed under the **GNU 3.0 Licence**.

---

# 🎨 README Graphics

Below is a collection of **ASCII diagrams**, **SVG banner designs**, and **GitHub badges** you can paste into your README.

---


![Cisco](https://img.shields.io/badge/Cisco-IOS%20Router-1a73e8?style=for-the-badge&logo=cisco)
![pfSense](https://img.shields.io/badge/pfSense-Firewall-283593?style=for-the-badge&logo=pfsense)
![GNS3](https://img.shields.io/badge/GNS3-Network%20Simulation-FF6F00?style=for-the-badge&logo=gns3)
![MPLS](https://img.shields.io/badge/MPLS-L3VPN-6f42c1?style=for-the-badge)
![IPsec](https://img.shields.io/badge/IPsec-GRE%20Tunnel-198754?style=for-the-badge)
![BGP](https://img.shields.io/badge/BGP-MP--BGP-e83e8c?style=for-the-badge)
![Ubuntu](https://img.shields.io/badge/Ubuntu-Server-dd4814?style=for-the-badge&logo=ubuntu)

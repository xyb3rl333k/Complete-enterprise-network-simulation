# Complete Enterprise Network Simulation (Goldshadow Network)

## 📌 Project Overview
This repository contains a comprehensive Cisco Packet Tracer simulation demonstrating a secure, multi-site enterprise network architecture. The project simulates a real-world corporate environment featuring a Headquarters (Admin/Servers), a Branch Office, and public internet access via an ISP, all interconnected using advanced routing and security protocols.

This project was built to showcase practical, hands-on skills in network engineering, enterprise security, and protocol implementation using Cisco IOS.

## 🛠️ Technologies & Protocols Implemented

### Routing & Switching
* **Dynamic Routing (EIGRP):** Implemented EIGRP (AS 1) for internal routing, ensuring fast convergence and scalable path selection.
* **Static Routing & Redistribution:** Configured default static routes to the ISP and successfully redistributed them into the EIGRP topology (`redistribute static`).
* **VLANs & Inter-VLAN Routing:** Segmented broadcast domains (e.g., Server LAN, Branch LAN) for logical organization and security.
* **Spanning Tree Protocol (PVST):** Prevented Layer 2 loops across the switching infrastructure.

### Enterprise Security & VPN
* **Site-to-Site VPN (GRE over IPsec):** Engineered a secure tunnel between the Headquarters and the Branch Office over the public ISP network. 
    * *Phase 1:* ISAKMP policy configuration (AES encryption, Pre-shared keys, Diffie-Hellman Group 2).
    * *Phase 2:* IPsec Transform Sets (`esp-aes esp-sha-hmac`) mapped to GRE tunnel interfaces.
* **Zone-Based Policy Firewall (ZPF):** Configured stateful firewall inspection at the network edge to protect internal LANs from outside threats while seamlessly permitting established return traffic and encrypted VPN payloads.
* **Access Control Lists (ACLs):** Deployed Extended ACLs to classify "interesting traffic" for the VPN and control NAT boundaries.
* **Layer 2 Security:** Implemented **Port Security** (Sticky MAC addresses) on access switches to mitigate unauthorized device access.

### IP Services & Addressing
* **Network Address Translation (NAT/PAT):** Configured Dynamic NAT with Overload (`ip nat inside source list ... pool ... overload`) to allow multiple internal users to share a small pool of public ISP addresses.
* **DHCP Server:** Configured Cisco routers (e.g., Amenities Router) to act as local DHCP servers, managing excluded addresses and dynamic IP allocation for end-user devices.
* **VLSM (Variable Length Subnet Masking):** Highly optimized IP addressing schema using `/32` for loopbacks, `/30` for point-to-point WAN links, and `/27` or `/28` for localized LANs to eliminate IP waste.

## 📂 Repository Structure
* `Task-2.pkt`, `Task-3.pkt`, `Task-4.pkt`: Cisco Packet Tracer simulation files detailing the progressive build-out of the network.
* `README.md`: Project documentation and technical overview.


## 💡 Key Configurations Highlight

**IPsec VPN Transform Set (ISP Router):**
```bash
crypto ipsec transform-set GRE-IPSEC esp-aes esp-sha-hmac
crypto map CMAP 10 ipsec-isakmp 
 set peer 10.0.0.1
 set transform-set GRE-IPSEC 
 match address VPN-GRE


**NAT Overload / PAT (ISP Router):**

ip nat pool NAT_POOL 202.0.0.1 202.0.0.5 netmask 255.255.255.248
ip nat inside source list NAT_BRANCHES pool NAT_POOL overload

'''bash

**🚀 How to Run the Simulation**
Download and install Cisco Packet Tracer here https://www.google.com/search?q=https://www.netacad.com/courses/packet-tracer 
Clone this repository or download the .pkt files.
Open any of the .pkt files in Packet Tracer to view the topology, inspect router configurations via the CLI, or run simulation traffic (ping, tracert) between sites.

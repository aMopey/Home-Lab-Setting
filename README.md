# Setting up a Cybersecurity Virtual Lab
**A Multi-Subnet Virtualized Environment for SOC Analysis and Penetration Testing**

## 👤 Author
**Rukayat Mopelola Lawal** *Cybersecurity Professional*

---

## 📖 Project Overview
This repository documents the end-to-end design and implementation of a professional-grade cybersecurity laboratory. The project simulates a real-world enterprise network by utilizing **pfSense** for granular firewalling and **VirtualBox** for infrastructure virtualization. 

The lab is intentionally segmented into two distinct subnets—**Operations** and **IT**—to test network isolation, cross-segment service delivery, and offensive security workflows.

## 🏗️ Network Architecture & Topology

### 1. Operations Network (Subnet A)
* **Windows Server:** Domain Controller (Active Directory), DNS, and DHCP.
* **Ubuntu Server:** Hosting organizational Web Services.
* **Client Devices:** Windows 8 instances for Sales, Audit, and HR departments.

### 2. IT & Security Network (Subnet B)
* **Offensive Platforms:** Kali Linux & Parrot OS.
* **Ubuntu Client:** General IT workstation.

### 3. Core Infrastructure
* **Firewall:** pfSense (Netgate) controlling all inter-subnet and WAN traffic.
* **Virtualization:** Oracle VM VirtualBox.

---

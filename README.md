# 🛡️ Home Virtual Cybersecurity Lab — Multi-VM SOC Environment

A fully virtualized Security Operations Center (SOC) lab built on a single home machine using free, open-source tools. Designed to simulate real-world corporate network segmentation for hands-on practice in networking, identity management, and cybersecurity.

---

## 📋 Overview

This project documents the design and implementation of a multi-subnet virtual lab featuring a dual-network architecture (Operations and IT), managed through pfSense and VirtualBox. It serves as a safe, isolated sandbox for testing firewall policies, incident response workflows, and offensive security techniques.

---

## 🧰 Tech Stack

| Component | Technology |
|---|---|
| Virtualization | Oracle VM VirtualBox |
| Firewall / Routing | pfSense (Netgate) |
| Identity Management | Windows Server (Active Directory, DNS, DHCP) |
| Operating Systems | Windows Server 2022, Windows 8, Ubuntu Server, Ubuntu Desktop |
| Security Toolkits | Kali Linux, Parrot OS |
| Network Segments | Operations Subnet & IT Subnet |

---

## 🗺️ Network Architecture

```
                        ┌─────────────┐
                        │   Internet  │
                        └──────┬──────┘
                               │
                          ┌────┴────┐
                          │ Router  │
                          └────┬────┘
                               │
                     ┌─────────┴──────────┐
                     │ Firewall (pfSense) │
                     └─────────┬──────────┘
                               │
                      ┌────────┴────────┐
                      │  Network Switch  │
                      └───┬─────────┬───┘
                          │         │
           ┌──────────────┘         └──────────────┐
           │                                        │
  ┌────────┴─────────┐                  ┌───────────┴──────────┐
  │ OPERATIONS SUBNET │                  │      IT SUBNET        │
  │  10.0.2.0/24      │                  │     10.0.3.0/24       │
  │                   │                  │                       │
  │  • Windows Server │                  │  • Kali Linux         │
  │  • Sales PC (W8)  │                  │  • Parrot OS          │
  │  • Audit PC (W8)  │                  │  • Ubuntu Server      │
  │  • HR PC (W8)     │                  │                       │
  └───────────────────┘                  └───────────────────────┘
```

### Shared Services
Windows Server and Ubuntu Server are accessible across both subnets.

---

## 🖥️ Virtual Machines

### Operations Subnet (`10.0.2.0/24`)
| VM | OS | Role |
|---|---|---|
| Windows Server | Windows Server 2022 | Domain Controller, DNS, DHCP |
| Sales Windows PC | Windows 8 | Sales department client |
| Audit Windows PC | Windows 8 | Audit department client |
| HR Windows PC | Windows 8 | HR department client |

### IT Subnet (`10.0.3.0/24`)
| VM | OS | Role |
|---|---|---|
| Kali Machine | Kali Linux | Offensive security / penetration testing |
| Parrot Machine | Parrot OS | Security research / testing |
| Ubuntu Server | Ubuntu Server | Web services, databases, containers |

---

## ⚙️ Setup Guide

### Prerequisites
- A host machine with sufficient RAM (8GB+ recommended) and storage (200GB+ free)
- [Oracle VM VirtualBox](https://www.virtualbox.org/wiki/Downloads)
- OS ISO files (see sources below)

### 1. Install VirtualBox
Download and install VirtualBox using default options. Reboot if prompted.

### 2. Create NAT Networks
In VirtualBox: **File → Preferences → Network → (+)**

| Network Name | IP Range |
|---|---|
| `operations_subnet` | `10.0.2.0/24` |
| `it_subnet` | `10.0.3.0/24` |

### 3. Create Virtual Machines
For each VM:
- **New** → set name and select ISO
- **RAM**: 1GB minimum (2GB+ recommended); **CPUs**: 2
- **Storage**: 40GB dynamically allocated VDI
- **Network**: Attach to the appropriate NAT Network

### 4. Assign VMs to Subnets
| VM | NAT Network |
|---|---|
| Windows Server, Sales PC, Audit PC, HR PC | `operations_subnet` |
| Kali Machine, Parrot Machine, Ubuntu Server | `it_subnet` |

### 5. Install Operating Systems
Boot each VM from its mounted ISO and follow the OS installer.
- **Windows Server**: Set a strong administrator password post-install
- **Windows 8 clients**: Requires a product key; create a local account per department
- **Kali Linux** (pre-built image): Default credentials are `kali` / `kali`

### 6. Verify Connectivity
```bash
# Windows
ipconfig

# Linux
ifconfig
# or
ip a
```
Each machine should receive an IP within its designated subnet range.

---

## 🌐 VirtualBox Network Types Reference

| Type | VM ↔ Internet | VM ↔ VM | Host ↔ VM | Use Case |
|---|---|---|---|---|
| NAT | ✅ | ❌ | ❌ | Single VM, internet only |
| NAT Network | ✅ | ✅ | ❌ | Multi-VM labs (used here) |
| Bridged Adapter | ✅ | ✅ | ✅ | VM visible on local network |
| Internal Network | ❌ | ✅ | ❌ | Fully isolated testing |
| Host-only Adapter | ❌ | ✅ | ✅ | Host access to VM (no internet) |

---

## 💡 Performance Tips

- Set CPU count to **2** per VM where possible
- Store VM virtual hard disks on an **SSD** for significantly faster disk I/O
- Use **dynamic allocation** for VDI files to conserve host disk space

---

## 📦 ISO Sources

| OS | Source |
|---|---|
| Windows Server 2022 | [Microsoft Evaluation Center](https://www.microsoft.com/en-us/evalcenter/) |
| Windows 8.1 | [Microsoft](https://www.microsoft.com) (product key required) |
| Kali Linux | [kali.org/get-kali](https://www.kali.org/get-kali/) |
| Parrot OS | [parrotsec.org](https://www.parrotsec.org/) |
| Ubuntu Server | [ubuntu.com/download/server](https://ubuntu.com/download/server) |

---

## 🎯 Learning Objectives

- Gain practical experience with virtualization and VM lifecycle management
- Configure and segment virtual networks using NAT Networks
- Install and administer Windows Server (Active Directory, DNS, DHCP)
- Deploy and use offensive security platforms (Kali Linux, Parrot OS)
- Build a foundation for SOC workflows, firewall policy testing, and incident response

---

## 👩‍💻 Author

**Rukayat Mopelola Lawal**  
*Version 1.0 — December 31, 2025*

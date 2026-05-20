# 🌐 Cisco Packet Tracer – Multi-Site Network Lab #4
<img width="2046" height="1142" alt="image" src="https://github.com/user-attachments/assets/876d921c-d8e6-459e-9c62-19fe06a9c0fb" />


## 📋 Overview

This Cisco Packet Tracer lab simulates a **three-site enterprise network** interconnected via a WAN backbone using **ISR4331 routers**. Each site hosts a local LAN with end-user PCs and a server. The project covers **IPv4 subnetting (VLSM)**, **inter-router WAN links**, and **multi-LAN routing** across three distinct network segments.

---

## 🗺️ Network Topology

![Network Topology](./topology.png)

```
                    ┌──────────────────────────────────────────────────┐
                    │              WAN BACKBONE (10.10.10.0/29)        │
                    │                                                  │
       10.10.10.1/29│                    10.10.10.17/29                │10.10.10.18/29
  ┌──────────────┐  │  ┌──────────────────────────────────────────┐   │  ┌──────────────┐
  │  🔵 LAN A   │  │  │                                          │   │  │  🟡 LAN B   │
  │ 192.168.1.0 │──┤  │     ISR4331          ISR4331             ├───┘  │ 192.168.2.0 │
  │    /29      │  │  │     Router0          Router1             │      │    /29      │
  └─────────────┘  │  └──────────┬──────────────────────────┬───┘      └─────────────┘
                   │             │10.10.10.6/29  10.10.10.9/29│
                   │             └──────────────┬─────────────┘
                   │                     ISR4331│
                   │                     Router2│
                   │              ┌──────────────┴──────────────┐
                   │              │         🟢 LAN C            │
                   │              │      192.168.3.0/27         │
                   │              └─────────────────────────────┘
                   └──────────────────────────────────────────────────┘
```

---

## 🏢 Site Summary

| Site   | LAN Name | Original Network    | Subnetted To        | Subnet Mask       | Default Gateway |
|--------|----------|---------------------|----------------------|-------------------|-----------------|
| 🔵 Blue | LAN A    | 192.168.1.0/24      | 192.168.1.0**/29**  | 255.255.255.248   | 192.168.1.1     |
| 🟡 Yellow | LAN B | 192.168.2.0/24      | 192.168.2.0**/29**  | 255.255.255.248   | 192.168.2.1     |
| 🟢 Green | LAN C  | 192.168.3.0/24      | 192.168.3.0**/27**  | 255.255.255.224   | 192.168.3.1     |

---

## 🖥️ Devices

### 🔵 LAN A (Blue Site)

| Device    | Model       | Hostname | Role         |
|-----------|-------------|----------|--------------|
| Router    | ISR4331     | Router0  | Site Gateway |
| Switch    | 2960-24TT   | Switch0  | Access Layer |
| PC        | PC-PT       | PC0      | End Host     |
| PC        | PC-PT       | PC1      | End Host     |
| Server    | Server-PT   | Server0  | Local Server |

### 🟡 LAN B (Yellow Site)

| Device    | Model       | Hostname | Role         |
|-----------|-------------|----------|--------------|
| Router    | ISR4331     | Router1  | Site Gateway |
| Switch    | 2960-24TT   | Switch1  | Access Layer |
| PC        | PC-PT       | PC2      | End Host     |
| PC        | PC-PT       | PC3      | End Host     |
| Server    | Server-PT   | Server1  | Local Server |

### 🟢 LAN C (Green Site)

| Device    | Model       | Hostname | Role         |
|-----------|-------------|----------|--------------|
| Router    | ISR4331     | Router2  | Site Gateway |
| Switch    | 2960-24TT   | Switch2  | Access Layer |
| PC        | PC-PT       | PC4–PC11 | End Hosts (×8)|
| Server    | Server-PT   | Server2  | Local Server |

---

## 🌍 IP Addressing Scheme

### LAN Interfaces

| Device   | Interface | IP Address      | Subnet Mask       | Network          |
|----------|-----------|-----------------|-------------------|------------------|
| Router0  | LAN port  | 192.168.1.1     | 255.255.255.248   | 192.168.1.0/29   |
| Router1  | LAN port  | 192.168.2.1     | 255.255.255.248   | 192.168.2.0/29   |
| Router2  | LAN port  | 192.168.3.1     | 255.255.255.224   | 192.168.3.0/27   |

### WAN Point-to-Point Links

| Link            | Router0 End      | Router1/2 End     | Network         |
|-----------------|------------------|-------------------|-----------------|
| Router0–Router1 | 10.10.10.18/29   | 10.10.10.17/29    | 10.10.10.16/29  |
| Router0–Router2 | 10.10.10.1/29    | 10.10.10.6/29     | 10.10.10.0/29   |
| Router1–Router2 | 10.10.10.10/29   | 10.10.10.9/29     | 10.10.10.8/29   |

### Subnetting Details

| Network          | Subnet Mask       | Usable Hosts | Usable Range                      |
|------------------|-------------------|--------------|-----------------------------------|
| 192.168.1.0/29   | 255.255.255.248   | 6 hosts      | 192.168.1.1 – 192.168.1.6         |
| 192.168.2.0/29   | 255.255.255.248   | 6 hosts      | 192.168.2.1 – 192.168.2.6         |
| 192.168.3.0/27   | 255.255.255.224   | 30 hosts     | 192.168.3.1 – 192.168.3.30        |
| 10.10.10.0/29    | 255.255.255.248   | 6 hosts      | WAN link R0–R2                    |
| 10.10.10.8/29    | 255.255.255.248   | 6 hosts      | WAN link R1–R2                    |
| 10.10.10.16/29   | 255.255.255.248   | 6 hosts      | WAN link R0–R1                    |

---

## ⚙️ Key Concepts Implemented

- ✅ **VLSM (Variable Length Subnet Masking)** — Different subnet sizes per site based on host requirements
- ✅ **Multi-Router WAN Topology** — Full mesh of 3 ISR4331 routers using /29 point-to-point links
- ✅ **Inter-LAN Routing** — Routing between three independent LAN segments
- ✅ **Static / Dynamic Routing** — Routes configured across all three routers
- ✅ **Layered Network Design** — Separate LAN and WAN addressing spaces
- ✅ **Server Infrastructure** — Dedicated Server-PT in each site

---

## 🚀 Getting Started

### Prerequisites

- [Cisco Packet Tracer](https://www.netacad.com/resources/lab-downloads) **7.x or 8.x**
- Free Cisco NetAcad account

### Open the Lab

```bash
git clone https://github.com/your-username/your-repo-name.git
cd your-repo-name
```

Then in Packet Tracer: **File → Open → `packet_tracer-4.pkt`**

---

## 🧪 Verification Commands

Run these on each router's CLI to verify the setup:

```bash
# Check routing table
show ip route

# Verify interfaces are up
show ip interface brief

# Check running config
show running-config
```

**Connectivity test from any PC:**
```
# Ping across sites (LAN A → LAN B)
ping 192.168.2.x

# Ping across sites (LAN A → LAN C)
ping 192.168.3.x

# Traceroute to verify path
tracert 192.168.3.1
```

---

## 📁 Repository Structure

```
📦 packet-tracer-lab-4/
├── 📄 packet_tracer-4.pkt    # Packet Tracer simulation file
├── 📄 README.md              # This file
└── 📷 topology.png           # Network diagram screenshot
```

---

## 👤 Author

**Your Name**
- GitHub: https://github.com/yuvagiridharan/cisco-3router-topology

---

*Built with Cisco Packet Tracer as part of a Networking course.*

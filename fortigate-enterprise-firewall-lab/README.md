# Enterprise FortiGate Firewall Deployment & Traffic Segmentation Lab

## Executive Summary
This repository documents the end-to-end deployment, network segmentation, and security hardening of an enterprise FortiGate Next-Generation Firewall (FortiOS v6.2.4). The objective of this project is to establish baseline network perimeters, configure secure management plane access, establish static default routing, integrate Unified Threat Management (UTM) profiles, and transition from open access rules to granular IPv4 policies adhering to the **Principle of Least Privilege**.

---

## Technical Environment Summary
* **Firewall Hostname:** `Sabik-Lab-FortiGate`
* **Firmware Version:** FortiOS v6.2.4 build6762
* **WAN Interface (`port15`):** `192.168.0.100/24` | Gateway: `192.168.0.2`
* **LAN Subnet (`lan`):** Hardware Switch (`port1`–`port14`) | IP: `10.1.1.1/24`
* **DHCP Scope:** `10.1.1.100` – `10.1.1.254` | Primary DNS: `8.8.8.8`
* **Routing:** Static Default Route (`0.0.0.0/0`) via Egress WAN

---

## Modular Documentation Index

Each core configuration phase is documented in detail within the `/docs` directory. Click a section below to review the technical breakdown, network parameters, and supporting CLI/GUI screenshots:

1. **[Dashboard Overview and Interface Mapping](docs/dashboard-and-interfaces.md)**
   System health audit, licensing verification, and physical/logical interface hierarchy mapping.

2. **[WAN Configuration & Management Isolation](docs/wan-setup.md)**
   External interface IP assignment, static default gateway parameters, and administrative protocol control (HTTPS/SSH/PING).

3. **[LAN Switch & Internal DHCP Provisioning](docs/lan-setup.md)**
   Hardware switch interface aggregation, internal gateway allocation, and automated DHCP scope setup broadcasting public DNS.

4. **[Static Default Route Configuration](docs/static-route.md)**
   Egress routing engine configuration directing non-local subnets toward the ISP next-hop.

5. **[Granular Policies & Security Profiles](docs/policies.md)**
   Transition from broad `LAN-ALL` rules to service-specific granular rules (DNS, Web, Mail) with attached Antivirus, Web Filter, and Application Control profiles.

6. **[FortiView Traffic Inspection & SOC Triage](docs/fortiview-analysis.md)**
   Operational traffic triage, host session tracking (`10.1.1.10`), and application destination auditing.

---

## Key SOC Analysis Takeaways
* **Least Privilege Enforcement:** Phased out broad `ANY-ANY` rules by implementing strict service-specific policies (Ports 53, 80/443, and Email protocols) to restrict lateral movement and unauthorized egress.
* **Management Plane Hardening:** Isolated administrative management controls (HTTPS/SSH) to secure channels, preventing clear-text credential exposure across untrusted segments.
* **Deep Packet Inspection & Visibility:** Integrated UTM profiles with live FortiView monitoring to ensure real-time threat hunting and payload inspection for passing network sessions.

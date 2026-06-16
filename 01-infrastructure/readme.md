# 01. Infrastructure

## Overview

This section documents the physical infrastructure and virtualization platform used throughout the HomeLab environment.

The lab is designed around low power consumption, security, and enterprise-inspired architecture while remaining practical for a home environment.

---

## Table of Contents

* [Hardware Overview](#hardware-overview)
* [Physical Architecture](#physical-architecture)
* [Switch Port Plan](#switch-port-plan)
* [Design Goals](#design-goals)

---

## Hardware Overview

<p align="center">
<img src="./screenshots/homelab.jpeg" width="750">
</p>
<p align="center">
<i>Figure: Physical HomeLab infrastructure</i>
</p>

---

| Device	| Purpose | 
| --|--|
| Fujitsu D3544-S	| Dedicated OPNsense Firewall | 
| Lenovo ThinkCentre M710q Tiny	| ESXi Host 01 | 
| Lenovo ThinkCentre M710q Tiny	| ESXi Host 02 | 
| TP-Link TL-SG108E Managed Switch	| VLAN-capable Layer 2 Switch | 
| Tecmojo 10” Mini Rack (6U)	| Rack enclosure | 
| DIGITUS 4-Port Power Strip (1U)	| Rack-mounted power distribution | 

---

## Physical Architecture

| System | Platform | Role |
|----------|----------|----------|
| OPNsense Firewall | Bare Metal | Routing, Firewall, DHCP, VPN, Network Segmentation |
| ESXi Host 01 | VMware ESXi | DC01 (Active Directory, DNS, Group Policy, AD CS), HR01 (Domain-Joined Client) |
| ESXi Host 02 | VMware ESXi | MON01 (Checkmk Monitoring Server) |

---

## Switch Port Plan

*TP-Link TL-SG108E*

| Port | Connected Device | Purpose |
|------|------------------|----------|
| 1 | ISP Router | WAN |
| 2 | NAS | Home Network |
| 3 | OPNsense WAN | WAN |
| 4 | OPNsense LAN | VLAN Trunk |
| 5 | ESXi 01 - NIC 1 | VLAN Trunk |
| 6 | ESXi 01 - NIC 2 | VLAN Trunk |
| 7 | ESXi 02 - NIC 1 | VLAN Trunk |
| 8 | ESXi 02 - NIC 2 | VLAN Trunk |

⸻

## Design Goals

The HomeLab is designed around:

* Security-first architecture
* Network segmentation
* Low power consumption
* Enterprise-inspired administration
* Windows infrastructure management
* Monitoring and operational visibility

The environment serves as a platform for learning and documenting practical infrastructure concepts including Active Directory, Group Policy, certificate services, firewall management, monitoring, and network security.
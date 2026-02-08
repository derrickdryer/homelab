# Hardware Overview

> [“Buy once, cry once.”](https://youtu.be/p8Fa7keyXPU?si=BJ0E22GUtEMtmJrS) 
> — [TechnoTim](https://www.youtube.com/@TechnoTim)

This document provides an overview of the physical hardware that makes up the homelab.  
It is organized by functional role rather than physical placement.

## Networking

Hardware responsible for connectivity, routing, switching, and wireless access across the homelab.

### Edge & Routing

- [**UniFi Cable Internet Modem**](https://store.ui.com/us/en/category/accessories-installations/products/uci)

  - Role: Cable modem for ISP connectivity
  - Description:

    - Multi-gigabit, rack-mountable cable modem with integrated connection monitoring

- [**UniFi Dream Machine Pro Max**](https://store.ui.com/us/en/category/all-cloud-gateways/products/udm-pro-max)

  - Role: Primary gateway, firewall, and network controller
  - Description:

    - 10G cloud gateway with advanced routing, firewalling, and UniFi management

  - Notes:

    - Serves as the central control plane for all UniFi networking equipment

### Switching

- [**UniFi Pro XG 24 PoE Switch**](https://store.ui.com/us/en/category/all-switching/products/usw-pro-xg-24-poe)

  - Role: Core aggregation switch for multi-gigabit devices
  - Description:

    - 24-port 10-gigabit PoE switch for high-performance networking and power delivery

- [**UniFi Pro 8 PoE Switch**](https://store.ui.com/us/en/category/all-switching/products/usw-pro-8-poe)

  - Role: Access switch for PoE-powered 1 GbE devices
  - Description:

    - 8-port managed PoE switch for connecting access points, IoT devices, and edge equipment

### Wireless

- [**UniFi U7 Pro XG**](https://store.ui.com/us/en/category/all-wifi/products/u7-pro-xgs)

  - Role: Primary wireless access point
  - Description:

    - High-performance Wi-Fi access point for trusted, guest, and IoT wireless networks

## Compute

Systems responsible for running virtual machines, containers, and clustered workloads across the homelab.

### Virtualization Hosts

- [**GMKtec AI Mini PC Ultra 9 285H**](https://a.co/d/0imZTpr2)

  - Role: Primary virtualization host
  - Description:

    - High-performance x64 mini PC used for compute-intensive workloads

  - Configuration:

    - 96 GB DDR5 RAM
    - 3× 2 TB NVMe SSD

  - Operating System:

    - [Proxmox VE](https://www.proxmox.com/en/)

- [**GMKtec Mini PC M7 Ultra (Ryzen 7 PRO 6850U)**](https://a.co/d/0162H3vL)

  - Role: Secondary virtualization host
  - Description:

    - x64 mini PC used for additional VM capacity and redundancy

  - Configuration:

    - 32 GB DDR5 RAM
    - 2× 2 TB NVMe SSD

  - Operating System:

    - [Proxmox VE](https://www.proxmox.com/en/)

### Cluster Nodes

- [**Raspberry Pi 5 (8 GB) ×3**](https://www.raspberrypi.com/products/raspberry-pi-5/)

  - Role: ARM-based cluster nodes
  - Description:

    - ARM systems used for lightweight services and clustered workloads

  - Configuration:

    - 8 GB RAM each
    - 1 TB NVMe SSD per node
    - [Waveshare PoE M.2 HAT+ (B)](https://a.co/d/0fKBlTgM)

  - Operating System:

    - [Raspberry Pi OS Lite (64-bit)](https://www.raspberrypi.com/software/operating-systems/)

## Storage

### Network Attached Storage

- [**UGREEN DXP6800 Pro**](https://nas.ugreen.com/products/ugreen-nasync-dxp6800-pro-nas-storage)

  - Role: Primary NAS and storage server
  - Description:

    - 6-bay NAS platform used for centralized storage and data services

  - Operating System:

    - [TrueNAS](https://www.truenas.com/)

#### Expansion & Controllers

- [**GLOTRENDS PA20 Dual M.2 NVMe to PCIe Adapter**](https://a.co/d/0bEmxtwH)

  - Role: NVMe expansion via PCIe
  - Description:

    - Dual M.2 NVMe adapter utilizing PCIe 3.0 x4 with bifurcation support

#### Storage Media

##### NVMe SSDs

- [**Western Digital WD Red SN700 – 1 TB (x2)**](https://a.co/d/0cxrQulW)

  - Role: High-endurance NVMe storage
  - Description:

    - NAS-rated NVMe SSDs designed for sustained workloads

- [**Crucial P3 PCIe Gen3 NVMe – 2 TB (x2)**](https://a.co/d/0dcssEQf)

  - Role: General-purpose NVMe storage
  - Description:

    - PCIe Gen3 NVMe SSDs used for high-speed storage workloads

##### HDDs

- [**Seagate IronWolf Pro – 8 TB (x6)**](https://a.co/d/0cPn3AK8)

  - Role: Primary bulk storage
  - Description:

    - NAS-grade HDDs designed for reliability and continuous operation

#### Memory

- [**Crucial 64 GB DDR5 RAM Kit (2×32 GB)**](https://a.co/d/06Mqu9aV)

  - Role: System memory for NAS and ZFS workloads
  - Description:

    - DDR5 4800 MHz CL40 laptop memory kit

## Environmental & Rack Infrastructure

Supporting hardware responsible for power stability, physical organization, and environmental control of the homelab.

### Power Protection

- [**CyberPower CP2000PFCRM2U PFC Sinewave UPS**](https://a.co/d/0hqBAxmx)

  - Role: Primary UPS for rack-mounted equipment
  - Description:

    - Rack-mountable PFC sinewave UPS providing battery-backed power and surge protection

### Rack & Physical Infrastructure

- [**SYSRACKS SRF 27.6.9 G (27U Cabinet)**](https://sysracks.com/product/27u-35-depth-24x35x57-19-it-telecom-cabinet-sysracks-srf-27-6-9-g/)

  - Role: Primary server rack and physical enclosure
  - Description:

    - 27U enclosed IT and telecom cabinet with front-to-back airflow

  - Specifications:

    - 27U height
    - 35" depth
    - 19" rack standard

## Notes & Future Changes

This hardware inventory evolves over time as components are upgraded, replaced, or retired.

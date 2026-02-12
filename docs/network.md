# Network Architecture

The homelab network is built around strong service separation using VLANs and UniFi zone-based firewall policies.  
Rather than relying on a single trusted network, services are grouped by trust level and function to reduce risk and limit lateral movement.

The goal is simple:

- Separate workloads by purpose
- Minimize unnecessary communication between networks
- Allow only intentional, controlled access paths

## Design Philosophy

The network follows a **zero-trust-inspired layout** where devices and services operate inside clearly defined network boundaries.

Key principles:

- VLANs separate traffic at Layer 2
- Zone firewall rules control Layer 3 communication
- Public services live in isolated networks
- IoT and wireless devices are treated as untrusted by default
- Access is initiated intentionally rather than implicitly allowed

## VLAN Overview

| Name | VLAN | Subnet | Purpose |
| --- | --- | --- | --- |
| Management | 1 | 10.102.1.0/24 | Network management and infrastructure (UniFi Required) |
| Private LAN | 10 | 10.102.10.0/24 | Trusted personal devices |
| Homelab | 20 | 10.102.20.0/24 | Servers, compute, and lab services |
| Public | 30 | 10.102.30.0/24 | Public-facing services (DMZ) |
| Surveillance | 40 | 10.102.40.0/24 | Cameras and isolated recording systems |
| IoT | 50 | 10.102.50.0/24 | Smart home and untrusted devices |
| Guest | 60 | 10.102.60.0/24 | Guest wireless access |

## Zone-Based Firewall Model

UniFi zones simplify firewall management by grouping networks based on trust level.

### Internal Zone

- Management

- Private LAN

Highly trusted devices capable of initiating connections outward.

### Homelab Zone

- Homelab VLAN

Dedicated to infrastructure services, virtualization hosts, and internal workloads.

### DMZ (Public)

- Public VLAN

Used for externally exposed services such as game servers and public applications.

**Security Model:**

- DMZ services cannot initiate connections to Internal networks.
- Internal users may access DMZ resources when needed.
- Return traffic is allowed for established sessions.

This prevents exposed systems from reaching back into trusted environments.

### Untrusted (Internet)

- IoT VLAN

IoT devices are isolated from internal services and are treated as internet-only clients whenever possible.

### Untrusted (No Internet)

- Surveillance VLAN

Camera systems are isolated and restricted from outbound internet access.

### Hotspot

- Guest VLAN

Guest devices receive internet access without visibility into internal networks.

## Public Services (DMZ Strategy)

Public-facing services such as game servers are intentionally placed inside the **Public VLAN**.

Design goals:

- Public workloads remain isolated from trusted LAN devices
- Compromised services cannot pivot into internal infrastructure
- Only return traffic is permitted when initiated by trusted users

Traffic flow example:

- External → Public VLAN: Allowed
- Public VLAN → Internal LAN: Blocked
- Internal LAN → Public VLAN: Allowed
- Return traffic: Allowed

This mirrors traditional enterprise DMZ design.

## IoT Segmentation

IoT devices are separated into their own VLAN and wireless network.

Reasons for isolation:

- Many IoT devices have limited security controls
- Vendor firmware may introduce unknown risks
- Network segmentation reduces blast radius

Controls in place:

- IoT devices cannot reach Internal or Homelab networks
- Wireless IoT SSIDs map directly to the IoT VLAN
- Firewall rules restrict lateral movement

## Wireless Segmentation

Wireless networks mirror wired VLAN separation.
*NOTE: Not my actual SSID names due to security concerns*

Each SSID maps to a dedicated network:

- Trusted Wi-Fi → Private LAN
- IoT Wi-Fi → IoT VLAN
- Guest Wi-Fi → Guest VLAN

This ensures wireless devices follow the same security boundaries as wired devices.

## Routing & Gateway

All routing, firewalling, and zone enforcement is handled by the **UniFi Dream Machine Pro Max**.

Responsibilities include:

- Inter-VLAN routing
- Zone-based firewall policies
- WAN connectivity
- VPN and external access controls

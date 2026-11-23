# E-Commerce Logistics System Network Design

## Overview
This project presents a robust and scalable enterprise network architecture designed for an E-Commerce Logistics System. Built and simulated using Cisco Packet Tracer, the network connects six distinct operational centers, ensuring seamless internal communication, centralized service access, automated IP provisioning, and resilient routing with failover capabilities.

## 🗺️ Network Topology
![E-Commerce Logistics Network Topology](./Labeled%20Topology%20Diagram.png)

## Operational Centers
The network topology interconnects the following six operational hubs:
*   **MOH (Main Operations Hub):** Core routing hub hosting the DNS Server and an Email Server.
*   **CSC (Customer Support Center):** Hosts the central Web Server (`www.orders.local`), a dedicated DHCP server, and acts as the primary email relay.
*   **WHC (Warehouse Center):** Features router-based DHCP and a redundant backup link to the CSC.
*   **DDU (Delivery Dispatch Unit):** Acts as an intermediate routing node featuring router-based DHCP.
*   **DPU (Data Processing Unit):** Statically addressed end-point utilizing recursive routing.
*   **RPP (Regional Pickup Point):** Statically addressed edge network utilizing default and exit-interface routing.

## Key Technologies & Protocols
*   **IP Addressing:** Variable Length Subnet Masking (VLSM) is utilized to efficiently subnet a `/16` base network across all LANs and point-to-point WAN links.
*   **Dynamic Routing:** RIPv2 is implemented across the core routers (MOH, WHC, DDU, CSC) to dynamically exchange routes.
*   **Advanced Static Routing:** 
    *   **Floating Static Route:** Configured on the backup link between WHC and CSC to automatically take over if the primary dynamic path fails.
    *   **Recursive Static Routing:** Implemented to allow edge nodes (DPU) to reach distant networks (RPP) via multiple hops.
    *   **Default & Exit-Interface Routing:** Used for simplified edge-router configuration.
*   **Route Redistribution:** Static routes are redistributed into the RIPv2 domain at the Main Operations Hub to ensure full network reachability.
*   **Network Services:** Integrated Web (HTTP), DNS, Email (SMTP/POP3), and DHCP services. 

## High Availability & Redundancy
The network is designed with fault tolerance in mind. A backup direct link between the Warehouse Center (WHC) and the Customer Support Center (CSC) is configured with a floating static route (higher administrative distance than RIPv2). If the primary network path goes down, traffic is automatically rerouted through the backup link without manual intervention.

## Repository Contents
*   `E-COMMERCE LOGISTICS SYSTEM NETWORK DESIGN.pkt`: The main Cisco Packet Tracer simulation file.
*   `Labeled Topology Diagram.png`: A high-resolution visual map of the network architecture.
*   `VLSM_IP Table_Config.pdf`: Complete documentation containing the VLSM tree, exhaustive IP addressing tables for all devices, and the raw CLI configuration commands for every router.

## How to Run
1. Download and install **Cisco Packet Tracer**.
2. Clone or download this repository to your local machine.
3. Open the `.pkt` file in Cisco Packet Tracer.
4. Allow a few moments for the STP (Spanning Tree Protocol) and RIPv2 routing tables to converge (link lights will turn green).
5. Use the PC command prompts to `ping` across the network or use the web browsers to access `www.orders.local`.

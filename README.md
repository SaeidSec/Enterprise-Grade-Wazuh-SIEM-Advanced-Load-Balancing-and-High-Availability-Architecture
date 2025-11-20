# Enterprise-Grade-Wazuh-SIEM-Advanced-Load-Balancing-and-High-Availability-Architecture
A resilient, enterprise-grade Wazuh SIEM architecture featuring advanced load balancing, multi-node clustering, and high-availability design. Ensures continuous log ingestion, fault tolerance, scalable performance, and reliable threat detection across distributed environments.

📌 Overview

This project demonstrates how to architect a fault-tolerant, scalable, and high-performance Wazuh SIEM using:

Active-Passive failover (HAProxy + Keepalived)

Active-Active load distribution across the Wazuh Manager cluster

Nginx Stream for high-speed TCP load balancing

Distributed Wazuh Indexer cluster for data redundancy

Redundant dashboard nodes for uninterrupted SOC visibility

The architecture is designed to survive node failures, traffic spikes, update cycles, and storage outages without losing event data or breaking agent connectivity.

🏗️ Architecture Zones

The deployment is structured into four isolated zones:

1. DMZ Zone (Perimeter)

Load balancers receive all external agent communication and distribute traffic intelligently.

2. Management Zone (Processing)

Wazuh Manager cluster (Master + Worker) handles:

Agent registration

Rule evaluation

Log processing

Alert generation

3. Data Zone (Storage & Indexing)

A multi-node Indexer cluster ensures:

Data replication

High query performance

Strong search reliability

4. Presentation Zone (UI Layer)

Wazuh Dashboard nodes provide:

Real-time visualization

Threat analysis

Alert management

⚙️ Key Components
Wazuh Manager Cluster

Master Node: 192.168.0.104

Worker Node: 192.168.0.201

Fully distributed, Active-Active processing

Cluster communication validated using ossec.conf and cluster logs

Indexer Cluster

Primary Indexer: 192.168.0.200

Replica Indexer: 192.168.0.203

Provides data redundancy with automatic node failover

🔁 High Availability & Load Balancing
1. Dual-Layer LB Strategy

Nginx Stream: High-speed TCP forwarding (Port 1514)

HAProxy: Layer 4/7 intelligent balancing for API & dashboard

2. Active-Passive Failover (HAProxy + Keepalived)

Virtual IP: 192.168.0.10

Instant failover if the primary LB goes down

Zero disruption for connected agents

3. Active-Active Manager Failover

Traffic is distributed across both Manager nodes, enabled via:

Round-robin

Least connections

Health-based routing

If one manager stops, the other instantly takes over.

🧪 Validation & Testing
✔ Agent Connectivity

Agents were deployed on:

Windows 11

Linux

Both streamed logs successfully through the full pipeline:
Agent → LB → Manager → Indexer → Dashboard

✔ Zero-Downtime Failover Test

Scenario: Master Node taken offline
Result:

No agent was disconnected

Traffic dynamically rerouted to Worker

Ingestion continued without interruption

This confirms genuine enterprise-grade resilience.

📦 Features

Zero-downtime architecture

Horizontal scalability

Strong fault tolerance at every layer

TLS-secured communication

Clean separation of zones

Resilient multi-node indexer configuration

Production-validated failover

📚 Documentation

Full architecture, diagrams, and verification screenshots are included in the attached PDF:

Architecting Resilience: A Deep Dive into Enterprise-Grade Wazuh SIEM with Advanced Load Balancing and High-Availability


Architecting Resilience_ A Deep…

👤 Author

Abu Saeid
Email: contact.abusaeid598@gmail.com

Phone: +8801752791256

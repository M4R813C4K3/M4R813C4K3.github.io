---
title: "Project: Value Engineering via Repurposed Enterprise Hardware"
date: 2025-06-21 12:00:00 -0500
categories: [Enthusiast-Projects]
tags: [lenovo, minecraft, linux, asset-reclamation, optimization, java, virtualization]
description: Repurposing decommissioned Lenovo Tiny hardware into a high-availability game server to achieve near-zero hardware overhead.
---

## Overview
This project focuses on the reclamation and optimization of a decommissioned **Lenovo ThinkCentre M90q Tiny** into a dedicated, high-performance Minecraft server. The objective was to demonstrate the feasibility of utilizing "end-of-life" enterprise assets to provide production-grade hosting services with minimal capital investment.

## The Business Case: TCO and Asset Reclamation
By repurposing a unit slated for decommissioning, the hardware cost was effectively zero, shifting the project focus toward software-defined optimization.

* **Capital Expenditure (CapEx):** $20 USD (Lifetime AMP License by CubeCoders).
* **Asset Value:** Reclaimed an enterprise-grade USFF node with an estimated market value of $150+ CAD.
* **Operating Expenditure (OpEx):** Calculated power consumption at idle/load results in an estimated monthly cost of $2 CAD.
* **Economic Benefit:** Achieved a hosting environment equivalent to commercial cloud providers ($40+/month) with a total first-year cost of approximately $44 CAD.

## Technical Specifications
* **Host Hardware:** Lenovo ThinkCentre M90q Tiny (Gen 1).
* **CPU:** Intel Core i5-10500T (6 Cores / 12 Threads).
* **Memory:** 32GB DDR4 2933MHz.
* **Storage:** 512GB NVMe Gen3 SSD.
* **OS:** Ubuntu Server 24.04 LTS (Headless).
* **Orchestration:** AMP (Application Management Panel).

## Implementation Methodology

### 1. OS Hardening and Remote Management
A minimal Ubuntu Server installation was utilized to ensure maximum system interrupts were available for the Java Virtual Machine. 
* **Management:** Management was conducted via SSH and the AMP web interface, allowing for headless operation within a network closet.
* **Security:** Implemented localized firewall rules (UFW) and configured specific port forwarding rules at the gateway level to isolate the server traffic.

### 2. JVM and Application Layer Optimization
To ensure a stable 20 TPS (Ticks Per Second) environment, the Java runtime required specific tuning to handle the high-frequency tick calculations inherent to Minecraft.
* **JVM Arguments:** Implemented **Aikar’s Flags** for garbage collection (GC) optimization. This minimized "Stop-the-World" pauses that typically cause intermittent lag spikes.
* **Memory Management:** Allocated a fixed **12GB heap size** (`-Xms12G -Xmx12G`) to prevent the CPU spikes associated with dynamic memory allocation and ballooning.



### 3. Thermal and Lifecycle Management
USFF (Ultra-Small Form Factor) hardware requires careful monitoring when repurposed for 24/7 high-load applications.
* **Thermals:** The system maintains a stable **65°C** under sustained load.
* **Persistence:** Created a systemd service unit to ensure the AMP instance and underlying Minecraft server initialize automatically upon power restoration.

## Outcome
The project resulted in a high-availability node that provides the same performance metrics as dedicated enterprise hosting. This deployment demonstrates proficiency in **Hardware Lifecycle Management**, **Linux Server Administration**, and **Financial Optimization**, proving that decommissioned assets can be successfully engineered into high-value infrastructure.

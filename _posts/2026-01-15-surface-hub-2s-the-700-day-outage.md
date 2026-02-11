---
title: "Operations: The 700-Day Outage — A Forensic Recovery Saga"
date: 2026-01-15 11:00:00 -0500
categories: [Operations-Deployment]
tags: [microsoft, surface-hub, mtr, vendor-management, forensic-recovery, hardware-diagnostics, project-management]
description: A multi-year investigation into systemic vendor failure, malicious compliance, and the rescue of a $10,000 executive asset.
---

## Overview
When I joined the organization in July 2024, I inherited an expensive piece of "wall art": a **Microsoft Surface Hub 2S** that had been non-functional for over 700 days. This asset predated my tenure and had effectively fallen off the organizational radar—likely omitted from Intune metrics to avoid negatively impacting UCC availability data. 

This is the exhaustive documentation of how I broke an 18-month vendor stalemate, bypassed a third-party support loop in Nicaragua, and finally forced a resolution from Microsoft’s US Head Office using high-speed video forensics and malicious compliance.

## The Cycle of Insanity (July 2024 – Early 2025)
For the first several months, I operated within the established "fix" cycles. The device would undergo a standard re-image, function for a week or two, and then predictably collapse back into a BitLocker recovery screen or a terminal Blue Screen of Death (BSOD). Every technician before me had either abandoned the ticket or ignored it because it sat outside their direct responsibility.

### The Hardware Gaslight
In early 2025, Microsoft Support (offshore) mandated a physical SSD re-image. They provided a "required" shopping list of third-party SATA-to-USB adapters, specifically the **StarTech USB312SAT3CB**. 

* **The Procurement:** I sourced the $20 adapter and waited weeks for delivery and internal approvals.
* **The Realization:** When the "official" guide arrived, I immediately identified a major red flag. Drawing on my prior experience with **Surface Hub V1** units (which featured a discrete SSD hatch), I realized the guide was for the wrong hardware revision. 
* **The Conflict:** Our **2S model** utilized a modular compute cartridge with no external hatch. When I pointed this out, support never acknowledged the error; they simply moved the goalposts and asked me to "try a standard USB re-image again."

## The 88% Wall & Malicious Compliance (Late 2025)
By late 2025, the fleet-wide migration to **Windows 11 IoT** was underway. Out of 300+ units, this device became a terminal "straggler." The migration launcher would execute, initialize, and then consistently hard-crash at exactly **88% completion**.

### The "Alibi" Camera
Internal UCC teams theorized that the migration was failing because I "wasn't sticking around to tap the screen" and keep the device awake. While I knew that UEFI-level recovery doesn't respect OS sleep timers, I turned to **Malicious Compliance** to silence the critics.

* **The Setup:** I staged an **iPhone** on a tripod to record the entire process.
* **The Proof:** I recorded myself physically standing by the unit for hours, tapping the screen every 4–5 minutes to satisfy the UCC team’s theory. 
* **The Forensic Catch:** When the unit inevitably crashed at 88% again, I had the evidence. By scrubbing the high-frame-rate video, I caught the split-second BSOD: **MEMORY_MANAGEMENT**. 
* **The Smoking Gun:** I backed this up with **Event Viewer** logs showing thousands of entries for that specific stop code. It was no longer a "user error" discussion; it was a documented hardware-firmware conflict.



## The Escalation: Nicaragua to Redmond (December 2025)
The project reached a turning point in December. While the rest of the team was "at the water cooler" or on holiday, I remained the only point of contact for the escalating ticket. 

* **The "Ghost" Call:** I received a direct Teams call from a US-based Microsoft manager. 
* **The Admission:** He had inherited the ticket and found **zero internal notes** from the previous 18 months of offshore support (Concentrix, Nicaragua). He had no idea what had been tried or why the unit was still down.
* **The Resolution:** After I provided the full forensic history, the timeline of misdirection, and the failure of the **SEMM (Surface Enterprise Management Mode)** certificate method, Microsoft finally conceded. 

## Outcome
After being down for over **700 days**, the Surface Hub 2S was finally stabilized. The diagnostic forced Microsoft to move past their standard "re-image it again" scripts, eventually leading to a hardware resolution that brought the unit back into the executive boardroom.

**Key Takeaways:**
1. **Persistence is a Technical Skill:** Technical knowledge is useless without the grit to hold vendors accountable for 18 months.
2. **Document the "Insanity":** When a process fails at 88% five times in a row, you aren't fighting a software bug; you're fighting a systemic failure.
3. **Forensic Initiative:** Using unconventional tools (like iPhone surveillance) can be the only way to catch "invisible" system crashes that standard logs miss.

---

**Status:** Production Stable (January 2026)
**Total Downtime:** ~740 Days
**Resolution:** Successful migration to Windows 11 IoT / MTR Pro.

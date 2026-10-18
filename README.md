# ECI Voter Roll Accountability & Fast-Track Restoration Portal

## 📌 Project Overview
🟢 Live Interactive Demo: https://deebong.github.io/eci-sir-restoration-portal/

This repository contains a functional frontend prototype and technical architecture proposal designed for the **Election Commission of India (ECI) IT Cell**. The platform aims to resolve the widespread administrative gridlock caused by the Special Intensive Revision (SIR) by providing an expedited, transparent digital pathway for erroneously deleted voters to audit their status and request immediate restoration without losing their electoral history[cite: 20, 21].

## ⚠️ The Problem: Systemic Bottlenecks in the SIR Process
The Special Intensive Revision (SIR) resulted in the deletion of roughly 130 million names from India's electoral rolls[cite: 7]. This automated cleanup created severe operational and civic challenges:

* **Lack of Public Transparency (The "Why Was I Deleted?" Problem):** The current National Electoral Search only returns a binary "Found/Not Found" status, failing to communicate the technical rationale (e.g., auto-flagged as absent/shifted) or the authorizing Electoral Registration Officer (ERO)[cite: 20]. 
* **The Form 6 Legal Contradiction:** ECI portals currently route deleted individuals to Form 6, which is legally restricted to brand-new, first-time voters[cite: 14, 20]. Forcing existing voters to sign this form scrubs their historical voting longevity and requires them to legally declare they have never voted before[cite: 14, 20].
* **The Manual Verification Lock:** Automated software generated tens of thousands of deletion forms without providing administrative reasons, forcing local officers to sign them[cite: 13]. Correcting these via manual Booth Level Officer (BLO) spot-checks cannot scale to meet election deadlines[cite: 20].

## 💡 The Solution: Expedited Remediation Architecture
This tool introduces an isolated **Fast-Track Restoration API layer** within the existing ECI ERONET infrastructure[cite: 20]. 

### Core Features
1. **Granular Audit Trail:** Pulls data from the ECI archival log to show the voter the exact technical reason they were purged (e.g., algorithmic demographic multi-match, absent/shifted flag)[cite: 15].
2. **Identity Verification Gateway:** Integrates a secure Aadhaar/DigiLocker digital verification step to instantly prove physical presence, overriding automated "Absent/Shifted" flags without waiting for manual BLO verification[cite: 15, 18, 20].
3. **Expedited Delta-Roll Injection:** Instead of a destructive Form 6, the system generates a specialized database patch that maps archived data to flip the voter's status from "Archived" back to "Active," preserving their unique EPIC identifier and legacy voting timeline[cite: 20, 21].
4. **Bulk Community Auditor:** Includes a bulk-upload feature that allows civil society groups, Resident Welfare Associations (RWAs), and political representatives to scan entire neighborhood CSV databases at once, generating batch restoration files for the local ERO[cite: 19, 21].

## 🏗️ System Architecture

The proposed data flow relies on existing ECI database structures while introducing a secure intermediary remediation engine:

| Component | Function within Architecture |
| :--- | :--- |
| **Citizen/NGO Input Layer** | Single EPIC lookup or Bulk CSV upload interface built in HTML/JS[cite: 20, 21]. |
| **Archival Database Lookup** | Interrogates the Central ECI ERONET Database archive to retrieve the specific deletion log and authorizing entity[cite: 20]. |
| **Identity Authentication** | UIDAI (Aadhaar) or DigiLocker API Gateway validates physical presence instantly[cite: 15, 18, 20]. |
| **Delta Patch Execution** | Uses a database trigger to transition entries from the Archived Table back to the Active Voters Table using the EPIC number as the primary key constraint[cite: 18, 21]. |

## 🚀 How to Run the Prototype

**Clone the Repository:**
   ```bash
   git clone https://github.com/yourusername/eci-sir-restoration-portal.git
   cd eci-sir-restoration-portal
   ```
 
1. **Run Locally:**
   Simply open the `index.html` file in any modern web browser. No local server, backend, or build-step is required for the frontend demonstration.
2. **Test the Single Audit:**
   * Enter Mock ID `XYZ9876543` to simulate an elector flagged as "Absent/Shifted".
   * Enter Mock ID `ABC1234567` to simulate an active elector.
3. **Test the Bulk Auditor:**
   * Click "Download Sample Neighborhood Dataset (.csv)" within the UI.
   * Upload the downloaded file to the dropzone to see the batch aggregation metrics and JSON export capabilities.

## 📖 Background & Context
This architectural proposal was developed against the backdrop of the youth-led Cockroach Janta Party (CJP) protests that escalated in late 2026[cite: 1, 10]. Originally formed in May 2026 to protest youth unemployment and NEET exam paper leaks, the movement expanded its focus by September and October 2026 to demand the resignation of Chief Election Commissioner Gyanesh Kumar[cite: 1, 5, 6]. This shift occurred after the Special Intensive Revision (SIR) led to the deletion of roughly 130 million names from the electoral rolls, a process critics alleged was arbitrary and bypassed internal ECI objections[cite: 6, 7, 8]. The Supreme Court of India intervened, issuing notices regarding the procedural legality of the mass deletions and clarifying that deletion from the roll does not equate to a loss of citizenship[cite: 8, 9]. This portal prototype is presented as a politically neutral, technical remediation tool to restore operational transparency, alleviate protest grievances, and optimize the ECI's digital infrastructure[cite: 11, 20].

## 📜 License
Open-Source (MIT License) - Intended for immediate civic, academic, and administrative adoption.

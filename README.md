# ECI Voter Roll Accountability & Fast-Track Restoration Portal

## 📌 Project Overview
🟢 Live Interactive Demo: https://deebong.github.io/eci-sir-restoration-portal/

This is a frontend prototype and architecture proposal for the Election Commission of India (ECI) IT Cell. It offers a way for voters mistakenly deleted during the Special Intensive Revision (SIR) to check their status and request restoration while keeping their electoral history.

## ⚠️ The Problem: SIR Bottlenecks
The Special Intensive Revision (SIR) deleted about 130 million names from India's electoral rolls. This caused three main issues:

* **Hidden reasons for deletion:** The National Electoral Search only tells voters if their record is found or not. It does not explain why a record was flagged (like "absent/shifted") or which Electoral Registration Officer (ERO) authorized it. 
* **The Form 6 problem:** ECI portals tell deleted voters to fill out Form 6. But Form 6 is only for first-time voters. When existing voters use it, they lose their voting history and have to falsely declare they have never voted before.
* **Verification backlog:** Automated software generated thousands of deletion forms without administrative reasons, forcing local officers to sign them. Booth Level Officers (BLOs) cannot manually verify all these flags before the next election.

## 💡 The Solution: Expedited Remediation
This tool proposes an isolated Fast-Track Restoration API layer for the existing ECI ERONET infrastructure. 

### Core Features
1. **Audit Trail:** Shows voters the exact technical reason they were deleted (e.g., algorithmic demographic multi-match, absent/shifted flag), pulling directly from the ECI archival log.
2. **Instant Verification:** Uses Aadhaar or DigiLocker to prove physical presence instantly, bypassing the manual BLO check.
3. **Delta-Roll Injection:** Instead of Form 6, it generates a database patch to change the voter's status from "Archived" back to "Active," keeping their EPIC identifier and voting history.
4. **Bulk Auditor:** Lets civil society groups and Resident Welfare Associations (RWAs) upload CSV files to scan whole neighborhoods at once, exporting batch files for the local ERO.

## 🏗️ System Architecture

The architecture uses existing ECI database structures alongside a new intermediary engine:

| Component | Function within Architecture |
| :--- | :--- |
| **Input Layer** | Single EPIC lookup or Bulk CSV upload interface built in HTML/JS. |
| **Archival Database Lookup** | Interrogates the Central ECI ERONET Database archive to retrieve the specific deletion log and authorizing entity. |
| **Identity Authentication** | UIDAI (Aadhaar) or DigiLocker API Gateway validates physical presence. |
| **Delta Patch Execution** | Uses a database trigger to transition entries from the Archived Table back to the Active Voters Table using the EPIC number as the primary key. |

## 🚀 How to Run the Prototype

This repository contains a standalone frontend prototype (`index.html`) built with vanilla JavaScript and Tailwind CSS.

**Clone the Repository:**
   ```bash
   git clone https://github.com/deebong/eci-sir-restoration-portal.git
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
The CJP (Cockroach Janta Party) protests in late 2026 prompted this proposal. After the movement expanded its focus from youth unemployment to the mass SIR deletions, protesters demanded the resignation of Chief Election Commissioner Gyanesh Kumar. Critics argued the deletions were arbitrary and bypassed ECI objections. The Supreme Court later intervened, issuing notices on the legality of the deletions and stating that deletion does not mean a loss of citizenship. This prototype is a technical approach to fixing the administrative side of the issue.

## Data Disclaimer
All data utilized in this prototype (EPIC numbers, names, Aadhaar OTP simulations) is entirely mocked for demonstration purposes and does not represent real ECI or UIDAI production data.

## 📜 License
Open-Source (MIT License) - Intended for immediate civic, academic, and administrative adoption.

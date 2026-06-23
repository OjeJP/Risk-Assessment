# Information Security Risk Assessment & Policy Analysis

> **Course:** Information Security Risk Management & Information Security Laws and Regulations
> **Institution:** ITMO University — Faculty of Secure Information Technologies
> **Supervisor:** Livshitz Ilya, PhD
> **Year:** 2023

**[View the live project page →](https://ojejp.github.io/Risk-Assessment/)**

---

## Overview

This repository contains two pieces of applied graduate-level information security work:

| # | Project | Standards |
|---|---------|-----------|
| 1 | **IS Risk Assessment, Implementation & Control** — full ISO 27005 risk treatment for JOP Corp, a simulated aviation technology company | ISO 27001, ISO 27005, ISO 31000, ISO 22301, ISO 13335-1 |
| 2 | **Boeing IS Policy — Critical Gap Analysis** — benchmarking Boeing's information security policy against ISO 27001 and ISO 27002 | ISO 27001, ISO 27002 |

---

## Project 1: IS Risk Assessment — JOP Corp

A complete end-to-end ISMS risk assessment for **JOP Corp** — a fictional flight school and aviation technology company — following the ISO 27005 risk management lifecycle across 21 identified assets.

### Methodology

```
Asset Identification → Vulnerability Assessment → Threat Assessment → Risk Quantification → Control Selection
```

---

### Phase 1 — Asset Identification & Assessment

- Identified and classified **21 assets** covering hardware, software, personnel, legal, and intangible categories
- Assets assessed using both qualitative (Very Big → Very Small) and quantitative (1–5) scoring
- Each asset assigned an owner per ISO 27001 and classified as Physical or Intangible
- Criteria mark threshold set at **5** — assets scoring above this were escalated for mandatory protection

**Top 6 escalated assets:**

| Asset | Mark | Decision |
|-------|------|----------|
| Server Room | 8 | Protect — mandatory |
| Backup Server Room | 8 | Protect — mandatory |
| IT Servers | 7 | Protect — mandatory |
| Digital Records (Databases) | 7 | Protect — mandatory |
| Networking Equipment | 7 | Protect — mandatory |
| Cloud Services | 6 | Protect — mandatory |

---

### Phase 2 — Vulnerability Assessment

Scoped to the 6 highest-priority assets. Specific CVEs identified and scored on a 0–5 significance scale. Criteria mark: **3**.

| Asset | Key Vulnerabilities | Score |
|-------|---------------------|-------|
| IT Servers | DoS, SQL Injection, Directory Attacks, CVE-2023-25928 (XSS) | 4/5 |
| Databases | CVE-2022-46763 (SQL injection in stored function) | 4/5 |
| Networking Equipment | CVE-2018-0101 (RCE), CVE-2021-1414 (Privilege Escalation) | 2/5 |
| Server Room | Lack of monitoring, social engineering, unauthorized hardware access | 5/5 |
| Backup Server Room | Social engineering, inadequate physical protection | 5/5 |
| Cloud Services | Misconfiguration, data loss, vulnerable access management, API flaws | 5/5 |

**Assessment methods used:** Penetration testing · Network-based scans · Database scans · Wireless assessment

---

### Phase 3 — Threat Assessment

Threats categorised across 7 types and tagged by origin. Scale: 1 (Very Small) to 5 (Very High). Criteria mark: **3**.

**Threat origin legend:**
- `A` — Accidental (unintentional human action)
- `D` — Deliberate (targeted/malicious action)
- `E` — Environmental (non-human origin)

| Asset | Threat | Type | Origin | Mark |
|-------|--------|------|--------|------|
| IT Servers | Saturation of IS · Server failure · SW/HW tampering | Technical Failures / Human Actions | A, D | 4 |
| Databases | Untrusted data input · Unauthorized personal data use | Human Actions | A, D | 4 |
| Server Room | Social Engineering · Equipment theft · HW tampering | Technical Failure / Human Actions | D | 5 |
| Backup Server Room | Social Engineering · Equipment theft · HW tampering | Technical Failure / Human Actions | D | 2 |
| Cloud Services | Failure of service providers | Organisational Threat | A, E | 4 |

---

### Phase 4 — Risk Quantification (5×5 Matrix)

**Risk Mark = Likelihood × Business Impact**

| Asset | Likelihood | Business Impact | Risk Mark | Risk Level |
|-------|-----------|----------------|-----------|------------|
| IT Servers | Unlikely (2) | Very Significant (5) | **10** | Medium |
| Databases | Unlikely (2) | Major (4) | **8** | Medium |
| Server Room | Rare (1) | Very Significant (5) | **5** | Low |
| Cloud Services | Rare (1) | Moderate (3) | **3** | Low |

Treatment threshold: assets scoring ≥ 6 received mandatory risk treatment.

---

### Phase 5 — Control Selection & Implementation

Controls applied to Medium-risk assets per ISO 27001 Annex A, ISO 31000, and ISO 22301.

| Asset | Risk Treatment | Controls |
|-------|---------------|----------|
| IT Servers | Staff training in IT policies · SSL/TLS implementation | `A.10.1.1`, `A.10.1.2` |
| Databases | Off-site backups · Firewall firmware update · New patch pack | `A.12.3.1`, `A.12.4.1–4.4` |

Additional controls across the broader asset set:

| Control | Description |
|---------|-------------|
| `A.11.1.1–1.5` | Physical security perimeter, entry controls, securing offices |
| `A.9.1.2 / A.9.2.2` | Network access control · User access provisioning |
| `A.9.2.3 / A.9.4.2` | Privileged access management · Secure log-on procedures |
| `A.13.1.3 / A.13.2.1` | Network segregation · Information transfer policies |
| `A.6.1.2` | Segregation of duties |

---

## Project 2: Boeing IS Policy — Critical Gap Analysis

A structured evaluation of Boeing's IS policy for protecting airline data on the ground and in the air, benchmarked against ISO/IEC 27001:2013 and ISO/IEC 27002:2013.

### Strengths
- Aligns with ISO 27001 Clause 4 — ISMS scope and risk identification
- Covers core ISO 27002 domains: data classification, access control, incident management, encryption, secure communication channels
- 24/7 third-party managed ethics and incident reporting line across 35 countries

### Gaps Identified

| Severity | Gap | Risk |
|----------|-----|------|
| Critical | Test/dev networks publicly exposed to the internet | Source code and build systems accessible; potential supply-chain compromise |
| Critical | Email server infected with malware; no DMARC enforcement | boeing.com domain spoofable — phishing risk to employees, suppliers, and government clients |
| Medium | No third-party vendor security policy | Supply chain incidents have no defined response path |
| Medium | Training programme has no defined audience, type, or frequency | Compliance immeasurable; ISO 27002 §6.3 unsatisfied |
| Medium | No detailed guidance on secure communication channels | Gaps in ground-to-air data transmission security |

### Recommendations

| Recommendation | ISO Reference |
|---------------|---------------|
| Network segmentation — isolate dev/test from public internet, enforce DMZ | ISO 27002 §13.1.3 |
| Deploy full email auth stack: SPF + DKIM + DMARC on boeing.com | ISO 27002 §10.x |
| Formalise vendor risk programme with contractual obligations and audit rights | ISO 27002 §15.1 |
| Define role-based training curricula with delivery cadence and KPIs | ISO 27002 §6.3 |
| Provide implementation-level guidance on secure communication channels | ISO 27002 §13.2 |

---

## Standards Referenced

| Standard | Title |
|----------|-------|
| ISO/IEC 13335-1:2004 | IT Security Management Concepts and Models |
| ISO/IEC 27001:2013 | Information Security Management Systems — Requirements |
| ISO/IEC 27002:2013 | Code of Practice for Information Security Controls |
| ISO/IEC 27005:2008 | Information Security Risk Management |
| ISO/IEC 31000:2018 | Risk Management — Guidelines |
| ISO/IEC 22301:2012 | Business Continuity Management Systems |

---

## Repository Structure

```
infosec-risk-assessment/
├── index.html      # Live project page (GitHub Pages)
└── README.md       # This file
```

---

## How to View

The project is deployed via GitHub Pages:
**`https://ojejp.github.io/Risk-Assessment/`**

---

*JOP Corp is a fictional company created solely for educational purposes.*

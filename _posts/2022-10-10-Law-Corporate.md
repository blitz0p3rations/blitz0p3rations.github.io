---
layout: post
title: 'Law Corporate Internal PT'
tags:
 - internal-network
 - real-activity
hero: https://images.unsplash.com/photo-1505664194779-8beaceb93744?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1470&q=80
overlay: blue
---

Please note that for this proof of concept, while images and step-by-step reproduction tips are fundamental for evidentiary purposes, they will not be supplied. Furthermore, in adherence to our commitment to privacy and compliance with non-disclosure agreements, all URLs and functionalities within this assessment have been anonymized. {: .lead} <!–-break-–>

# Law Corporate

## Type of activity and objectives
The objective of this engagement was to conduct an internal penetration assessment for the organization. The aim was to identify potential vulnerabilities that could potentially be exploited from inside sources, with the goal of preventing unauthorized access, compromise and data exfiltration.
## Scope of evaluation
The evaluation was focused on the internal surface of the organization. This scope encompassed assessing the security and potential vulnerabilities within this internal surface.
## Executive Summary
The internal penetration test conducted on the organization's infrastructure revealed several critical vulnerabilities that require immediate attention. The findings include unauthorized access to sensitive systems due to the presence of default credentials.
## Finding Summary
- Postgres DB access with default credentials 
- Printer RICOH with default credentials
- Router with default credentials
## Risk Impact Graph with CVSS Scores

![](https://raw.githubusercontent.com/blitz0p3rations/blitz0p3rations.github.io/master/uploads/id33.png)

## Vulnerability Types Distribution

![](https://raw.githubusercontent.com/blitz0p3rations/blitz0p3rations.github.io/master/uploads/id34.png)

## Attack storyline and findings### PostGres DB access with default credentials
- CVSS Vector: None
#### Proof of Concept (PoC) 
During the assessment, it was discovered that the PostgreSQL database was accessible using default credentials. This vulnerability poses a significant security risk as unauthorized users could potentially gain access to sensitive data stored within the database.

#### Remediations
- Change Default Credentials

### RICOH Printer with Default Credentials:
- CVSS Vector: None
#### Proof of Concept (PoC) 
The assessment identified a RICOH printer that was accessible using default credentials. This poses a potential threat as an attacker could exploit this vulnerability to compromise the printer, potentially leading to unauthorized access, data leakage, or disruption of printing services.
#### Remediations
- Change Default Credentials

### Router with Default Credentials
- CVSS Vector: None
#### Proof of Concept (PoC) 
The penetration test also revealed a router within the internal network that was accessible using default credentials. This finding is concerning as unauthorized access to network devices can provide attackers with a foothold to further infiltrate the network, potentially compromising critical systems and data.
#### Remediations
- Change Default Credentials

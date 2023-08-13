---
layout: post
title: 'ISP Company network PT'
tags:
 - network
 - real-engagement
hero: https://images.unsplash.com/photo-1462206092226-f46025ffe607?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1474&q=80
overlay: blue
---

No images (image for the step by step PoC are essential as evidence but will not be provided
) or references will be provided, as this assessment was a real engagement. Additionally, all URLs and functionalities have been anonymized to ensure privacy and compliance with non-disclosure agreements (NDAs). {: .lead} <!--break-->

# ISP Company

## Type of activity and objectives
The main objective of this engagement was to conduct an extensive network penetration test on the billing virtual machine infrastructure.
## Scope of evaluation
The evaluation was focused on the specific subents give to the team by the target organization. 
## Executive Summary
Following a web applicaiton penetration test, the offensive team has identified a critical Insecure Direct Object Reference (IDOR) vulnerability. 
This vulnerability enables regular users to elevate their privileges and bypass the paywall, gaining unauthorized access with administrative rights.
## Finding Summary
- MongoDB wiht no Auth required
- Hashicorp console web UI access
- SNMP default credentials
## Attack storyline or vulnerabilities with CVSS,CVE and remedations
### MongoDB wiht no Auth required
- CVSS Vector: None
#### Proof of Concept (PoC) 
A MongoDB instance was discovered with no authentication required, exposing sensitive data to potential unauthorized access.
- `mongo ip:port`
#### Remediations
- Enable Authentication: Implement strong authentication mechanisms, such as username and password or key-based authentication, to ensure that only authorized users can access the MongoDB instance.

- Configure Firewall Rules: Restrict access to the MongoDB instance by configuring firewall rules to allow connections only from trusted IP addresses.
### Hashicorp console web UI access
- CVSS Vector: None
#### Proof of Concept (PoC) 
The HashiCorp console's web UI was accessible without proper authentication, which could lead to unauthorized configuration changes and potential data breaches.
#### Remediations
- Configure the HashiCorp console to require proper authentication before granting access to the web UI.
- Configure IP whitelisting to restrict access to the HashiCorp console's web UI from trusted IP addresses or networks only.
### SNMP default credentials
- CVSS Vector: None
#### Proof of Concept (PoC) 
SNMP devices were found using default credentials, posing a significant security risk by allowing attackers to gather sensitive information and potentially manipulate network devices.
#### Remediations
- Enforce strong password policies for all SNMP community strings.
- Require regular password updates and disallow the use of default or easily guessable passwords.
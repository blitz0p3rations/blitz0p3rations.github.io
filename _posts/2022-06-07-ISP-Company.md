---
layout: post
title: 'ISP Company network PT'
tags:
 - internal-network
 - real-activity
hero: https://images.unsplash.com/photo-1462206092226-f46025ffe607?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1474&q=80
overlay: blue
---

Please note that for this proof of concept, while images and step-by-step reproduction tips are fundamental for evidentiary purposes, they will not be supplied. Furthermore, in adherence to our commitment to privacy and compliance with non-disclosure agreements, all URLs and functionalities within this assessment have been anonymized. {: .lead} <!–-break-–>

# ISP Company

## Type of activity and objectives
The main objective of this engagement was to conduct an extensive network penetration test on the billing virtual machine network infrastructure.
## Scope of evaluation
The evaluation was focused on the specific subnets given to the team by the target organization. 
## Executive Summary
During the assessment, several high-severity findings were revealed. The first concerned a database instance that was accessible without any required authentication. This vulnerability poses a significant risk as it could potentially allow unauthorized access to sensitive data stored in the database. The second notable finding was the discovery of an unsecured HashiCorp remote console user interface, which also lacked necessary authentication measures. This vulnerability presents a risk of unauthorized access and control over the console. Additionally, the assessment identified the use of default credentials in an SMTP setup, which is a common security risk that could lead to unauthorized access or misuse of the email server.
## Finding Summary
- MongoDB with no Auth required
- Hashicorp console web UI access
- SNMP default credentials
## Risk Impact Graph with CVSS Scores

![](https://raw.githubusercontent.com/blitz0p3rations/blitz0p3rations.github.io/master/uploads/id15.png)

## Vulnerability Types Distribution

![](https://raw.githubusercontent.com/blitz0p3rations/blitz0p3rations.github.io/master/uploads/id16.png)

## Attack storyline and findings### MongoDB with no Auth required
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

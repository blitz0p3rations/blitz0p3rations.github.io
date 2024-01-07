---
layout: post
title: 'Luxury Corporate External PT'
tags:
 - web
 - real-activity
hero: 
overlay: red
---

Please note that for this proof of concept, while images and step-by-step reproduction tips are fundamental for evidentiary purposes, they will not be supplied. Furthermore, in adherence to our commitment to privacy and compliance with non-disclosure agreements, all URLs and functionalities within this assessment have been anonymized. {: .lead}
 <!--break-->

# Luxury Company

## Type of activity and objectives
The objective of this engagement was to conduct an external penetration assessment for the corporation. The aim was to identify potential vulnerabilities that could potentially be exploited from outside sources, to prevent unauthorized access and compromise.
## Scope of evaluation
The evaluation was focused on the specific netblock assigned to the organization. This scope encompassed assessing the security and potential vulnerabilities within this network range.
## Executive Summary
Following an external penetration test, the offensive team has identified a few misconfigurations involving exposed Telnet interfaces.
Telnet interfaces are found to be accessible on standard ports across multiple instances, which presents significant security risks to the organization.
## Finding Summary
- Telnet exposed
## Risk Impact Graph with CVSS Scores

![](https://raw.githubusercontent.com/blitz0p3rations/blitz0p3rations.github.io/master/uploads/lux1.png)

## Vulnerability Types Distribution
![](https://raw.githubusercontent.com/blitz0p3rations/blitz0p3rations.github.io/master/uploads/lux2.png)
## Attack storyline and findings
### Telnet exposed 
- CVSS Vector: None
#### Proof of Concept (PoC) 
During the test, multiple instances of servers with Telnet interfaces were identified as available on standard ports.
#### Remediations
- Disable Telnet: The most effective solution is to disable Telnet altogether and use more secure alternatives like SSH for remote access.

- Replace with SSH: Replace Telnet with SSH (Secure Shell), which provides encrypted communication and stronger authentication mechanisms.

- Firewall Rules: Restrict access to the Telnet service using firewall rules. Allow access only from trusted IP addresses and networks.

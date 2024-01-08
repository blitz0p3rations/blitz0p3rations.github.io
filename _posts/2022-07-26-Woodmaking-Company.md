---
layout: post
title: 'Woodmaking Company External PT'
tags:
 - web
 - real-activity
hero: https://images.unsplash.com/photo-1462206092226-f46025ffe607?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1474&q=80
overlay: blue
---

Please note that for this proof of concept, while images and step-by-step reproduction tips are fundamental for evidentiary purposes, they will not be supplied. Furthermore, in adherence to our commitment to privacy and compliance with non-disclosure agreements, all URLs and functionalities within this assessment have been anonymized. {: .lead}
 <!--break-->

# Woodmaking Company

## Type of activity and objectives
The objective of this engagement was to conduct an external penetration assessment for the organization. The aim was to identify potential vulnerabilities that could potentially be exploited from outside sources, with the goal of preventing unauthorized access and compromise.
## Scope of evaluation
The evaluation was focused on the external surface of the organization. This scope encompassed assessing the security and potential vulnerabilities within this external surface.
## Executive Summary
The assessment conducted on the external surface of the target organization identified two critical vulnerabilities: SQL Injection (SQLi) and IFrame Injection (CVE-2021-45092). 
Immediate remediation is recommended to mitigate the risk of potential data breaches, unauthorized access, and malicious content injection.
## Finding Summary
- SQLi 
- IFrame Injection CVE-2021-45092
## Risk Impact Graph with CVSS Scores

![](https://raw.githubusercontent.com/blitz0p3rations/blitz0p3rations.github.io/master/uploads/id25.png)

## Vulnerability Types Distribution

![](https://raw.githubusercontent.com/blitz0p3rations/blitz0p3rations.github.io/master/uploads/id26.png)

## Attack storyline and findings### SQLi to RCE (0day)
- CVSS Vector: CVSS:3.0/AV:N/AC:L/PR:N/UI:N/S:C/C:H/I:H/A:H
#### Proof of Concept (PoC) 
SQL Injection (SQLi) is a type of cyber attack where an attacker exploits vulnerabilities in a web application's input validation mechanisms to inject malicious SQL (Structured Query Language) statements into the application's database. 

The "ip" parameter was vulnerable to SQLi.

#### Remediations
- Update the software solution
- Restrict access to mitigate
### IFrame Injection CVE-2021-45092
- CVSS Vector: CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:H
#### Proof of Concept (PoC) 
Thinfinity VirtualUI before 3.0 has functionality in /lab.html reachable by default that could allow IFRAME injection via the vpath parameter.

By accessing the following payload (URL) an attacker could iframe any external website (of course, only external endpoints that allows being iframed).

The vulnerable vector is **https://target.com/lab.html?vpath=//wikipedia.com <https://target.com/lab.html?vpath=//wikipedia.com>** where "vpath=//" is the pointer to the external site to be iframed.
#### Remediations
- Update the software solution
- Restrict access to mitigate

---
layout: post
title: 'Freeze Company External PT'
tags:
 - web
 - real-engagement
hero: https://images.unsplash.com/photo-1538108149393-fbbd81895907?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1528&q=80
overlay: blue
---

No images (image for the step by step PoC are essential as evidence but will not be provided
) or references will be provided, as this assessment was a real engagement. Additionally, all URLs and functionalities have been anonymized to ensure privacy and compliance with non-disclosure agreements (NDAs). {: .lead} <!--break-->

# Freeze Company

## Type of activity and objectives
The objective of this engagement was to conduct an external penetration assessment for the organization. The aim was to identify potential vulnerabilities that could potentially be exploited from outside sources, with the goal of preventing unauthorized access and compromise.
## Scope of evaluation
The evaluation was focused on the specific website of the organization. This scope encompassed assessing the security and potential vulnerabilities within this website.
## Executive Summary
The security assessment conducted on the Content Management System (CMS) of the target website has identified a critical vulnerability that could potentially lead to user disclosure. This finding highlights a significant risk to user privacy and the security of sensitive information stored within the CMS.

The vulnerability allows unauthorized individuals to gain access to user-related data, such as personal information, login credentials, and other sensitive details, stored on the CMS nodes. Such unauthorized access can result in privacy breaches, identity theft, and the exposure of confidential information to malicious actors.
## Finding Summary
- Secrets disclosure from CMS nodes
## Attack storyline or vulnerabilities with CVSS,CVE and remedations
### Secrets disclosure from CMS nodes
- CVSS Vector: None
#### Proof of Concept (PoC) 
The PoC involved examining the CMS nodes and their contents, revealing the presence of secrets, user-related data, and confidential information. By accessing these nodes, an attacker could potentially extract sensitive details, compromise user accounts, and gain unauthorized access to restricted areas of the CMS.
#### Remediations
- The organization should implement strict access controls and permissions for CMS nodes, ensuring that only authorized personnel can view and manipulate sensitive information.
- Delete secrets from nodes.



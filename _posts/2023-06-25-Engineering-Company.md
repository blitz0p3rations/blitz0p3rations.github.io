---
layout: post
title: 'Engineering Company external PT'
tags:
 - web
 - real-engagement
hero: https://images.unsplash.com/photo-1462206092226-f46025ffe607?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1474&q=80
overlay: blue
---

No images (image for the step by step PoC are essential as evidence but will not be provided
) or references will be provided, as this assessment was a real engagement. Additionally, all URLs and functionalities have been anonymized to ensure privacy and compliance with non-disclosure agreements (NDAs). {: .lead} <!--break-->

# Engineering Company

## Type of activity and objectives
The objective of this engagement was to conduct an external penetration assessment for the organization. The aim was to identify potential vulnerabilities that could potentially be exploited from outside sources, with the goal of preventing unauthorized access, compromise and data exfiltration.
## Scope of evaluation
The evaluation was focused on the outised surface of the organization. This scope encompassed assessing the security and potential vulnerabilities within this external surface.
## Executive Summary
The assessment of the target environment uncovered two significant findings:

1. **Credentials Disclosure in JS File:** The evaluation revealed that sensitive credentials are being exposed within a JavaScript file. This situation poses a critical security concern as it could potentially allow unauthorized individuals to access sensitive user information. Urgent measures are required to prevent the unauthorized exposure of these credentials and to ensure that proper security controls are in place.

2. **Remote Code Execution (RCE):** An RCE vulnerability was identified in the environment. However, the provided information lacks details to accurately assess the severity and specific nature of this vulnerability. Without further context, it is challenging to offer appropriate recommendations for remediation.

Given the seriousness of both findings, immediate attention and action are necessary to safeguard sensitive data, prevent unauthorized access, and address any potential vulnerabilities.
## Finding Summary
- Credentials disclosre in JS file
- CVE-2021-44529
## Attack storyline or vulnerabilities with CVSS,CVE and remedations
### Credentials disclosre in JS file
- CVSS Vector: None
#### Proof of Concept (PoC) 
The Proof of Concept (PoC) demonstrates the identification of a security issue in the "main.js" file of the application. By analyzing this file, sensitive credentials were discovered, which were then exploited to gain unauthorized access to the medical factory.
#### Remediations
- Never expose hardcoded secrets
### CVE-2021-44529
- CVSS Vector: CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:H
#### Proof of Concept (PoC) 
The Proof of Concept (PoC) demonstrates a code injection vulnerability present in the Ivanti EPM Cloud Services Appliance (CSA). This vulnerability enables an unauthenticated user to execute arbitrary code within the context of limited permissions, typically associated with the 'nobody' user.

The provided exploit, available at https://github.com/jkana/CVE-2021-44529, successfully leverages this vulnerability to achieve remote code execution (RCE) on the targeted system.

#### Remediations
- Patch or update Ivanti EPM Cloud Services Appliance
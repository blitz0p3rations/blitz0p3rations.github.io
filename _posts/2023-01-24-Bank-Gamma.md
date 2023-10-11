---
layout: post
title: 'Bank Gamma Android mobile PT'
tags:
 - mobile
 - real-engagement
hero: https://images.unsplash.com/photo-1501167786227-4cba60f6d58f?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxzZWFyY2h8Mnx8YmFua3xlbnwwfHwwfHx8MA%3D%3D&auto=format&fit=crop&w=400&q=60
overlay: blue
---

No images (images for the step-by-step PoC are essential as evidence but will not be provided
) or references will be provided, as this assessment was a real engagement. Additionally, all URLs and functionalities have been anonymized to ensure privacy and compliance with non-disclosure agreements (NDAs). {: .lead} <!--break-->

# Bank Gamma

## Type of activity and objectives
The objective of this engagement was to conduct a mobile penetration assessment for the organization. The aim was to identify potential vulnerabilities that could potentially be exploited from the mobile app, to prevent unauthorized access, compromise and data exfiltration.
## Scope of evaluation
The evaluation was focused on the Bank Connect Android Mobile app of the organization. This scope encompassed assessing the security and potential vulnerabilities within this surface.
## Executive Summary
The assessment of the Android bank account app revealed two significant findings: a root detection bypass vulnerability and the absence of certificate pinning. These vulnerabilities could expose the app and its users to potential security risks, including unauthorized access and data interception. These issues must be addressed promptly to ensure the security and integrity of the app and the sensitive financial data it handles.
## Finding Summary
- Root Detection bypass
- Lack of certificate pinning
## Attack storyline or vulnerabilities with CVSS, CVE and remediations
### Root Detection bypass
- CVSS Vector: None
#### Proof of Concept (PoC) 
The mobile app's root detection mechanism was successfully bypassed using the FRIDA tool. By analyzing the app's code, we identified the function responsible for root detection. Subsequently, a custom FRIDA script was developed to reverse engineer the function's behaviour and effectively bypass the security measure. This exploit demonstrates the app's vulnerability to root detection evasion and highlights the need for a more robust root detection mechanism to ensure the app's security.
#### Remediations
- Implement more robust root detection
### Lack of certificate pinning
- CVSS Vector: None
#### Proof of Concept (PoC) 
The mobile app lacked certificate pinning, which allowed interception of requests and traffic. By exploiting this vulnerability, an attacker could potentially intercept and manipulate the app's communication with external servers. This underscores the importance of implementing proper certificate pinning to ensure the integrity and security of data exchanged between the app and its backend servers.
#### Remediations
- Implement certificate pinning

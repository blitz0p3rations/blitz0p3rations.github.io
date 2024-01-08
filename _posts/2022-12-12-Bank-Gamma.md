---
layout: post
title: 'Bank Gamma Android mobile PT'
tags:
 - mobile
 - real-activity
hero: https://images.unsplash.com/photo-1501167786227-4cba60f6d58f?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxzZWFyY2h8Mnx8YmFua3xlbnwwfHwwfHx8MA%3D%3D&auto=format&fit=crop&w=400&q=60
overlay: blue
---

Please note that for this proof of concept, while images and step-by-step reproduction tips are fundamental for evidentiary purposes, they will not be supplied. Furthermore, in adherence to our commitment to privacy and compliance with non-disclosure agreements, all URLs and functionalities within this assessment have been anonymized. {: .lead}
 {: .lead} <!--break-->

# Bank Gamma

## Type of activity and objectives
The objective of this engagement was to conduct a mobile penetration assessment for the organization. The aim was to identify potential vulnerabilities that could potentially be exploited from the mobile app, with the goal of preventing unauthorized access, compromise and data exfiltration.
## Scope of evaluation
The evaluation was focused on the Bank Account Android Mobile app of the organization. This scope encompassed assessing the security and potential vulnerabilities within this surface.
## Executive Summary
The assessment of the Android bank account app revealed two significant findings: a root detection bypass vulnerability and the absence of certificate pinning. These vulnerabilities could expose the app and its users to potential security risks, including unauthorized access and data interception. It is crucial that these issues are addressed promptly to ensure the security and integrity of the app and the sensitive financial data it handles.
## Finding Summary
- Root Detection bypass
- Lack of certificate pinning
## Risk Impact Graph with CVSS Scores

![](https://raw.githubusercontent.com/blitz0p3rations/blitz0p3rations.github.io/master/uploads/id37.png)

## Vulnerability Types Distribution

![](https://raw.githubusercontent.com/blitz0p3rations/blitz0p3rations.github.io/master/uploads/id38.png)

## Attack storyline and findings### Root Detection bypass
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

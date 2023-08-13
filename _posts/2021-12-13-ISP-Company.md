---
layout: post
title: 'ISP Company Web Application PT'
tags:
 - web
 - real-engagement
hero: https://images.unsplash.com/photo-1462206092226-f46025ffe607?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1474&q=80
overlay: blue
---

No images (image for the step by step PoC are essential as evidence but will not be provided
) or references will be provided, as this assessment was a real engagement. Additionally, all URLs and functionalities have been anonymized to ensure privacy and compliance with non-disclosure agreements (NDAs). {: .lead} <!--break-->

# ISP Company

## Type of activity and objectives
The primary goal of this engagement was to perform a comprehensive penetration test on the web applications within the defined scope.
## Scope of evaluation
The evaluation was focused on the specific web apps give to the team by the target organization. Additionally, the company supplied a selection of credentials with varying levels of privileges for assessment purposes.
## Executive Summary
Following a web applicaiton penetration test, the offensive team has identified a critical Insecure Direct Object Reference (IDOR) vulnerability. 
This vulnerability enables regular users to elevate their privileges and bypass the paywall, gaining unauthorized access with administrative rights.
## Finding Summary
- IDOR
## Attack storyline or vulnerabilities with CVSS,CVE and remedations
### Telnet exposed 
- CVSS Vector: CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:N
#### Proof of Concept (PoC) 
The presented Proof of Concept (PoC) reveals an Insecure Direct Object Reference (IDOR) vulnerability within an electronic billing web application. By examining the path of the admin functionalities and attempting to replicate them using a lower-privileged user account, an exploitation path was identified that bypasses the paywall. This issue highlights inadequate implementation of access controls within the application.

The impact of this vulnerability can be significant, as it allows unauthorized users to gain access to premium content (**/v2/getBillsPremium**) that should only be accessible to authorized users. Such a vulnerability may lead to unauthorized disclosure of sensitive information or manipulation of premium features without proper privileges.
#### Remediations
To mitigate this issue, it is strongly recommended that the organization improves access control mechanisms, ensuring that only authorized users can access the premium content. By addressing this vulnerability, the application's security posture can be enhanced, preventing unauthorized access and maintaining the confidentiality of sensitive information. access to the Telnet service using firewall rules. Allow access only from trusted IP addresses and networks.
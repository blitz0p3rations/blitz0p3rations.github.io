---
layout: post
title: 'ISP Company Web Application PT'
tags:
 - web
 - real-activity
hero: https://images.unsplash.com/photo-1462206092226-f46025ffe607?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1474&q=80
overlay: blue
---

Please note that for this proof of concept, while images and step-by-step reproduction tips are fundamental for evidentiary purposes, they will not be supplied. Furthermore, in adherence to our commitment to privacy and compliance with non-disclosure agreements, all URLs and functionalities within this assessment have been anonymized. {: .lead} <!–-break-–>

# ISP Company

## Type of activity and objectives
The primary goal of this engagement was to perform a comprehensive penetration test on the web applications within the defined scope.
## Scope of evaluation
The evaluation was focused on the specific web apps given to the team by the target organization. Additionally, the company supplied a selection of credentials with varying levels of privileges for assessment purposes.
## Executive Summary
After conducting a web application penetration test, the offensive team identified a critical Insecure Direct Object Reference (IDOR) vulnerability. This vulnerability allows regular users to elevate their privileges, enabling them to bypass the paywall and gain unauthorized access with administrative rights.

This discovery highlights a significant security flaw, as it compromises the integrity of the application by allowing unauthorized access and control. The potential for such elevated access underscores the urgency for prompt and effective remediation to safeguard the application against exploitation.
## Finding Summary
- IDOR
## Risk Impact Graph with CVSS Scores

![](https://raw.githubusercontent.com/blitz0p3rations/blitz0p3rations.github.io/master/uploads/mau1.png)

## Vulnerability Types Distribution

![](https://raw.githubusercontent.com/blitz0p3rations/blitz0p3rations.github.io/master/uploads/mau2.png)

## Attack storyline and findings
### IDOR 
- CVSS Vector: CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:N
#### Proof of Concept (PoC) 
The presented Proof of Concept (PoC) reveals an Insecure Direct Object Reference (IDOR) vulnerability within an electronic billing web application. By examining the path of the admin functionalities and attempting to replicate them using a lower-privileged user account, an exploitation path was identified that bypasses the paywall. This issue highlights the inadequate implementation of access controls within the application.

The impact of this vulnerability can be significant, as it allows unauthorized users to gain access to premium content (**/v2/getBillsPremium**) that should only be accessible to authorized users. Such a vulnerability may lead to unauthorized disclosure of sensitive information or manipulation of premium features without proper privileges.
#### Remediations
To mitigate this issue, it is strongly recommended that the organization improves access control mechanisms, ensuring that only authorized users can access the premium content. By addressing this vulnerability, the application's security posture can be enhanced, preventing unauthorized access and maintaining the confidentiality of sensitive information—access to the Telnet service using firewall rules. Allow access only from trusted IP addresses and networks.

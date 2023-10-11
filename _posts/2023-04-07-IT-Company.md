---
layout: post
title: 'IT Company Web Application PT'
tags:
 - web
 - real-engagement
hero: https://images.unsplash.com/photo-1462206092226-f46025ffe607?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1474&q=80
overlay: red
---

No images (images for the step-by-step PoC are essential as evidence but will not be provided
) or references will be provided, as this assessment was a real engagement. Additionally, all URLs and functionalities have been anonymized to ensure privacy and compliance with non-disclosure agreements (NDAs). {: .lead} <!--break-->

# IT Company

## Type of activity and objectives
The objective of this engagement was to conduct a web application penetration test for the organization. The aim was to identify potential vulnerabilities that could potentially be exploited from the outside, to prevent unauthorized access, compromise and data exfiltration.
## Scope of evaluation
The evaluation was focused on the exposed web application. This scope encompassed assessing the security and potential vulnerabilities within this surface.
## Executive Summary 
During the assessment, two critical security vulnerabilities were identified in the target system:

- Admin Dashboard Accessible from Guest User: The evaluation revealed a significant security lapse where the admin dashboard, meant to be restricted to authorized users, was accessible from a guest user account. This misconfiguration poses a serious risk as unauthorized individuals could potentially gain access to privileged administrative functions, compromising the security and integrity of the system. Immediate attention is required to rectify this issue and enforce proper access controls to prevent unauthorized access.

- Unrestricted File Download Vulnerability: A vulnerability allowing unrestricted file downloads was identified within the system. This flaw could be exploited by attackers to download sensitive files, possibly containing critical information or proprietary data. The absence of proper validation and access controls could lead to unauthorized access and data breaches. It is recommended to implement proper input validation, authorization checks, and access controls to mitigate this vulnerability and safeguard the system's data and assets.

## Finding Summary
- Admin dashboard accessible from Guest user
- Unrestricted file download
## Attack storyline or vulnerabilities with CVSS, CVE and remediations
### Admin dashboard accessible from Guest user
- CVSS Vector: None 
#### Proof of Concept (PoC)
It was observed that the admin dashboard could be accessed by manipulating the URL path through fuzzing activities, even from a guest account. By attempting different variations of URL paths and parameters, a guest user was able to discover a specific path that led to the admin dashboard. This unauthorized access allowed the guest user to view sensitive administrative information and perform actions intended only for privileged users.
#### Remediations
- Restrict access to the admin dashboard
- Add a layer of authentication

### Unrestricted file download
- CVSS Vector: CVSS:3.0/AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:N/A:N
#### Proof of Concept (PoC)
It was observed that certain files located within the restricted area of the web application were accessible for download even by non-authenticated users. 
#### Remediations
- Implement Proper Access Controls: Restrict access to files based on user authentication and authorization. Only authenticated and authorized users should be able to access and download files.

- Use Server-Side Validation: Implement server-side validation and authorization checks to ensure that users are only able to download files they are authorized to access.

- Apply Secure Directories: Store sensitive files outside of the web root directory to prevent direct access from URLs. This helps ensure that files can only be accessed through authorized means within the application.

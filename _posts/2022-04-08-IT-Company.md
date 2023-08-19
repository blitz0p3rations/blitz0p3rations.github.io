---
layout: post
title: 'IT Company Web Applicaion PT'
tags:
 - web
 - real-engagement
hero: https://images.unsplash.com/photo-1462206092226-f46025ffe607?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1474&q=80
overlay: red
---

No images (image for the step by step PoC are essential as evidence but will not be provided
) or references will be provided, as this assessment was a real engagement. Additionally, all URLs and functionalities have been anonymized to ensure privacy and compliance with non-disclosure agreements (NDAs). {: .lead} <!--break-->

# IT Company

## Type of activity and objectives
The objective of this engagement was to conduct a web application penetration test for the organization. The aim was to identify potential vulnerabilities that could potentially be exploited from the outside, with the goal of preventing unauthorized access, compromise and data exfiltration.
## Scope of evaluation
The evaluation was focused on the exposed web application. This scope encompassed assessing the security and potential vulnerabilities within this surface.
## Executive Summary 
During the assessment of the target application, it was identified that the Swagger documentation for the application's APIs was exposed and accessible without proper authentication or authorization. The exposure of Swagger documentation can pose a security risk as it provides detailed information about the APIs, endpoints, parameters, and data structures used by the application.

Exposing Swagger documentation without proper access controls can potentially aid attackers in understanding the application's functionality, endpoints, and how to interact with the APIs. This can lead to various security issues, including unauthorized data access, injection attacks, and other vulnerabilities.
## Finding Summary
- Exposed Swagger Documentation
## Attack storyline or vulnerabilities with CVSS,CVE and remedations
### IDOR
- CVSS Vector: None
#### Proof of Concept (PoC)
During the assessment of the target web application, it was observed that the Swagger documentation for the application's APIs was accessible without proper authentication. The following URL led to the exposed Swagger documentation:
`https://example.com/swagger/index.html`
#### Remediations
- Restrict access to this resource

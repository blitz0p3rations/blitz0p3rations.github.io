---
layout: post
title: 'IT Company Web Application PT'
tags:
 - web
 - real-activity
hero: https://images.unsplash.com/photo-1462206092226-f46025ffe607?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1474&q=80
overlay: blue
---

Please note that for this proof of concept, while images and step-by-step reproduction tips are fundamental for evidentiary purposes, they will not be supplied. Furthermore, in adherence to our commitment to privacy and compliance with non-disclosure agreements, all URLs and functionalities within this assessment have been anonymized. {: .lead}
 <!--break-->

# IT Company

## Type of activity and objectives
The objective of this engagement was to conduct a web application penetration test for the organization. The aim was to identify potential vulnerabilities that could potentially be exploited from the outside, to prevent unauthorized access, compromise and data exfiltration.
## Scope of evaluation
The evaluation was focused on the exposed web application. This scope encompassed assessing the security and potential vulnerabilities within this surface.
## Executive Summary 
During the assessment of the target application, several instances of Insecure Direct Object References (IDOR) vulnerabilities were identified. These vulnerabilities allow authenticated or unauthenticated users to access sensitive resources or perform actions that they are not authorized for. The IDOR vulnerabilities could potentially lead to unauthorized data exposure, manipulation, or other security breaches.
## Finding Summary
- IDOR
## Risk Impact Graph with CVSS Scores

![](https://raw.githubusercontent.com/blitz0p3rations/blitz0p3rations.github.io/master/uploads/id5.png)

## Vulnerability Types Distribution

![](https://raw.githubusercontent.com/blitz0p3rations/blitz0p3rations.github.io/master/uploads/id6.png)

## Attack storyline and findings
### IDOR
- CVSS Vector: CVSS:3.0/AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:H
#### Proof of Concept (PoC)
During the testing phase, leveraging the provided user accounts from the client, it was possible to identify three distinct business logic flaws. These flaws allowed the user with the STANDARD role to access functions that are exclusively intended for the PREMIUM role. Additionally, three other business logic flaws were identified, which enabled the PREMIUM user to access functionalities that were meant to be exclusive to the STANDARD user.
#### Remediations
- Authorization Checks: Implement proper authorization checks to ensure that users are only able to access the resources and functionalities they are authorized for. Use role-based access control (RBAC) mechanisms to restrict access based on user roles and permissions.

- Object Mapping: Avoid exposing internal identifiers directly in URLs or parameters. Instead, use object mapping techniques, such as using randomized or hashed identifiers, to prevent attackers from easily guessing or manipulating resource identifiers.

- Input Validation: Validate and sanitize all input parameters to ensure that they are within expected ranges and formats. Perform validation on the server side to prevent unauthorized access to resources.

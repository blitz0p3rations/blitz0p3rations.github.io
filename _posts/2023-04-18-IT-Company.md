---
layout: post
title: 'IT Company Web Application PT'
tags:
 - web
 - real-activity
hero: https://images.unsplash.com/photo-1462206092226-f46025ffe607?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1474&q=80
overlay: blue
---

Please note that for this proof of concept, while images and step-by-step reproduction tips are fundamental for evidentiary purposes, they will not be supplied. Furthermore, in adherence to our commitment to privacy and compliance with non-disclosure agreements, all URLs and functionalities within this assessment have been anonymized. {: .lead} <!–-break-–>

# IT Company

## Type of activity and objectives
The objective of this engagement was to conduct a web application penetration test for the organization. The aim was to identify potential vulnerabilities that could potentially be exploited from the outside, to prevent unauthorized access, compromise and data exfiltration.
## Scope of evaluation
The evaluation was focused on the exposed web application. This scope encompassed assessing the security and potential vulnerabilities within this surface.
## Executive Summary 
The security assessment of the target system identified two critical vulnerabilities: Insecure Direct Object Reference (IDOR) via Social Security numbers and unrestricted file downloads. 
The IDOR vulnerability allowed an attacker to manipulate the input parameter associated with Social Security numbers, gaining unauthorized access to sensitive information belonging to other users. Additionally, the system allowed unrestricted file downloads without proper authentication, potentially leading to the exposure of sensitive files to unauthorized users. 
These vulnerabilities pose significant security risks and emphasize the need for immediate remediation to protect user data and prevent unauthorized access to critical system resources.
## Finding Summary
- IDOR
- Unrestricted file download
## Risk Impact Graph with CVSS Scores

![](https://raw.githubusercontent.com/blitz0p3rations/blitz0p3rations.github.io/master/uploads/c12.png)

## Vulnerability Types Distribution

![](https://raw.githubusercontent.com/blitz0p3rations/blitz0p3rations.github.io/master/uploads/c13.png)

## Attack storyline and findings### IDOR
- CVSS Vector: CVSS:3.0/AV:N/AC:L/PR:N/UI:N/S:U/C:L/I:L/A:L 
#### Proof of Concept (PoC)
During the security assessment, it was discovered that the application's URL structure allowed for an Insecure Direct Object Reference (IDOR) vulnerability via Social Security numbers. By manipulating the Social Security number parameter in the URL, it was possible to access other users' personal information without proper authorization. This vulnerability potentially exposed sensitive user data to unauthorized individuals.

- Vulnerable URL: https://example.com/profile?ssn=123-45-6789
- Attacker Action: Changing the Social Security number parameter to another user's value, e.g., https://example.com/profile?ssn=987-65-4321
- Outcome: The attacker gained unauthorized access to the profile information of a different user, potentially exposing their sensitive personal data.
#### Remediations
Remediating Insecure Direct Object Reference (IDOR) vulnerabilities requires careful consideration of authorization controls and data access mechanisms within an application. Here are some recommended remediation steps:

1. **Implement Proper Authorization Checks**:
   - Establish strict access controls that ensure users can only access resources and data that they are authorized to view.
   - Validate the user's identity and permissions before providing access to sensitive data or actions.

2. **Use Indirect References**:
   - Avoid directly exposing internal identifiers (such as database IDs) in URLs or other user-controlled parameters.
   - Utilize tokens or hashes that are not easily guessable or manipulated by attackers.

3. **Validate Input and Context**:
   - Implement input validation and data sanitization to prevent malicious input from bypassing authorization checks.
   - Ensure that user inputs related to authorization (such as IDs, tokens, or keys) are valid and allowed.

4. **Implement Role-Based Access Control (RBAC)**:
   - Assign roles and permissions to users based on their roles within the application.
   - Ensure that users can only access functionalities and data that are relevant to their roles.

5. **Use Session and Authentication Tokens**:
   - Implement strong session management and use secure authentication tokens to track user sessions.
   - Associate user identity with the session and use that information to determine authorized actions.

### Unrestricted file download
- CVSS Vector: CVSS:3.0/AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:N/A:N
#### Proof of Concept (PoC)
It was observed that certain files located within the restricted area of the web application were accessible for download even by non-authenticated users. 
#### Remediations
- Implement Proper Access Controls: Restrict access to files based on user authentication and authorization. Only authenticated and authorized users should be able to access and download files.

- Use Server-Side Validation: Implement server-side validation and authorization checks to ensure that users are only able to download files they are authorized to access.

- Apply Secure Directories: Store sensitive files outside of the web root directory to prevent direct access from URLs. This helps ensure that files can only be accessed through authorized means within the application.

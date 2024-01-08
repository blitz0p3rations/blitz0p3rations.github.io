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
During this assessment of the target web application, the team revealed an unrestricted file download vulnerability. An attacker could potentially download files without the need for authentication, this could lead to data exfiltration and private data of the customers of the target client. The team suggest following the remediation guidelines. 
## Finding Summary
- Unrestricted file download
## Risk Impact Graph with CVSS Scores

![](https://raw.githubusercontent.com/blitz0p3rations/blitz0p3rations.github.io/master/uploads/c1.png)

## Vulnerability Types Distribution

![](https://raw.githubusercontent.com/blitz0p3rations/blitz0p3rations.github.io/master/uploads/c2.png)

## Attack storyline and findings
### Unrestricted file download
- CVSS Vector: CVSS:3.0/AV:N/AC:L/PR:N/UI:N/S:U/C:L/I:L/A:N
#### Proof of Concept (PoC)
An unrestricted file download vulnerability is a security issue that occurs when an attacker can manipulate the application to download files from the server that they shouldn't have access to. This can lead to the unauthorized retrieval of sensitive files or even the execution of malicious files on the victim's system. 

**Proof of Concept (PoC) - Insecure Direct Object Reference (IDOR) for CV Download**
1. Identified Users:
   - User A with GUID: 8af965b3-9305-4dd5-8ff5-2cafd50a00af
   - User B with GUID: 01234567-89ab-cdef-0123-456789abcdef 

2. Observation:
   - I noticed that the ID parameter in the CV download URL is using the GUID value.
   - Memorized GUID values of both User A and User B.

3. Exploitation:
   - Attempted to access the CV of User A using User B's GUID:
     URL: .it/api/v1/attachments/curriculumVitae/download/01234567-89ab-cdef-0123-456789abcdef
   - Found that the CV of User A was successfully downloaded.
   
   - Similarly, attempted to access the CV of User B using User A's GUID:
     URL: .it/api/v1/attachments/curriculumVitae/download/8af965b3-9305-4dd5-8ff5-2cafd50a00af
   - Found that the CV of User B was also successfully downloaded.

4. Vulnerability Confirmation:
   - The ability to access the CVs of different users using their GUID values confirms the presence of an Insecure Direct Object Reference (IDOR) vulnerability.
   
Impact:
- This vulnerability allows unauthorized users to access the CVs of other users, potentially leading to a breach of confidentiality and privacy issues.

#### Remediations
- Validate User Input: Always validate and sanitize user input before using it to generate file download paths or URLs. Ensure that user-provided values cannot be manipulated to access files outside the intended directory.

- Implement Access Controls: Implement proper access controls and authorization mechanisms to prevent unauthorized users from accessing files they shouldn't have access to.

- Whitelist Allowed File Types: Allow only specific file types to be downloaded and block access to executable files or other potentially malicious content.

- Use Server-Side File Handling: Use server-side scripts to handle file downloads and restrict direct access to files through URLs.

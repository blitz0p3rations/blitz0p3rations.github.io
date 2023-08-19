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
The assessment of the school's Content Management System (CMS) identified two critical security vulnerabilities: SQL Injection (SQLi) and Unrestricted File Upload. Both vulnerabilities pose significant risks to the confidentiality, integrity, and availability of the system and the data it handles. Exploiting this vulnerability can allow unauthorized access to the underlying database, potentially leading to data exposure, data manipulation, or even unauthorized access to the system.
## Finding Summary
- SQL Injection (SQLi)
- Unrestricted file upload
## Attack storyline or vulnerabilities with CVSS,CVE and remedations
### SQL Injection (SQLi)
- CVSS Vector: CVSS:3.0/AV:N/AC:L/PR:N/UI:N/S:C/C:H/I:H/A:H
#### Proof of Concept (PoC)
#### Proof of Concept (PoC)
A time-based SQL injection vulnerability was identified in the POST request sent to the endpoint `/admin/technical/MessageAction`. The vulnerable parameter that can be exploited is `filter_email`.

**Vulnerable Endpoint:** /admin/technical/MessageAction

**Vulnerable Parameter:** filter_email

**Payload:** 
`
1 | as' AND (SELECT 9802 FROM (SELECT(SLEEP(5)))pLMs) AND 'ddyw'='ddyw&filter_status=as
`

When this payload is injected into the "filter_email" parameter, it triggers a time delay of approximately 5 seconds in the SQL query execution. This delay indicates a successful exploitation of the time-based SQL injection vulnerability.

#### Remediations
- Input Validation and Sanitization: Always validate and sanitize user inputs before using them in SQL queries. Use parameterized queries or prepared statements to separate user inputs from the SQL code.

- Use ORM Frameworks: Consider using Object-Relational Mapping (ORM) frameworks that generate SQL queries automatically. These frameworks help prevent direct SQL injection by handling database interactions using safe methods.

- Whitelist Input: Define acceptable input patterns using whitelists. Only allow specific characters and formats in user inputs, rejecting any input that doesn't adhere to the whitelist.

### Unrestricted file upload
- CVSS Vector: None
#### Proof of Concept (PoC)
The provided Proof of Concept (PoC) demonstrates an unrestricted file upload vulnerability in a web application, allowing the upload of .zip and .exe files that can later be downloaded by users from the backend.

1. **Scenario:**
   - Web Application: VulnerableApp
   - Upload Form: /upload

2. **Steps:**
   a. Access the upload form within the web application.

   b. Fill in the form with the necessary details:
      - Select File: Choose a .zip or .exe file to upload.
      - Additional Information: Provide any relevant information.

   c. Submit the form to upload the chosen file.

3. **Impact:**
   - The uploaded .zip and .exe files are stored on the server.
   - The backend lacks proper access controls, allowing unauthorized users to access uploaded files.






#### Remediations
- File Type Verification: Allow only specific file types that are required for your application. Reject files with file extensions that are not expected or necessary.

- File Size Limitation: Implement maximum file size restrictions to prevent users from uploading excessively large files that could potentially cause denial of service or other issues.

- File Content Validation: Check the content of uploaded files to ensure they adhere to expected formats. For example, you can use file validation libraries to verify that uploaded images are indeed images and not executable scripts.

- Rename Uploaded Files: Rename uploaded files to a unique name using a combination of random characters and timestamps. This prevents attackers from guessing or overwriting existing files.

- Isolate Uploaded Files: Store uploaded files in a separate directory outside of the web root, ensuring they cannot be directly accessed via URL. Use server-side scripts to serve files to users.

- Implement Content Disposition Headers: Set proper content disposition headers when serving files to users. This can prevent browsers from automatically executing certain file types, such as scripts.

- Scan for Malware: Implement a system to scan uploaded files for malware or suspicious content before allowing them to be stored on the server.

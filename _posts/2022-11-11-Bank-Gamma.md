---
layout: post
title: 'Bank Gamma external PT'
tags:
 - web
 - real-engagement
hero: https://images.unsplash.com/photo-1501167786227-4cba60f6d58f?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxzZWFyY2h8Mnx8YmFua3xlbnwwfHwwfHx8MA%3D%3D&auto=format&fit=crop&w=400&q=60
overlay: red
---

No images (image for the step by step PoC are essential as evidence but will not be provided
) or references will be provided, as this assessment was a real engagement. Additionally, all URLs and functionalities have been anonymized to ensure privacy and compliance with non-disclosure agreements (NDAs). {: .lead} <!--break-->

# Bank Gamma

## Type of activity and objectives
The objective of this engagement was to conduct an external penetration assessment for the organization. The aim was to identify potential vulnerabilities that could potentially be exploited from outside sources, with the goal of preventing unauthorized access, compromise and data exfiltration.
## Scope of evaluation
The evaluation was focused on the outised surface of the organization. This scope encompassed assessing the security and potential vulnerabilities within this external surface.
## Executive Summary

## Finding Summary
- Yoast SEO < 17.3 - Unauthenticated Full Path Disclosure (CVE-2021-25118)
- x2 From Exposed .git to dump of the appliations with secrets
- SQL Injection (SQLi)
- Cross Site Scripting (XSS)
## Attack storyline or vulnerabilities with CVSS,CVE and remedations
###  Yoast SEO < 17.3 - Unauthenticated Full Path Disclosure (CVE-2021-25118)
- CVSS Vector: CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:U/C:L/I:N/A:N
#### Proof of Concept (PoC) 
The Yoast SEO WordPress plugin (from versions 16.7 until 17.2) discloses the full internal path of featured images in posts via the wp/v2/posts REST endpoints which could help an attacker identify other vulnerabilities or help during the exploitation of other identified vulnerabilities.

- curl -s 'https://target.com/wp-json/wp/v2/posts?per_page=1' | jq '.[0].yoast_head_json.og_image[0].path' 
#### Remediations
- Update the plugin

### x2 From Exposed .git to dump of the appliations with secrets
- CVSS Vector: None
#### Proof of Concept (PoC) 
In the course of the assessment, it was identified that two primary web applications had an exposed .git folder. This oversight enabled unauthorized access to the contents of the .git directory, thereby exposing a wide range of sensitive information. The extracted data included secrets related to OTP generation, private SSH keys for intranet access, database credentials, admin credentials, and other crucial credentials.#### Remediations
- Restrict access to the .git directory

### SQL Injection (SQLi)
- CVSS Vector: CVSS:3.0/AV:N/AC:L/PR:N/UI:N/S:C/C:H/I:H/A:H
#### Proof of Concept (PoC) 
The provided Proof of Concept (PoC) demonstrates the presence of a time-based SQL injection vulnerability in the "getCorsiTipologie" action of the "/Controllers/PostsHandler.ashx" path. This vulnerability allows an attacker to manipulate the input parameters in such a way that they can influence the behavior of the underlying SQL query.

In the given payload:

**action=getCorsiTipologie&tipologie=-1) AND 3951 IN (SELECT (CHAR(113)+CHAR(113)+CHAR(122)+CHAR(122)+CHAR(113)+(SELECT (CASE WHEN (3951=3951) THEN CHAR(49) ELSE CHAR(48) END))+CHAR(113)+CHAR(120)+CHAR(112)+CHAR(122)+CHAR(113))) AND (5833=5833&_=1666769259298**

The part **-1) AND 3951 IN (SELECT ...** is attempting to inject malicious SQL code into the query. The provided SQL code appears to create a boolean condition that is always true (3951=3951) and generates certain character sequences. This type of payload is often used to create time delays in the SQL query execution, allowing an attacker to infer whether the injection is successful based on the observed delay.

The vulnerability could spotentially allow an attacker to gather sensitive information from the database or manipulate its behavior by crafting malicious SQL queries.

#### Remediations
- To remediate this vulnerability, it's recommended to implement proper input validation, parameterized queries, and prepared statements to prevent SQL injection attacks. 
### Cross Site Scripting (XSS)
- CVSS Vector: CVSS:3.0/AV:N/AC:L/PR:N/UI:N/S:U/C:L/I:N/A:N
#### Proof of Concept (PoC) 
During the course of the tests, it was possible to perform JavaScript code injection by setting the value of the "startSlide" parameter with the following payload: **336563';alert(1)//686** in URL encoding. The injected payload triggers an alert(1) JavaScript function. Below is the request made and its corresponding response.
#### Remediations
- Input Validation and Sanitization: Ensure that all user inputs are validated and sanitized properly before they are used in any part of the application, including HTML content.

- Output Encoding: Encode dynamic content that is being inserted into HTML, JavaScript, or other contexts. This prevents the browser from treating user input as executable code.
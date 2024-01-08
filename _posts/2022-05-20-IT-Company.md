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
The objective of this engagement was to conduct a web application penetration test for the organization. The aim was to identify potential vulnerabilities that could potentially be exploited from the outside, with the goal of preventing unauthorized access, compromise and data exfiltration.
## Scope of evaluation
The evaluation was focused on the exposed web application. This scope encompassed assessing the security and potential vulnerabilities within this surface.
## Executive Summary 
The assessment of the target system revealed three critical security vulnerabilities: Path Traversal, XML External Entity (XXE) Injection, and LDAP Injection. Each of these vulnerabilities presents significant risks to the security and integrity of the application.

Path Traversal exposes the system to unauthorized file access, XXE Injection could lead to data leakage or server-side request forgery, and LDAP Injection may allow unauthorized query and data manipulation within the application. The identification of these vulnerabilities highlights the need for immediate remediation to safeguard the application and protect sensitive data.
## Finding Summary
- Path Traversal
- XXE
- LDAP Injection
## Risk Impact Graph with CVSS Scores

![](https://raw.githubusercontent.com/blitz0p3rations/blitz0p3rations.github.io/master/uploads/id13.png)

## Vulnerability Types Distribution

![](https://raw.githubusercontent.com/blitz0p3rations/blitz0p3rations.github.io/master/uploads/id14.png)

## Attack storyline and findings### Path Traversal
- CVSS Vector: CVSS:3.0/AV:N/AC:L/PR:N/UI:N/S:U/C:L/I:L/A:L
#### Proof of Concept (PoC)
Path traversal is a vulnerability that occurs when an attacker can manipulate file paths to access files or directories outside of the intended scope. This can lead to unauthorized access to sensitive files, including configuration files, source code, or even system files. If exploited, this vulnerability could result in a breach of confidential data or compromise the integrity of the system.

In the URL path "secure/getVersionFile?fileName=x1v1-viewerwebversion.properties," there is a path traversal vulnerability. By altering the value of the "fileName" parameter with the following payload in URL encoding: "../../../../../../../../../../../../../../../../etc/passwd," an attacker can navigate to sensitive system files such as the "/etc/passwd" file.
#### Remediations
- Input Validation and Whitelisting: Implement strict input validation and use whitelisting to restrict user input to expected values or patterns. Only allow specific characters and prevent the use of "../" or other traversal indicators.

- Apply Contextual Output Encoding: Use output encoding appropriate for the output context. This prevents user-controlled input from being interpreted as code by the application.

- Use Absolute Paths: Avoid using relative paths in your application, and use absolute paths to access files and resources. This reduces the risk of traversal.
### XXE
- CVSS Vector: CVSS:3.0/AV:N/AC:L/PR:N/UI:N/S:C/C:L/I:L/A:Lone
#### Proof of Concept (PoC)
XXE is a vulnerability that occurs when an attacker is able to include external entities in XML input, leading to disclosure of internal files, server-side request forgery (SSRF), or even remote code execution. XXE attacks can have severe consequences, allowing attackers to extract sensitive information or perform malicious actions on the server.

XXE (External Entity Interaction - HTTP & DNS)
Add the following payload, include an arbitrary entity name, and the URL of the Burp Collaborator:
`<!DOCTYPE foo [ <!ENTITY xxe SYSTEM "http://burpcollaborator.net"> ]> `
Insert this payload after the initial XML declaration and reference the created entity using `&entityID;` right after the first `https://localhost:9443/samlsso` URL. 
Re-encode the payload and forward the request. In a matter of seconds, the Collaborator should receive the out-of-band interactions, and as expected, the detected IPs confirm an interaction.

#### Remediations
- Disable External Entities: In your XML parser's configuration, disable the processing of external entities. This prevents the parser from fetching external resources referenced in the XML document.

- Input Validation: Implement strict input validation for XML input. Ensure that user-provided input is properly sanitized and doesn't allow external entity references or doctype declarations.

- Use Whitelists: Define a whitelist of allowed elements, attributes, and entities in your XML documents. Reject any input that doesn't match the whitelist.

- Upgrade Libraries: Keep XML processing libraries up to date. Newer versions often include security enhancements that mitigate XXE vulnerabilities.

Sandboxing: If you need to process XML with untrusted content, consider using a sandboxed environment that limits access to external resources.
### LDAP Injection
- CVSS Vector: CVSS:3.0/AV:N/AC:L/PR:N/UI:N/S:C/C:L/I:L/A:Lone
#### Proof of Concept (PoC)
In the context of the login process, a LDAP injection vulnerability was identified. This vulnerability occurs in the "user" and "psw" parameters of a POST request. By injecting the payload **")(objectClass=*,"** an attacker can manipulate the LDAP query to retrieve a wide range of objects, bypassing authentication. 
#### Remediations
- Parameterized Queries: Use parameterized queries or prepared statements provided by your programming language or framework to handle LDAP queries. Parameterization ensures that user input is properly sanitized and separated from the query logic.

- Input Validation and Sanitization: Validate and sanitize user input before constructing LDAP queries. Ensure that input values match expected formats and reject any input that contains special characters used in LDAP queries.

- Least Privilege: Set appropriate access controls and permissions on LDAP server objects to restrict access to only necessary resources. Users should have the minimum required privileges to perform their tasks.

- Escaping Special Characters: If input needs to be used directly in queries, escape special characters like *, (, ), , and = before constructing the query.

- Whitelisting: Maintain a whitelist of allowed characters or patterns for input fields that will be used in LDAP queries. Reject any input that doesn't match the whitelist.

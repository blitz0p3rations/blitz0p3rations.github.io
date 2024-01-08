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
The assessment of the target web application identified a security vulnerability related to HTML injection. This type of vulnerability occurs when user-provided data is improperly validated and injected into the HTML output of the application, potentially allowing an attacker to execute malicious scripts or manipulate the content displayed to users.
## Finding Summary
- HTML Injection
## Risk Impact Graph with CVSS Scores

![](https://raw.githubusercontent.com/blitz0p3rations/blitz0p3rations.github.io/master/uploads/id11.png)

## Vulnerability Types Distribution

![](https://raw.githubusercontent.com/blitz0p3rations/blitz0p3rations.github.io/master/uploads/id12.png)

## Attack storyline and findings
### IDOR
- CVSS Vector: CVSS:3.0/AV:N/AC:L/PR:N/UI:N/S:U/C:N/I:L/A:N
#### Proof of Concept (PoC)

The provided Proof of Concept (PoC) demonstrates the discovery of an HTML injection vulnerability within the target application. By using the payload **"param":"<a href=https://google.com>click here</a>"**, an attacker was able to inject HTML content into the application's user interface. This particular injection occurred in the context of the URL path app/#/ticketdetail/401.

HTML injection vulnerabilities can have serious consequences, potentially leading to cross-site scripting (XSS) attacks, data manipulation, and other security breaches. Remediation for this vulnerability would involve implementing input validation and output encoding to ensure that user-provided content is properly sanitized and rendered safely within the application
#### Remediations
- Input Validation: Validate and sanitize user inputs to prevent the injection of malicious code. Use whitelists to allow only specific types of input and reject anything that doesn't adhere to the allowed patterns.

- Output Encoding: Encode all dynamic data rendered in the HTML output to ensure that any user-provided content is displayed as plain text and not executed as code. Use context-specific encoding functions, such as HTML escaping, to prevent script execution.

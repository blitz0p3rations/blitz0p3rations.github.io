---
layout: post
title: 'Betting Company external PT'
tags:
 - web
 - real-engagement
hero: https://plus.unsplash.com/premium_photo-1670005278847-3398f72aecdc?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1470&q=80
overlay: red
---

No images (images for the step-by-step PoC are essential as evidence but will not be provided
) or references will be provided, as this assessment was a real engagement. Additionally, all URLs and functionalities have been anonymized to ensure privacy and compliance with non-disclosure agreements (NDAs). {: .lead} <!--break-->

# Betting Company

## Type of activity and objectives
The objective of this engagement was to conduct an external penetration assessment for the organization. The aim was to identify potential vulnerabilities that could potentially be exploited from outside sources, to prevent unauthorized access, compromise and data exfiltration.
## Scope of evaluation
The evaluation was focused on the outside surface of the organization. This scope encompassed assessing the security and potential vulnerabilities within this external surface.
## Executive Summary
The assessment revealed a Cross-Site Scripting (XSS) vulnerability in the web application. This vulnerability could potentially allow attackers to inject malicious scripts into the application, leading to the execution of arbitrary code or the theft of sensitive information. It is recommended that appropriate remediation steps be taken to address this security issue and ensure the protection of user data and the application's integrity.
## Finding Summary
- Cross-Site Scripting (XSS)
## Attack storyline or vulnerabilities with CVSS, CVE and remediations
### Cross-Site Scripting (XSS)
- CVSS Vector: None
#### Proof of Concept (PoC) 
The provided Proof of Concept demonstrates an example of a Cross-Site Scripting (XSS) vulnerability within the target CMS. In this case, the payload is injected into the "payment provider" parameter. The payload used is:

- **paymentprovider=sd'%3balert(1)%2f%2f253**


This payload takes advantage of improper input sanitization, allowing malicious JavaScript code to be executed in the context of other users' sessions. When this payload is processed and rendered by the web application, it triggers an alert box with the message "1".


#### Remediations
- Input Validation and Sanitization: Ensure that all user-provided input is properly validated and sanitized before being displayed on web pages. Use input validation libraries or frameworks to filter out malicious code and special characters.

- Output Encoding: Encode any user-generated content that is displayed in HTML, JavaScript, or other contexts to prevent it from being treated as executable code.

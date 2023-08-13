---
layout: post
title: 'IT Company Web Applicaion PT'
tags:
 - web
 - real-engagement
hero: https://images.unsplash.com/photo-1462206092226-f46025ffe607?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1474&q=80
overlay: blue
---

No images (image for the step by step PoC are essential as evidence but will not be provided
) or references will be provided, as this assessment was a real engagement. Additionally, all URLs and functionalities have been anonymized to ensure privacy and compliance with non-disclosure agreements (NDAs). {: .lead} <!--break-->

# IT Company

## Type of activity and objectives
The objective of this engagement was to conduct a web application penetration test for the organization. The aim was to identify potential vulnerabilities that could potentially be exploited from the outside, with the goal of preventing unauthorized access, compromise and data exfiltration.
## Scope of evaluation
The evaluation was focused on the exposed web application. This scope encompassed assessing the security and potential vulnerabilities within this surface.
## Executive Summary 
During the assessment of the target web application, two significant vulnerabilities were identified. Firstly, the application's Swagger documentation was found to be exposed, allowing unauthorized access to sensitive information about the application's APIs and functionality. Secondly, a lack of rate limiting in the SMS sending functionality of the application allowed for the potential abuse of sending an unlimited number of SMS messages.
## Finding Summary
- Exposed Swagger Documentation
- No rate limit lead to sending infinitive SMS
## Attack storyline or vulnerabilities with CVSS,CVE and remedations
### IDOR
- CVSS Vector: None
#### Proof of Concept (PoC)
During the assessment of the target web application, it was observed that the Swagger documentation for the application's APIs was accessible without proper authentication. The following URL led to the exposed Swagger documentation:
```
https://example.com/swagger/index.html
```
#### Remediations
- Restrict access to this resource
### No rate limit lead to sending infinitive SMS
- CVSS Vector: None
#### Proof of Concept (PoC)
The Proof of Concept (PoC) highlights an issue where the endpoint "/api/v1/Auth/resend" was exploited to send an unlimited number of SMS messages, bypassing any rate limiting mechanisms that should have been in place. This misuse of the functionality could potentially overwhelm the recipient with an excessive volume of SMS messages, causing service disruption and degrading the user experience.

It is imperative to address this vulnerability by implementing robust rate limiting and abuse prevention mechanisms for the SMS sending functionality. By setting appropriate limits on the number of SMS messages that can be sent within a specific time frame, the application can prevent abuse and ensure that its resources are not misused for malicious purposes.
#### Remediations
- Introduce rate limiting mechanisms for the SMS sending functionality
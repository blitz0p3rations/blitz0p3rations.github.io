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
The objective of this engagement was to conduct a web application penetration test for the organization. The aim was to identify potential vulnerabilities that could potentially be exploited from the outside, with the goal of preventing unauthorized access, compromise and data exfiltration.
## Scope of evaluation
The evaluation was focused on the exposed web application. This scope encompassed assessing the security and potential vulnerabilities within this surface.
## Executive Summary 
During the assessment of the target web application, one significant vulnerabilities were identified. Firstly, the application's Swagger documentation was found to be exposed, allowing unauthorized access to sensitive information about the application's APIs and functionality. 
## Finding Summary
- Exposed Swagger Documentation
## Risk Impact Graph with CVSS Scores

![](https://raw.githubusercontent.com/blitz0p3rations/blitz0p3rations.github.io/master/uploads/id6.png)

## Vulnerability Types Distribution

![](https://raw.githubusercontent.com/blitz0p3rations/blitz0p3rations.github.io/master/uploads/id7.png)

## Attack storyline and findings
### Exposed Swagger Documentation
- CVSS Vector: None
#### Proof of Concept (PoC)
During the assessment of the target web application, it was observed that the Swagger documentation for the application's APIs was accessible without proper authentication. The following URL led to the exposed Swagger documentation:
`
https://example.com/swagger/index.html
`
#### Remediations
- Restrict access to this resource

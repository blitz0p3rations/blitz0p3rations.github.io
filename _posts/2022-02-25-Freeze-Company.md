---
layout: post
title: 'Freeze Company External PT'
tags:
 - web
 - real-activity
hero: https://images.unsplash.com/photo-1538108149393-fbbd81895907?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1528&q=80
overlay: blue
---

Please note that for this proof of concept, while images and step-by-step reproduction tips are fundamental for evidentiary purposes, they will not be supplied. Furthermore, in adherence to our commitment to privacy and compliance with non-disclosure agreements, all URLs and functionalities within this assessment have been anonymized. {: .lead}
 <!--break-->

# Freeze Company

## Type of activity and objectives
The objective of this engagement was to conduct an external penetration assessment for the organization. The aim was to identify potential vulnerabilities that might be exploited by external sources, with the ultimate goal of preventing unauthorized access and compromise.
## Scope of evaluation
The evaluation was focused on the specific website of the organization. This scope encompassed assessing the security and potential vulnerabilities within this website.
## Executive Summary
The security assessment conducted on the Content Management System (CMS) of the target website has identified a critical vulnerability that could potentially lead to user disclosure. This finding highlights a significant risk to user privacy and the security of sensitive information stored within the CMS.

The vulnerability allows unauthorized individuals to gain access to user-related data, such as personal information, login credentials, and other sensitive details, stored on the CMS nodes. Such unauthorized access can result in privacy breaches, identity theft, and the exposure of confidential information to malicious actors.
## Finding Summary
- Secrets disclosure from CMS nodes
## Risk Impact Graph with CVSS Scores

![](https://raw.githubusercontent.com/blitz0p3rations/blitz0p3rations.github.io/master/uploads/id1.png)

## Vulnerability Types Distribution

![](https://raw.githubusercontent.com/blitz0p3rations/blitz0p3rations.github.io/master/uploads/id2.png)

## Attack storyline and findings### Secrets disclosure from CMS nodes
- CVSS Vector: None
#### Proof of Concept (PoC) 
The PoC involved examining the CMS nodes and their contents, revealing the presence of secrets, user-related data, and confidential information. By accessing these nodes, an attacker could potentially extract sensitive details, compromise user accounts, and gain unauthorized access to restricted areas of the CMS.
#### Remediations
- The organization should implement strict access controls and permissions for CMS nodes, ensuring that only authorized personnel can view and manipulate sensitive information.
- Delete secrets from nodes.



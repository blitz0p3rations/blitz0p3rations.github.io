---
layout: post
title: Stockings Brand Web PT
tags:
  - web
  - real-activity
hero: https://images.unsplash.com/photo-1462206092226-f46025ffe607?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1474&q=80
overlay: blue
---

Please note that for this proof of concept, while images and step-by-step reproduction tips are fundamental for evidentiary purposes, they will not be supplied. Furthermore, in adherence to our commitment to privacy and compliance with non-disclosure agreements, all URLs and functionalities within this assessment have been anonymized. {: .lead} <!–-break-–>

# Stockings Brands Mobile PT Android & IOS

## Type of activity and objectives
The objective of this engagement was to conduct a Mobile IOS & Android penetration assessment for the two organization mobile apps used by the sales branches to manage the shop. The aim was to identify potential vulnerabilities that might be exploited by external sources, with the ultimate goal of preventing unauthorized access and compromise.
## Scope of evaluation
The evaluation was focused on the mobile apps of the organization. This scope encompassed assessing the security and potential vulnerabilities within this  surface.
## Executive Summary

The Web Application Penetration Test conducted on the defined perimeter revealed the presence of vulnerabilities related to HTML Injection and Broken Access Control (IDOR).

The first issue, HTML Injection, if exploited, could potentially redirect users to domains controlled by the attacker. This vulnerability can facilitate social engineering attacks by altering elements and styles on the page.

The second issue, Broken Access Control (IDOR), allows various user profiles assigned to respective stores to view data related to staff, schedules, and services belonging to other stores. This vulnerability exposes sensitive information and undermines the intended access controls within the application.
## Finding Summary
- HTML Injection
- IDOR
## Risk Impact Graph with CVSS Scores

## Vulnerability Types Distribution



## Attack storyline and findings
### HTML Injection
- CVSS Vector: AV:N/AC:L/PR:N/UI:N/S:U/C:N/I:L/A:N
#### Proof of Concept (PoC) 
To verify the presence of the vulnerability, the team introduced arbitrary HTML elements, such as titles or images, into the application. These elements were then interpreted by the application as part of the HTML markup, thereby confirming the existence of the HTML Injection vulnerability.

To reproduce the described scenario, it is sufficient to insert the following payload `<h1>Blitz<h1>` into the daily work input form, as all parameters are found to be vulnerable. This method demonstrates the application's failure to properly sanitize input, allowing for the injection of arbitrary HTML.

#### Remediations
- Input Validation and Sanitization: Implement rigorous input validation and sanitization to prevent malicious data from being processed. This is particularly important for mitigating risks associated with HTML Injection and Cross-Site Scripting (XSS).

### IDOR
- CVSS Vector: AV:N/AC:L/PR:N/UI:N/S:U/C:N/I:L/A:N](AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:N/A:N
#### Proof of Concept (PoC) 
In the first scenario, using the account assigned to USER1 (store F336), it was possible to view the staff members belonging to store 18034. Simply modifying the value of the X-Request-Store header allowed access to data from other stores. Similarly, using the account assigned to USER2 (store 18034), it was possible to view additional information about store F336. As before, with the accounts belonging to USER1 and USER2 (store 18034), viewing arbitrary stores was feasible, with further evidence provided below.

This scenario indicates a Broken Access Control vulnerability, specifically IDOR (Insecure Direct Object References), where insufficient access validation allows users to view data beyond their authorized scope by manipulating request parameters or headers.

#### Remediations
Data-level access controls should be implemented such that the server verifies whether the current user account has the necessary permissions for the requested functionality. Consequently, resource access should only be allowed after the server has performed a check on the user's privileges.
Include session and authorization controls to confirm that users are authenticated and authorized to access specific resources.



`



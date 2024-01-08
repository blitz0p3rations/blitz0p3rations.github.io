---
layout: post
title: 'Betting Company external PT'
tags:
 - web
 - real-activity
hero: https://plus.unsplash.com/premium_photo-1670005278847-3398f72aecdc?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1470&q=80
overlay: red
---

Please note that for this proof of concept, while images and step-by-step reproduction tips are fundamental for evidentiary purposes, they will not be supplied. Furthermore, in adherence to our commitment to privacy and compliance with non-disclosure agreements, all URLs and functionalities within this assessment have been anonymized. {: .lead}
 <!--break-->

# Betting Company

## Type of activity and objectives
The objective of this engagement was to conduct an external penetration assessment for the organization. The aim was to identify potential vulnerabilities that might be exploited by external sources, with the ultimate goal of preventing unauthorized access and compromise.
## Scope of evaluation
The evaluation was focused on the outside surface of the organization. This scope encompassed assessing the security and potential vulnerabilities within this external surface.
## Executive Summary
The assessment revealed a Cross-Site Scripting (XSS) vulnerability in the web application. This vulnerability could potentially allow attackers to inject malicious scripts into the application, leading to the execution of arbitrary code or the theft of sensitive information. It is recommended that appropriate remediation steps be taken to address this security issue and ensure the protection of user data and the application's integrity.
## Finding Summary
- Cross-Site Scripting (XSS)
## Risk Impact Graph with CVSS Scores

![](https://raw.githubusercontent.com/blitz0p3rations/blitz0p3rations.github.io/master/uploads/id21.png)

## Vulnerability Types Distribution

![](https://raw.githubusercontent.com/blitz0p3rations/blitz0p3rations.github.io/master/uploads/id22.png)

## Attack storyline and findings### Cross-Site Scripting (XSS)
- CVSS Vector: None
#### Proof of Concept (PoC) 
The provided Proof of Concept demonstrates an example of a Cross-Site Scripting (XSS) vulnerability within the target CMS. In this case, the payload is injected into the "payment provider" parameter. The payload used is:

- **paymentprovider=sd'%3balert(1)%2f%2f253**


This payload takes advantage of improper input sanitization, allowing malicious JavaScript code to be executed in the context of other users' sessions. When this payload is processed and rendered by the web application, it triggers an alert box with the message "1".


#### Remediations
- Input Validation and Sanitization: Ensure that all user-provided input is properly validated and sanitized before being displayed on web pages. Use input validation libraries or frameworks to filter out malicious code and special characters.

- Output Encoding: Encode any user-generated content that is displayed in HTML, JavaScript, or other contexts to prevent it from being treated as executable code.

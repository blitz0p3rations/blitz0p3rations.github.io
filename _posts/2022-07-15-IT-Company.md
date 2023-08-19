---
layout: post
title: 'IT Company Web Applicaion PT'
tags:
 - web
 - real-engagement
hero: https://images.unsplash.com/photo-1462206092226-f46025ffe607?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1474&q=80
overlay: red
---

No images (image for the step by step PoC are essential as evidence but will not be provided
) or references will be provided, as this assessment was a real engagement. Additionally, all URLs and functionalities have been anonymized to ensure privacy and compliance with non-disclosure agreements (NDAs). {: .lead} <!--break-->

# IT Company

## Type of activity and objectives
The objective of this engagement was to conduct a web application penetration test for the organization. The aim was to identify potential vulnerabilities that could potentially be exploited from the outside, with the goal of preventing unauthorized access, compromise and data exfiltration.
## Scope of evaluation
The evaluation was focused on the exposed web application. This scope encompassed assessing the security and potential vulnerabilities within this surface.
## Executive Summary 
The assessment identified Cross-Site Scripting (XSS) vulnerabilities within the target application. These vulnerabilities could potentially allow malicious attackers to inject and execute arbitrary JavaScript code in the context of other users' browsers, compromising their sessions and stealing sensitive information. The XSS vulnerabilities pose a serious threat to the confidentiality, integrity, and availability of the application and its users' data.
## Finding Summary
- Cross Site Scripting (XSS)
## Attack storyline or vulnerabilities with CVSS,CVE and remedations
### Path Traversal
- CVSS Vector: CVSS:3.0/AV:N/AC:L/PR:N/UI:N/S:U/C:L/I:L/A:N
#### Proof of Concept (PoC)
Cross-Site Scripting (XSS) is a type of security vulnerability commonly found in web applications. It occurs when an attacker is able to inject malicious scripts, usually in the form of HTML or JavaScript, into a web page that is then viewed by other users. This can happen when user input is not properly validated or sanitized before being displayed on a web page.

It was possible to exploit a Cross-Site Scripting (XSS) vulnerability by injecting the following payload:

`
 .it/exec/Jet/%5EJetJfVsSesst0/90xp2ez%3cscript%3ealert(1)%3c/script%3ewozs
 e z.it/exec/Jet/WebJmVsJolog0.anagSearch/90?
 SESSIONID=1657524558585w0nnw%3cscript%3
 ealert(1)%3c%2fscript%3ewpbq1rgx0r9&FORMORD=0&CURRENTRECORD=-
 1&nomecoda=FAST&JMCDUTES=qwqq&JMNMHOST=1&JMNMJOBE=qwqwqw&JMDSJOBE=wqwqw&es
 ito=F&JMNMDSPE=qwqwq&DTINIZDA=11%2F07%2F2022&DTINIZAL=11%2F07%2F2022&DTFINED
 A=&DTF
INEAL=&DTSOTTDA=&DTSOTTAL=&ORAINIDA=&ORAINIAL=&ORAFINDA=&ORAFINAL=&ORASOTD
A=&OR
ASOTAL=&IDJOB=&CODA=FAST&ESITO=F&RICTER=N&CHDTIN=N&CHDTFI=N&CHDTSO=N&UT=A
`

By injecting this payload, an attacker was able to execute arbitrary JavaScript code within the context of the application, potentially leading to session compromise, unauthorized data access, and other malicious activities. It is crucial to remediate this vulnerability by implementing input validation, output encoding, and context-aware security measures to prevent such attacks and safeguard the application and its users.
#### Remediations
- Input Validation and Sanitization: Ensure that all user input is properly validated and sanitized before it is displayed on a web page. This can involve stripping out or encoding potentially dangerous characters.

- Output Encoding: Encode user-generated content before it is displayed in the browser to prevent the execution of malicious scripts.

---
layout: post
title: 'Bank Gamma Web Application PT'
tags:
 - web
 - real-engagement
hero: https://images.unsplash.com/photo-1501167786227-4cba60f6d58f?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxzZWFyY2h8Mnx8YmFua3xlbnwwfHwwfHx8MA%3D%3D&auto=format&fit=crop&w=400&q=60
overlay: blue
---

No images (images for the step-by-step PoC are essential as evidence but will not be provided
) or references will be provided, as this assessment was a real engagement. Additionally, all URLs and functionalities have been anonymized to ensure privacy and compliance with non-disclosure agreements (NDAs). {: .lead} <!--break-->

# Bank Gamma

## Type of activity and objectives
The objective of this engagement was to conduct an external penetration assessment for the organization. The aim was to identify potential vulnerabilities that could potentially be exploited from the outside, to prevent unauthorized access, compromise and data exfiltration.
## Scope of evaluation
The evaluation was focused on the outside surface. This scope encompassed assessing the security and potential vulnerabilities within this surface.
## Executive Summary
The assessment of the target system identified the presence of two vulnerabilities, namely CVE-2005-2204 and CVE-2007-5923, both categorized as DOM-based Cross-Site Scripting (XSS) vulnerabilities. These vulnerabilities pose a significant security risk as they allow attackers to inject malicious scripts directly into the Document Object Model (DOM) of a web application, leading to the potential execution of arbitrary code within the context of a user's browser.
## Finding Summary
- CVE-2005-2204 and CVE-2007-5923 DOM Cross-Site Scripting (XSS)
## Attack storyline or vulnerabilities with CVSS, CVE and remediations

### DOM Cross-Site Scripting (XSS)
- CVSS Vector: CVSS:3.0/AV:N/AC:L/PR:N/UI:N/S:U/C:L/I:N/A:N
#### Proof of Concept (PoC)
DOM-based XSS vulnerabilities arise when an application incorporates unvalidated user input into its dynamic content, which is subsequently processed by the browser. Exploiting these vulnerabilities can lead to unauthorized access, data theft, session hijacking, and other malicious actions, jeopardizing both the security and privacy of users.

The present vulnerability stems from the implementation of fixes related to CVE-2005-2204 and CVE-2007-5923 using the "BadCSSChars" and "BadUrlChars" parameters. Particularly, the configuration of the second parameter is found incapable of blocking certain characters that allow a potential attacker to execute arbitrary JavaScript code on the vulnerable target. Exploiting this specific vulnerability, a potential attacker could inject arbitrary JavaScript code into the application's response, enabling them to carry out a wide range of actions, such as stealing the victim's session token or login credentials, performing arbitrary actions on behalf of the victim, and capturing all input entered into the generated input form.

The vulnerability, categorized as reflected DOM-based Cross-Site Scripting (XSS), occurs when an application receives data in an HTTP request and includes this data within the Document Object Model (DOM) of the response. This response is then processed unsafely by a client-side script. In the case of the URL under analysis, the "Username" parameter is integrated into the application's response DOM. Subsequently, the content is parsed by a client-side script. By inputting a payload encoded in Unicode, it became possible to execute arbitrary JS code on the vulnerable target. Below are the original payload and the payload in Unicode encoding:

- Original Payload: `<img src=x onerror="confirm(document.domain)">`
- Unicode Encoded Payload: `=\u003cimg\u0020src\u003dx\u0020onerror\u003d\u0022confirm(document.domain)\u0022\u0020\u003e`
#### Remediations
- Input Validation and Output Encoding: Validate and sanitize all user inputs on both the server and client sides. Ensure that any input is properly validated and that the output is correctly encoded to prevent malicious scripts from being executed.

- Contextual Output Encoding: Depending on the context in which data is displayed, apply appropriate output encoding mechanisms. Different contexts require different encoding methods.

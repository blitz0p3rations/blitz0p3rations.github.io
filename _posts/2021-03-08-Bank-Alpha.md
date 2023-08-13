---
layout: post
title: 'Bank Alpha External PT'
tags:
 - web
 - real-engagement
hero: https://images.unsplash.com/photo-1501167786227-4cba60f6d58f?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1470&q=80
overlay: red
---

No images (image for the step by step PoC are essential as evidence but will not be provided
) or references will be provided, as this assessment was a real engagement. Additionally, all URLs and functionalities have been anonymized to ensure privacy and compliance with non-disclosure agreements (NDAs). {: .lead} <!--break-->

# Bank Alpha

## Type of activity and objectives
The objective of this engagement was to conduct an external penetration assessment for the bank. The aim was to identify potential vulnerabilities that could potentially be exploited from outside sources, with the goal of preventing unauthorized access and compromise.
## Scope of evaluation
The evaluation was focused on the specific netblock assigned to the organization. This scope encompassed assessing the security and potential vulnerabilities within this network range.
## Executive Summary
During the recent security assessment conducted for Bank Alpha, two significant vulnerabilities were identified within the company's external infrastructure. 

- Cross-Site Scripting (XSS) Vulnerability: The security assessment uncovered a critical Cross-Site Scripting (XSS) vulnerability within the application. This vulnerability allows attackers to inject malicious code into web pages viewed by other users. By exploiting this vulnerability, an attacker could execute arbitrary scripts in a victim's browser, potentially stealing sensitive information, hijacking user sessions, or delivering malware. The impact of successful exploitation could be severe, leading to data breaches, financial loss, and reputational damage. 

- Exposed CMS Installation Directory: Another notable issue discovered during the assessment was the exposure of the content management system (CMS) installation directory. This exposure could potentially allow attackers to gain unauthorized access to the CMS, reconfigure its settings, or manipulate its content. Such unauthorized access could lead to the manipulation or defacement of the company's website, compromising its integrity and user trust. 

## Finding Summary
- Reflected Cross Site Scripting (XSS)
- Exposed CMS installation directory
## Attack storyline or vulnerablities with CVSS,CVE and remedation
### Reflected Cross Site Scripting (XSS) 
- CVSS Vector: CVSS:3.1/AV:N/AC:L/PR:N/UI:R/S:C/C:L/I:L/A:N

A reflected Cross-Site Scripting (XSS) vulnerability is a type of security flaw that occurs when an attacker injects malicious code, typically in the form of a script or code snippet, into a web application. This code is then reflected back to the user's browser and executed within the context of the application. The vulnerability arises when the application doesn't properly sanitize or validate user input before displaying it in the application's response.  
#### Proof of Concept (PoC) 
The following Proof of Concept (PoC) demonstrates a reflected Cross-Site Scripting (XSS) vulnerability in the application. In this case, the attacker was able to inject custom JavaScript code into the values of the parameters "m_cFailedLoginReason" and "m_cInstance." This injected code was then executed when the application processed the input and displayed it back to the user.

Here's how the attack works:

Injection: The attacker includes custom JavaScript code ("<script>alert(1)</script>") as the value for the "m_cFailedLoginReason" and "m_cInstance" parameters in the URL.

Reflection: The application takes these parameter values and incorporates them into the response. Since the application fails to properly validate or sanitize the input, it reflects the injected JavaScript code back to the user's browser as part of the rendered content.

Execution: The victim's browser interprets the injected JavaScript code and executes it. In this case, the JavaScript code triggers an alert dialog box displaying the number "1."

Impact: While the PoC example triggers a simple alert, an attacker could use this vulnerability to execute more malicious actions, such as stealing user data, session hijacking, or performing actions on behalf of the user.

#### Remediations
To remediate this vulnerability, developers should implement proper input validation and sanitization for user-provided data before rendering it in the application's responses. Encoding or escaping special characters within the input helps prevent the execution of injected scripts. Additionally, applying a strong Content Security Policy (CSP) can restrict the sources of executable code, further mitigating the risk of XSS attacks. Regular security testing and code reviews are essential to identify and fix such vulnerabilities.

### Exposed CMS installation directory
- CVSS Vector: None
In the target application, the directory of the installed Content Management System (CMS) used for employee training was inadvertently exposed. This exposure could potentially allow an attacker to re-install the CMS or modify its configuration to serve malicious purposes.
#### Proof of Concept (PoC) 
A potential Proof of Concept (PoC) could involve an attacker accessing the exposed installation directory and attempting to modify configuration files or reinstall the CMS. However, due to the sensitive nature of these actions and the potential for harm, it is recommended to refrain from demonstrating such activities in a public or unauthorized environment.
#### Remediations
To address the issue of an exposed CMS installation directory and mitigate potential risks, the following steps should be taken:

- Restrict Directory Access: Ensure that the directory containing the CMS installation is properly configured to restrict unauthorized access. Implement appropriate access controls and permissions to prevent direct browsing or listing of its contents.

- Secure Configuration Files: Ensure that sensitive configuration files within the CMS installation directory are properly protected and not accessible through the web server. These files should only be readable by the CMS application itself and not directly by users or visitors.

- Regular Updates: Keep the CMS software and any related components up to date with the latest security patches and updates. This helps to address known vulnerabilities that attackers might exploit.

- Application Firewall: Implement a Web Application Firewall (WAF) to monitor and filter incoming traffic, helping to detect and block any unauthorized attempts to access or modify the exposed CMS directory.


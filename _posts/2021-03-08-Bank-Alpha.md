---
layout: post
title: 'Bank Alpha External PT'
tags:
 - web
 - real-activity
hero: https://images.unsplash.com/photo-1501167786227-4cba60f6d58f?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1470&q=80
overlay: red
---

Please note that for this proof of concept, while images and step-by-step reproduction tips are fundamental for evidentiary purposes, they will not be supplied. Furthermore, in adherence to our commitment to privacy and compliance with non-disclosure agreements, all URLs and functionalities within this assessment have been anonymized.  {: .lead} <!--break-->

# Bank Alpha

## Type of activity and objectives
The objective of this engagement was to conduct an external penetration assessment for the bank. It was aimed at identifying vulnerabilities that could be exploited by external sources. The goal was to prevent unauthorized access and safeguard against potential compromises.
## Scope of evaluation
The evaluation was centered on the specific netblock assigned to the organization.
## Executive Summary
In the recent security assessment undertaken for Bank Alpha, two significant vulnerabilities were identified within the company's external infrastructure:

- Cross-Site Scripting (XSS) Vulnerability: A critical XSS vulnerability was identified in the application during the assessment. This vulnerability enables attackers to inject malicious scripts into web pages viewed by others. If exploited, it could allow an attacker to execute scripts in the browsers of unsuspecting victims, which might result in the theft of sensitive data, session hijacking, or malware distribution. The consequences of such exploitation are grave, potentially leading to data breaches, financial losses, and harm to the bank's reputation.

- Exposed CMS Installation Directory: The assessment also revealed the exposure of the CMS installation directory. This vulnerability might permit attackers to gain unauthorized access to the CMS, modify its settings, or alter its content. Such access poses a significant risk of website manipulation or defacement, thereby undermining the integrity of the site and eroding user trust.

In the subsequent sections of this report, detailed Proof of Concept (PoC) demonstrations and remediation steps will be provided (anonymized). These are intended to guide technicians in addressing the findings outlined earlier. Implementing these steps is crucial for enhancing the overall security posture of the organization.

## Finding Summary
- Reflected Cross Site Scripting (XSS)
- Exposed CMS installation directory
## Attack storyline and findings
### Reflected Cross Site Scripting (XSS) 
- CVSS Vector: CVSS:3.1/AV:N/AC:L/PR:N/UI:R/S:C/C:L/I:L/A:N

A reflected Cross-Site Scripting (XSS) vulnerability occurs when an attacker injects malicious code into a web application, usually as a script. The code is reflected to the user's browser and executed within the application's context. This vulnerability arises from the application's failure to adequately sanitize or validate user input before its inclusion in the response.

#### Proof of Concept (PoC) 
This PoC demonstrates a reflected XSS vulnerability. An attacker injected custom JavaScript code into the "m_cFailedLoginReason" and "m_cInstance" parameters. The application, failing to sanitize the input, executed the injected code upon processing.

Attack Process:

1. Injection: Custom JavaScript code (<script>alert(1)</script>) was inserted as values for "m_cFailedLoginReason" and "m_cInstance" in the URL.
2. Reflection: The application incorporated these values into its response, reflecting the injected code.
3. Execution: The code executed in the victim's browser, exemplified by an alert dialog with the number "1".

Impact: This example illustrates a basic alert; however, the vulnerability could enable more harmful actions, like data theft or session hijacking.

#### Remediations
To remediate this vulnerability, developers should implement proper input validation and sanitization for user-provided data before rendering it in the application's responses. Encoding or escaping special characters within the input helps prevent the execution of injected scripts. Additionally, applying a strong Content Security Policy (CSP) can restrict the sources of executable code, further mitigating the risk of XSS attacks. Regular security testing and code reviews are essential to identify and fix such vulnerabilities.

### Exposed CMS installation directory
- CVSS Vector: None
In the target application, the directory of the installed Content Management System (CMS) used for employee training was inadvertently exposed. This exposure could potentially allow an attacker to re-install the CMS or modify its configuration to serve malicious purposes.
#### Proof of Concept (PoC) 
A hypothetical PoC could involve accessing the exposed directory to alter configurations or reinstall the CMS. However, due to the potential harm, such activities should not be executed in an unauthorized setting.
#### Remediations
To address the issue of an exposed CMS installation directory and mitigate potential risks, the following steps should be taken:

- Restrict Directory Access: Ensure that the directory containing the CMS installation is properly configured to restrict unauthorized access. Implement appropriate access controls and permissions to prevent direct browsing or listing of its contents.

- Secure Configuration Files: Ensure that sensitive configuration files within the CMS installation directory are properly protected and not accessible through the web server. These files should only be readable by the CMS application itself and not directly by users or visitors.

- Regular Updates: Keep the CMS software and any related components up to date with the latest security patches and updates. This helps to address known vulnerabilities that attackers might exploit.

- Application Firewall: Implement a Web Application Firewall (WAF) to monitor and filter incoming traffic, helping to detect and block any unauthorized attempts to access or modify the exposed CMS directory.


---
layout: post
title: 'Corporate Alpha External PT'
tags:
 - web
 - real-engagement
hero: https://images.unsplash.com/photo-1462206092226-f46025ffe607?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1474&q=80
overlay: blue
---

No images (image for the step by step PoC are essential as evidence but will not be provided
) or references will be provided, as this assessment was a real engagement. Additionally, all URLs and functionalities have been anonymized to ensure privacy and compliance with non-disclosure agreements (NDAs). {: .lead} <!--break-->

# Corporate Alpha

## Type of activity and objectives
The objective of this engagement was to conduct an external penetration assessment for the Corporate. The aim was to identify potential vulnerabilities that could potentially be exploited from outside sources, with the goal of preventing unauthorized access and compromise.
## Scope of evaluation
The evaluation was focused on the specific netblock assigned to the organization. This scope encompassed assessing the security and potential vulnerabilities within this network range.
## Executive Summary
During the  web penetration testing conducted on Corporate Alpha, our offensive team identified critical vulnerabilities that pose potential risks to the security and integrity of the external surface. 
The two primary vulnerabilities discovered are Cross-Site Scripting (XSS) and SQL Injection (SQLi), both of which expose the application to potential exploitation by malicious actors.
The impact of successful exploitation could range from user data exposure to compromising user trust and brand reputation.

## Finding Summary
- Cross Site Scripting (XSS)
- Time Based SQL Injection (SQLi)
## Attack storyline or vulnerabilities with CVSS,CVE and remedations
### Reflected Cross Site Scripting (XSS) 
- CVSS Vector: CVSS:3.1/AV:N/AC:L/PR:N/UI:R/S:C/C:L/I:L/A:N

A reflected Cross-Site Scripting (XSS) vulnerability is a type of security flaw that occurs when an attacker injects malicious code, typically in the form of a script or code snippet, into a web application. This code is then reflected back to the user's browser and executed within the context of the application. The vulnerability arises when the application doesn't properly sanitize or validate user input before displaying it in the application's response.  
#### Proof of Concept (PoC) 
A proof of concept (PoC) has been created to demonstrate the presence of a reflected Cross-Site Scripting (XSS) vulnerability within the application. This vulnerability is found in the "where" parameter of the URL. The following payload has been injected into the parameter to trigger a JavaScript-based alert when the page is loaded:

`/index.cfm?where=aw0e2"><img src=a onerror=alert("xss")>uybfa`

By injecting this payload, an attacker can exploit the XSS vulnerability and execute arbitrary JavaScript code within the context of a victim's browser. This could potentially lead to various malicious actions, such as stealing sensitive information, hijacking user sessions, or delivering malware.

#### Remediations
To remediate this vulnerability, developers should implement proper input validation and sanitization for user-provided data before rendering it in the application's responses. Encoding or escaping special characters within the input helps prevent the execution of injected scripts. Additionally, applying a strong Content Security Policy (CSP) can restrict the sources of executable code, further mitigating the risk of XSS attacks. Regular security testing and code reviews are essential to identify and fix such vulnerabilities.

### Time Based SQL Injection (SQLi)
- CVSS Vector: CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:U/C:L/I:N/A:N

A time-based SQL injection is a type of security vulnerability that occurs when a web application's input is not properly sanitized or validated before being used in a SQL query to a database. This vulnerability allows attackers to manipulate the application's behavior and gain unauthorized access to the database's contents by injecting malicious SQL code.

The exploitation of a time-based SQL injection takes advantage of the fact that different SQL database management systems (DBMS) might handle delays in executing queries differently.
#### Proof of Concept (PoC) 

The following Proof of Concept (PoC) shows a time-based SQL injection vulnerability in the context of a parameter called `idmedia` within the `Views/viewDoc.cfm` endpoint. The payload provided is designed to induce a delay in the SQL query execution and demonstrates the presence of the vulnerability.

In this PoC, the payload `%2b(select*from(select(sleep(5)))a)%2b` is appended to the URL parameter `idmedia`, aiming to execute a SQL query that causes a delay of 5 seconds using the `SLEEP()` function. If the application is vulnerable to time-based SQL injection, the server's response time will noticeably increase, indicating that the payload successfully caused a delay in the query execution.

The exploited Confusion application was running with root privileges, running an application with root privileges means that it has the highest level of access and control over the system, potentially leading to severe consequences.

#### Remediations
To secure the application against such vulnerabilities, it's crucial to implement proper input validation and use parameterized queries or prepared statements. These measures prevent attackers from injecting malicious SQL code into the application and help safeguard the integrity and security of your data. Regular security assessments and testing are also important to identify and address vulnerabilities like these before they can be exploited by malicious actors.
Root-level access allows an application to perform actions that can compromise the entire system, including modifying system files, installing malicious software, accessing sensitive data, and more. If an attacker gains control of an application running with root privileges, they can escalate their access to control the entire system.

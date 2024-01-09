---
layout: post
title: 'Corporate Alpha External PT'
tags:
 - web
 - real-activity
hero: https://images.unsplash.com/photo-1577962917302-cd874c4e31d2?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1632&q=80
overlay: red
---

Please note that for this proof of concept, while images and step-by-step reproduction tips are fundamental for evidentiary purposes, they will not be supplied. Furthermore, in adherence to our commitment to privacy and compliance with non-disclosure agreements, all URLs and functionalities within this assessment have been anonymized. {: .lead} <!–-break-–>
# Corporate Alpha

## Type of activity and objectives
The objective of this engagement was to conduct an external penetration assessment for the corporation. The aim was to identify potential vulnerabilities that could potentially be exploited from outside sources, intending to prevent unauthorized access and compromise.
## Scope of evaluation
The evaluation was focused on the specific net block assigned to the organization. This scope encompassed assessing the security and potential vulnerabilities within this network range.
## Executive Summary
## Finding Summary
- Cross-Site Scripting (XSS)
- Time-Based SQL Injection (SQLi)
- Leaked SMTP Credentials in source code
- HTML Injection
## Risk Impact Graph with CVSS Scores

![](https://raw.githubusercontent.com/blitz0p3rations/blitz0p3rations.github.io/master/uploads/id17.png)

## Vulnerability Types Distribution

![](https://raw.githubusercontent.com/blitz0p3rations/blitz0p3rations.github.io/master/uploads/id18.png)

## Attack storyline and findings
### Reflected Cross Site Scripting (XSS) 
- CVSS Vector: CVSS:3.1/AV:N/AC:L/PR:N/UI:R/S:C/C:L/I:L/A:N
#### Proof of Concept (PoC) 
A reflected Cross-Site Scripting (XSS) vulnerability is a type of security flaw that occurs when an attacker injects malicious code, typically in the form of a script or code snippet, into a web application. This code is then reflected back to the user's browser and executed within the context of the application. The vulnerability arises when the application doesn't properly sanitize or validate user input before displaying it in the application's response.  
The provided Proof of Concept (PoC) demonstrates the presence of a reflected Cross-Site Scripting (XSS) vulnerability within the application. The vulnerability allows an attacker to inject malicious scripts into the application, which are then executed in the context of the victim's browser when the vulnerable page is loaded. This can lead to unauthorized access, data theft, or other malicious actions.

In the PoC, the injected payload consists of JavaScript code that triggers an alert dialog with the message "1" when the page loads. The payload is injected into different parts of the application's parameters, including the "return" parameter of the URL and the body of a POST request.

Here is the breakdown of the PoC:

1. **return Parameter:**
   The payload injected into the "return" parameter:
   `Applicationcrh3y</script><script>alert(1)</script>lve4ge6x57u`
   This payload aims to execute the JavaScript code `alert(1)` when the page loads. 
   It takes advantage of the vulnerability to inject malicious scripts into the 
   parameter.

2. **object Parameter:**
   The payload injected into the "object" parameter:
   `<img src=a onerror=alert(1)> `
   This payload injects an image tag with an `onerror` attribute containing the 
   JavaScript code `alert(1)`. This code is triggered if the image fails to load.

3. **forms Parameter:**
   The payload injected into the "forms" parameter of a POST request:
   *{"loginForm":{"loadTarget":"hkgps<img src=a onerror=alert(1)>g7w17","stusername":"cv","sppassword":"vc","ntuseraction":"login"}}*
   Similar to the "object" parameter, this payload injects an image tag with an `onerror` attribute containing the JavaScript code `alert(1)`.

The provided PoC demonstrates how an attacker can exploit the XSS vulnerability to execute arbitrary JavaScript code within the context of the application's pages. This could lead to various security risks, including stealing user credentials, session hijacking, defacement, or spreading malware.

#### Remediations
To remediate this vulnerability, developers should implement proper input validation and sanitization for user-provided data before rendering it in the application's responses. Encoding or escaping special characters within the input helps prevent the execution of injected scripts. Additionally, applying a strong Content Security Policy (CSP) can restrict the sources of executable code, further mitigating the risk of XSS attacks. Regular security testing and code reviews are essential to identify and fix such vulnerabilities.

### Time Based SQL Injection (SQLi)
- CVSS Vector: CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:U/C:L/I:N/A:N

A time-based SQL injection is a type of security vulnerability that occurs when a web application's input is not properly sanitized or validated before being used in a SQL query to a database. This vulnerability allows attackers to manipulate the application's behavior and gain unauthorized access to the database's contents by injecting malicious SQL code.

The exploitation of a time-based SQL injection takes advantage of the fact that different SQL database management systems (DBMS) might handle delays in executing queries differently.
#### Proof of Concept (PoC) 
The presented Proof of Concept (PoC) highlights the discovery of a time-based SQL injection vulnerability within the targeted application. This vulnerability enables an attacker to manipulate a specific parameter and cookies, resulting in delays in the application's responses. This delay indicates the possible existence of the vulnerability and may allow unauthorized access to sensitive database information.

The following Proof of Concept (PoC) shows a time-based SQL injection vulnerability in the context of following cookies: **/application/watch_video.php**
-  vid_name
-  company
-  email
-  name
-  message

In the PoC scenario, the parameter action within the endpoint **/components/ajaxengine.cfc** of the application was found to be susceptible to SQL injection. The provided value for the email parameter is **collab'&action=forgotPsw**. This input attempts to inject a payload that can potentially manipulate the SQL query and achieve unintended results.

In both scenarios involving two distinct applications, a critical security vulnerability was exploited that led to unauthorized access with full read capabilities to the internal database. Although the security assessment team identified this vulnerability, they did not proceed with attempting to write or modify the database, as this action was not authorized by the customer.
#### Remediations
To secure the application against such vulnerabilities, it's crucial to implement proper input validation and use parameterized queries or prepared statements. These measures prevent attackers from injecting malicious SQL code into the application and help safeguard the integrity and security of your data. Regular security assessments and testing are also important to identify and address vulnerabilities like these before they can be exploited by malicious actors.
Root-level access allows an application to perform actions that can compromise the entire system, including modifying system files, installing malicious software, accessing sensitive data, and more. If an attacker gains control of an application running with root privileges, they can escalate their access to control the entire system.

### HTML Injection
- CVSS Vector: CVSS:3.1/AV:N/AC:L/PR:N/UI:R/S:U/C:N/I:L/A:N
HTML Injection is a type of web security vulnerability that occurs when an attacker is able to inject malicious code, usually in the form of HTML, into a web application.
#### Proof of Concept (PoC) 
The provided Proof of Concept (PoC) demonstrates an HTML Injection vulnerability within the "where" parameter of the application. By submitting the payload `""><a href=https://google.com></a>`, an attacker was able to trigger the HTML Injection vulnerability. This payload consists of HTML code that includes an anchor element (`<a>`) with an `href` attribute pointing to the URL "https://google.com".

When this payload is processed by the vulnerable application and the affected page is rendered, the injected HTML code will be executed within the context of the victim's browser. As a result, the browser will create a hyperlink to "https://google.com", potentially leading users to a malicious website or unintended content.
#### Remediations
Preventing HTML Injection:

- Input Validation and Sanitization: Web applications should validate and sanitize user inputs before displaying them on web pages.

- Context-Aware Escaping: Properly escape user inputs depending on where they are displayed (HTML, JavaScript, URL, etc.).
### Leaked SMTP Credentials
- CVSS Vector: None

Leaked SMTP credentials in the source code of a web application can have serious security and operational implications for both the application and the organization that owns it. SMTP (Simple Mail Transfer Protocol) is used for sending email messages, and if the credentials used to authenticate with an SMTP server are exposed, it can lead to several negative consequences:
- Email Abuse and Spoofing
- Phishing Attacks
- Reputation Damage
- Blacklisting
- Operational Disruption
- Financial Impact
#### Proof of Concept (PoC) 
The presence of leaked credentials within the source code of the target application represents a significant security concern. While the team did not proceed to exploit these credentials due to their origin from a third-party company that developed the web application, it is essential to recognize the potential risk and the implications it could have on the in-scope organization's security posture.

Leaked credentials, even from external parties, can lead to various detrimental outcomes.

While the leaked credentials were not exploited, their discovery highlights the need for diligence in managing third-party relationships and ensuring that proper security measures are in place to safeguard sensitive information and maintain the organization's overall security posture.
#### Remediations
To mitigate the impact of leaked SMTP credentials, organizations should:

- Regularly audit and review their source code for any exposed credentials.
- Follow secure coding practices to ensure that sensitive credentials are not hard-coded in source code.
- Use environment variables or secure configuration management tools to store and manage credentials.
- Implement strong access controls and authentication mechanisms to prevent unauthorized access to systems and servers.
- Educate developers and staff about the risks of exposing credentials and train them in secure coding practices.

Swift action should be taken to address any identified vulnerabilities and prevent potential exploitation of leaked credentials.

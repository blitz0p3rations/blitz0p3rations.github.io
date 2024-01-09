---
layout: post
title: 'Freeze Company External PT'
tags:
 - web
 - real-activity
hero: https://images.unsplash.com/photo-1577962917302-cd874c4e31d2?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1632&q=80
overlay: blue
---

Please note that for this proof of concept, while images and step-by-step reproduction tips are fundamental for evidentiary purposes, they will not be supplied. Furthermore, in adherence to our commitment to privacy and compliance with non-disclosure agreements, all URLs and functionalities within this assessment have been anonymized. {: .lead} <!–-break-–>

# Freeze Company

## Type of activity and objectives
The objective of this engagement was to conduct an external penetration assessment for the organization. The aim was to identify potential vulnerabilities that might be exploited by external sources, with the ultimate goal of preventing unauthorized access and compromise.
## Scope of evaluation
The evaluation was focused on the external surface of the organization. This scope encompassed assessing the security and potential vulnerabilities within this external surface.
## Executive Summary
The assessment conducted on the external surface unveiled two significant findings, posing critical security risks to the organization. 

The first finding pertains to a SQL injection (SQLi) vulnerability that, when exploited, could potentially lead to remote code execution (RCE). This zero-day vulnerability emphasizes the immediate need for remediation to prevent unauthorized access and potential compromise of the application.

The second finding involves the exposure of the .git directory, which contains sensitive information, including Short Message Service (SMS) API secrets. This exposure increases the organization's vulnerability to potential data breaches and unauthorized access, posing a considerable threat to the confidentiality and integrity of the application and its associated systems.

To address these vulnerabilities, swift actions are essential. The organization should prioritize the immediate patching or mitigation of the SQL injection vulnerability to prevent potential RCE and unauthorized access. Additionally, the exposure of the .git directory should be mitigated by implementing proper access controls and restricting public access to sensitive information.
## Finding Summary
- SQLi to RCE (0day)
- Exposed .git with SMS API secrets
## Risk Impact Graph with CVSS Scores

![](https://raw.githubusercontent.com/blitz0p3rations/blitz0p3rations.github.io/master/uploads/id19.png)

## Vulnerability Types Distribution

![](https://raw.githubusercontent.com/blitz0p3rations/blitz0p3rations.github.io/master/uploads/id20.png)

## Attack storyline and findings### SQLi to RCE (0day)
- CVSS Vector: CVSS:3.0/AV:N/AC:L/PR:N/UI:N/S:C/C:H/I:H/A:H
#### Proof of Concept (PoC) 
The vulnerability allowed an attacker to execute SQL injection attacks through the login form. This posed a severe risk to the confidentiality and integrity of the application's data.

The payload is the following:
- **e: fUsername=sd'||(SELECT 0x6746556a FROM DUAL WHERE 6376=6376 AND (SELECT 1971 FROM(SELECT COUNT(*),CONCAT(0x71706b6b71,(SELECT (ELT(1971=1971,1))),0x71707a7171,FLOOR(RAND(0)*2))x FROM INFORMATION_SCHEMA.PLUGINS GROUP BY x)a))||'&fPassword=sd&submit=Entra**

By exploiting the SQL injection vulnerability with a crafted payload, the team confirmed unauthorized access to the database's contents. Moreover, during further analysis, a writable location was discovered by reading the **/etc/httpd/conf/httpd.conf** file using the permissions of an admin username that had been previously dumped.

So we discovered that this location is writable /var/www/html/mailredeacted/* .


This critical discovery provided the attacker with the ability to upload malicious content, leading to remote code execution (RCE) on the application's web server. A webshell (https://github.com/epinna/weevely3) was successfully uploaded, allowing the attacker to execute arbitrary commands with the privileges of the web server, potentially compromising the entire application and server environment.

The application has been used for conducting mail exchanges for over a decade.

#### Remediations
- Update the mail solution
- Restrict access to mitigate
### Exposed .git with SMS API secrets
- CVSS Vector: CVSS:3.0/AV:N/AC:H/PR:N/UI:N/S:C/C:H/I:N/A:H
#### Proof of Concept (PoC) 
During the assessment of the target web application, a .git folder was discovered containing the application's source code and hardcoded secrets for the SMS API service. This presents a significant security concern as unauthorized access to these secrets could potentially lead to misuse of the service, enabling malicious actors to conduct phishing campaigns and impersonation attacks. The path to the exposed .git configuration file is as follows: "documents.target.com/.git/config". Immediate action must be taken to secure these secrets and prevent unauthorized access to sensitive information.
#### Remediations
- Adjust permission on that specific folder
- Restrict access to mitigate

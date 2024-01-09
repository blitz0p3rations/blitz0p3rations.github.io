---
layout: post
title: 'Building Company External PT'
tags:
 - web
 - real-activity
hero: 
overlay: red
---

Please note that for this proof of concept, while images and step-by-step reproduction tips are fundamental for evidentiary purposes, they will not be supplied. Furthermore, in adherence to our commitment to privacy and compliance with non-disclosure agreements, all URLs and functionalities within this assessment have been anonymized. {: .lead} <!–-break-–>
# Building Company

## Type of activity and objectives
The objective of this engagement was to conduct an external penetration assessment for the organization. The aim was to identify potential vulnerabilities that could potentially be exploited from outside sources, with the goal of preventing unauthorized access and compromise.
## Scope of evaluation
The evaluation was focused on the specific netblock assigned to the organization. This scope encompassed assessing the security and potential vulnerabilities within this network range.
## Executive Summary
The assessment of the external infrastructure uncovered two significant findings: the CVE-2009-2265 vulnerability and User Enumeration vulnerabilities. The CVE-2009-2265 vulnerability represents a critical security risk due to the system's susceptibility to arbitrary code execution. If exploited, this vulnerability could allow unauthorized access and manipulation of sensitive data by malicious actors.

Furthermore, the User Enumeration vulnerability enables attackers to identify valid usernames within the system. Although this might appear benign, such information can be leveraged in more complex attacks, including brute-force password guessing efforts. This vulnerability underscores the importance of robust security measures to prevent unauthorized access and safeguard sensitive data.
## Finding Summary
- CVE-2009-2265
- User Enumeration
## Risk Impact Graph with CVSS Scores

![](https://raw.githubusercontent.com/blitz0p3rations/blitz0p3rations.github.io/master/uploads/bu1.png)

## Vulnerability Types Distribution

![](https://raw.githubusercontent.com/blitz0p3rations/blitz0p3rations.github.io/master/uploads/bu2.png)

## Attack storyline and findings
### CVE-2009-2265 
- CVSS Vector: CVSS:2.0/AV:N/AC:L/Au:N/C:P/I:N/A:N
#### Proof of Concept (PoC) 
This exploit permits unauthenticated users to upload files, thereby enabling remote code execution on the target host. The vulnerability is found within FCKeditor, where the file upload path is not adequately restricted.

Utilizing a modified version of the exploit found at https://github.com/0xConstant/CVE-2009-2265, remote code execution (RCE) was achieved on the target system. Notably, the service was running under the 'root' user, providing extensive system access. To test the response time of the Security Operations Center (SOC), a standard binary of Mimikatz was uploaded.
#### Remediations
- Update ColdFusion: Ensure that your ColdFusion installation is updated to a version that includes the fix for CVE-2009-2265. Adobe, the company behind ColdFusion, has released patches and security updates to address this vulnerability. Apply the latest available patches or updates to your ColdFusion server.
- Implement Web Application Firewall (WAF): Consider implementing a WAF that can help detect and block malicious requests attempting to exploit vulnerabilities like CVE-2009-2265. A WAF can provide an additional layer of protection for your web applications.
### User Enumeration
- CVSS Vector: CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:U/C:L/I:N/A:N
#### Proof of Concept (PoC) 
During the assessment of the HR web application, it was discovered that the application exposed a list of all users within the target organization. The information was accessible without requiring any form of authentication or proper authorization.

To verify the presence of this vulnerability, the following URL paths were tested:

- **/users**
- **/employees**
- **/directory**
- **/staff**
Each of these URLs returned a list of users, potentially including sensitive information such as names, email addresses, and other employee details. This exposure of user information could have serious privacy implications and could potentially be exploited by attackers for various malicious purposes.
#### Remediations
- Add a layer of authentication.


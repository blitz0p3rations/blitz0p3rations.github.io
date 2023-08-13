---
layout: post
title: 'Multimaster HTB'
tags:
  - ctf
  - network
hero: https://images.unsplash.com/photo-1495149905644-c9f27692c2c3?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1475&q=80
overlay: blue
---

The following report presents a comprehensive walkthrough and analysis of a recently completed Hack The Box (HTB) challenge. This writeup aims to provide insight into the methodologies, techniques, and thought processes employed to successfully tackle the challenge. {: .lead} <!–-break-–> 

# Multimaster HTB

## Type of activity and objectivies
The objective of this activity is to conduct a penetration test on the target system, utilizing a machine within the same network. This test aims to assess the security posture of the target, identify vulnerabilities, and potentially exploit them to simulate real-world attack scenarios. 
By performing this penetration test from within the same network, we can assess the effectiveness of the network segmentation and security controls while identifying potential risks that an insider threat might exploit. 
The results of this test will provide valuable insights into the overall security of the target system and guide the implementation of necessary remediation measures to enhance its defenses.
## Scope of evalutaion
The scope of evaluation for this assessment encompasses the target network and specific IP address. During this evaluation, we will focus on assessing the security of the designated network and the identified IP address. Our analysis will include identifying potential vulnerabilities, weaknesses, and areas of concern within the given network and IP range. Through thorough testing and analysis, we aim to provide valuable insights into the security posture of the target network and IP, highlighting any potential risks that may need to be addressed.
## Executive Summary
The security assessment conducted on the target network revealed several critical vulnerabilities, each presenting unique risks and potential impact. These vulnerabilities were mapped to the MITRE ATT&CK framework, providing a structured perspective on their relevance and potential implications.

- **SQL Injection (SQLi)**:
  The discovery of SQL injection vulnerabilities exposes a weakness in the application's input validation. Exploiting SQLi could allow an attacker to manipulate database queries, potentially leading to unauthorized data access or data manipulation.
  - Tactic: Initial Access (TA0001)
  - Technique: Exploit Public-Facing Application (T1190)

- **Password Spraying (PSW Spraying)**:
  The attempt to use commonly used passwords across multiple accounts highlights a weakness in user password management. This technique could lead to unauthorized access to accounts and data.
  - Tactic: Credential Access (TA0006)
  - Technique: Password Spraying (T1110)

- **CVE-2020-1472 (ZeroLogon)**:
  Exploiting the CVE-2020-1472 vulnerability indicates that attackers can target Microsoft Windows Active Directory to compromise domain controllers and potentially gain control over the entire domain. This could lead to widespread unauthorized access and control.
  - Tactic: Defense Evasion (TA0005)
  - Technique: Exploitation of Remote Services (T1210)

Each of these vulnerabilities represents a distinct avenue of attack, potentially resulting in unauthorized access, data exposure, or system compromise. It's crucial to address these vulnerabilities promptly to mitigate their impact and bolster the overall security posture of the organization.

## Finding summary
- SQLi
- PSW Spraying
- CVE-2020-1472
## Attack storyline or vulnerabilties with MITRE mapping,CVE and with remediations

T1590 - Conduct Active Scanning: The attacker initiates the reconnaissance phase by actively scanning the target network for open ports and services.
T1046 - Network Service Scanning: The attacker employs network service scanning to identify open ports and services on the target systems.

Through the port scanning results and other common enumerations techniques, the attacker identifies exposed services within the target network.

![](https://raw.githubusercontent.com/blitz0p3rations/blitz0p3rations.github.io/master/uploads/mul1.png)

### SQLi
SQL Injection (SQLi) is a type of cybersecurity vulnerability that occurs when an attacker is able to manipulate an application's input fields to execute arbitrary SQL (Structured Query Language) commands in a database. SQLi vulnerabilities occur primarily in web applications that use user inputs to construct database queries without proper validation or sanitization.
### PoC
It was possible to identify a SQL Injection (SQLi) vulnerability within the target application. By exploiting this vulnerability, the team was able to extract sensitive information, including user credentials and corresponding hashes, from the application's database.

The following Python exploit was used for the exploitation part:

![](https://raw.githubusercontent.com/blitz0p3rations/blitz0p3rations.github.io/master/uploads/mul2.png)

### Remediations
- Input Validation and Sanitization:Validate and sanitize user inputs before using them in SQL queries. Implement strict input validation by allowing only expected characters and formats.

- Use Prepared Statements or Parameterized Queries: Utilize prepared statements or parameterized queries provided by your programming language or framework. Parameterized queries separate user inputs from SQL commands, preventing direct injection.

- Stored Procedures: Use stored procedures as they can provide a layer of abstraction between user inputs and SQL commands. This can limit the exposure of SQL code to user inputs.

### PSW Spraying
T1201 - Password Policy Discovery: The attacker's actions involve probing the password policy to exploit vulnerabilities.


### PoC
To identify weak password usage among the list of usernames, we employed the tool CrackMapExec. This allowed us to try a limitied sets of passwords with all user accounts. By utilizing the --continue-on-success flag, we ensured that CrackMapExec would assess the complete list of usernames, even if a valid account was discovered. This approach helps uncover instances of poor password practices that could potentially lead to unauthorized access.

![](https://raw.githubusercontent.com/blitz0p3rations/blitz0p3rations.github.io/master/uploads/mul3.png)

### Remediations
- Account Lockout: Enforce account lockout policies to limit the number of unsuccessful login attempts for an account. This prevents attackers from continuously guessing passwords.

- Multi-Factor Authentication (MFA): Implement MFA to add an additional layer of security. Even if an attacker guesses a password, they would still need a second factor to gain access.

- Complex Password Policies: Enforce strong password policies that require a combination of uppercase, lowercase, numbers, and special characters. Discourage the use of easily guessable passwords.

- Rate Limiting: Implement rate limiting on authentication attempts to prevent rapid and repeated login attempts from the same source.

### CVE-2020-1472
- CVSS Vector: CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:C/C:H/I:H/A:H

An elevation of privilege vulnerability exists when an attacker establishes a vulnerable Netlogon secure channel connection to a domain controller, using the Netlogon Remote Protocol (MS-NRPC), aka 'Netlogon Elevation of Privilege Vulnerability'.
### PoC
The PoC demonstrates the exploitation of the CVE-2020-1472 vulnerability (Zerologon) to elevate privileges and perform a pass-the-hash attack to gain domain admin access. The following steps outline the attack process:

1. **Exploiting Zerologon (CVE-2020-1472)**:
   - Exploiting the Zerologon vulnerability allows an attacker to establish a Netlogon secure channel with a domain controller without proper authentication.
   - The attacker can execute the Netlogon authentication request without providing a valid password, effectively bypassing the authentication process.

2. **Elevating Privileges**:
   - After successfully exploiting Zerologon, the attacker gains access to the domain controller with a computer account.
   - The attacker can then impersonate the computer account and escalate privileges to a domain administrator.

3. **Dumping Hashes**:
   - Using the impacket-secretsdump tool, the attacker extracts the NTLM hash of domain user accounts from the domain controller's database.
   - This hash can be used for pass-the-hash attacks, allowing the attacker to authenticate as domain users without knowing their actual passwords.

4. **Pass-the-Hash Attack**:
   - The attacker uses the extracted NTLM hash to authenticate as a domain user, bypassing the need for the actual password.
   - With the privileges of the compromised user, the attacker moves laterally within the network, potentially accessing sensitive resources and systems.

5. **Gaining Domain Admin Access**:
   - By targeting a user with domain admin privileges, the attacker can authenticate with their hash.
   - The attacker now has access to the domain admin rights and can perform administrative tasks, access critical systems, and potentially take control of the entire domain.

The following exploit was used: https://github.com/dirkjanm/CVE-2020-1472/tree/master .

![](https://raw.githubusercontent.com/blitz0p3rations/blitz0p3rations.github.io/master/uploads/mul4.png)
![](https://raw.githubusercontent.com/blitz0p3rations/blitz0p3rations.github.io/master/uploads/mul5.png)

![](https://raw.githubusercontent.com/blitz0p3rations/blitz0p3rations.github.io/master/uploads/mul6.png)

### Remediations
- Patch Systems: Apply the security updates provided by Microsoft to all affected systems, especially the domain controllers. This is the most crucial step to address the vulnerability.

- Enforce Secure RPC: After applying the patch, enforce secure RPC communication to prevent unauthenticated attackers from exploiting the vulnerability.

- Enable Enforcement Mode: Windows Server 2012 and later versions provide an enforcement mode for Netlogon secure channel connections. Enabling enforcement mode can help protect against unauthenticated connections.
---
layout: post
title: 'Mantis HTB'
tags:
  - ctf
  - network
hero: https://images.unsplash.com/photo-1495149905644-c9f27692c2c3?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1475&q=80
overlay: blue
---

The following report presents a comprehensive walkthrough and analysis of a recently completed Hack The Box (HTB) challenge. This write-up aims to provide insight into the methodologies, techniques, and thought processes employed to successfully tackle the challenge. {: .lead} <!–-break-–> 

# Mantis HTB

## Type of activity and objectives
The objective of this activity is to conduct a penetration test on the target system, utilizing a machine within the same network. This test aims to assess the security posture of the target, identify vulnerabilities, and potentially exploit them to simulate real-world attack scenarios. 
By performing this penetration test from within the same network, we can assess the effectiveness of the network segmentation and security controls while identifying potential risks that an insider threat might exploit. 
The results of this test will provide valuable insights into the overall security of the target system and guide the implementation of necessary remediation measures to enhance its defences.
## Scope of evalutaion
The scope of evaluation for this assessment encompasses the target network and specific IP address. During this evaluation, we will focus on assessing the security of the designated network and the identified IP address. Our analysis will include identifying potential vulnerabilities, weaknesses, and areas of concern within the given network and IP range. Through thorough testing and analysis, we aim to provide valuable insights into the security posture of the target network and IP, highlighting any potential risks that may need to be addressed.
## Executive Summary
During the assessment, several notable security vulnerabilities were identified and exploited, aligning with various MITRE ATT&CK techniques.

- Password Spraying (T1110): By employing password spraying techniques, attackers attempted to gain unauthorized access by systematically testing a set of common passwords against multiple user accounts. Despite these efforts, the attack was unsuccessful due to robust password policies in place.

- Credentials Disclosure via Share Folders (T1083): The assessment revealed that sensitive credentials were unintentionally exposed through improperly secured network shares. This scenario demonstrates the importance of proper access controls and the potential impact of credential exposure on an organization's security posture.

- Azure AD Connect Password Extraction (T1003): A vulnerability in Azure AD Connect was exploited, allowing the extraction of password information. This technique highlights the significance of secure configuration management and maintaining up-to-date security patches.

## Finding summary
- PSW Spraying
- Credentials disclosure in a shared folder
- Azure AD Connect password extraction
## Attack storyline or vulnerabilities with MITRE mapping, CVE and remediations

T1590 - Conduct Active Scanning: The attacker initiates the reconnaissance phase by actively scanning the target network for open ports and services.
T1046 - Network Service Scanning: The attacker employs network service scanning to identify open ports and services on the target systems.

Through the port scanning results and other common enumeration techniques, the attacker identifies exposed services within the target network.

![](https://raw.githubusercontent.com/blitz0p3rations/blitz0p3rations.github.io/master/uploads/mont1.png)

### PSW Spraying
T1201 - Password Policy Discovery: The attacker's actions involve probing the password policy to exploit vulnerabilities.


### PoC
To identify weak password usage among the list of usernames, we employed the tool CrackMapExec. This allowed us to determine if any of the user accounts were using their username as their password. By utilizing the --continue-on-success flag, we ensured that CrackMapExec would assess the complete list of usernames, even if a valid account was discovered. This approach helps uncover instances of poor password practices that could potentially lead to unauthorized access.

![](https://raw.githubusercontent.com/blitz0p3rations/blitz0p3rations.github.io/master/uploads/mont2.png)

![](https://raw.githubusercontent.com/blitz0p3rations/blitz0p3rations.github.io/master/uploads/mont3.png)

### Remediations
- Account Lockout: Enforce account lockout policies to limit the number of unsuccessful login attempts for an account. This prevents attackers from continuously guessing passwords.

- Multi-Factor Authentication (MFA): Implement MFA to add a layer of security. Even if an attacker guesses a password, they would still need a second factor to gain access.

- Complex Password Policies: Enforce strong password policies that require a combination of uppercase, lowercase, numbers, and special characters. Discourage the use of easily guessable passwords.

- Rate Limiting: Implement rate limiting on authentication attempts to prevent rapid and repeated login attempts from the same source.

### Credentials disclosure in shared folder
This finding aligns with the MITRE ATT&CK technique "Credential Dumping" (T1003), where adversaries obtain account login and password information. It is crucial to secure shared resources to prevent unauthorized access and credential exposure.
### PoC
Following the compromise of the previously compromised account, we explored the contents of a shared folder that was accessible to the compromised account. Through this access, we were able to identify credentials associated with Azure services. This information leakage illustrates a potential security weakness, as sensitive credentials were exposed within a shared environment.

![](https://raw.githubusercontent.com/blitz0p3rations/blitz0p3rations.github.io/master/uploads/mont4.png)

![](https://raw.githubusercontent.com/blitz0p3rations/blitz0p3rations.github.io/master/uploads/mont5.png)

### Remediations
- Never expose secrets in shared folders.

### Azure AD Connect password extraction
- Tactic: Credential Access (TA0006):
  - Technique: Credential Dumping (T1003): Using scripts to decrypt and retrieve stored credentials could be seen as a form of credential dumping.
- Tactic: Defense Evasion (TA0005):
    Technique: Obfuscated Files or Information (T1027): If the script is obfuscated to evade detection, it may be relevant to this technique.
- Tactic: Execution (TA0002):
    Technique: PowerShell (T1086): The use of PowerShell to execute the decryption script may align with this technique.
### PoC
In the following, it can be noticed that the forest-login-user is an administrator. 
It means that it could be possible to recover the password of the administrator account.
The script for the PoC is the following: https://gist.githubusercontent.com/xpn/0dc393e944d8733e3c63023968583545/raw/d45633c954ee3d40be1bff82648750f516cd3b80/azuread_decrypt_msol.ps1.

![](https://raw.githubusercontent.com/blitz0p3rations/blitz0p3rations.github.io/master/uploads/mont6.png)

![](https://raw.githubusercontent.com/blitz0p3rations/blitz0p3rations.github.io/master/uploads/mont7.png)

### Remediations
- Use Managed Service Accounts: Instead of using regular user accounts, consider using Managed Service Accounts (MSAs) or Group Managed Service Accounts (gMSAs) for services that require credentials.

- Least Privilege Principle: Limit the permissions of accounts used for synchronization. Only grant the necessary permissions required for the synchronization process.

- Secure Credential Storage: Ensure that account credentials are stored securely. Avoid hardcoding credentials in scripts or configuration files.

---
layout: post
title: 'Power Plant Internal PT'
tags:
  - internal-network
  - real-activity
hero: https://images.unsplash.com/photo-1541955193702-9ca03b1bb11a?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1470&q=80
overlay: red
---

Please note that for this proof of concept, while images and step-by-step reproduction tips are fundamental for evidentiary purposes, they will not be supplied. Furthermore, in adherence to our commitment to privacy and compliance with non-disclosure agreements, all URLs and functionalities within this assessment have been anonymized. {: .lead} <!–-break-–>

# Power Plant Internal PT

## Type of activity and objectives
The objective of this engagement was to conduct an internal penetration assessment for the organization. The aim was to identify potential vulnerabilities that might be exploited by external sources, with the ultimate goal of preventing unauthorized access and compromise.
## Scope of evaluation
The evaluation was focused on the internal surface of the organization. This scope encompassed assessing the security and potential vulnerabilities within this internal surface.
## Executive Summary

The primary goal of this activity was to determine the adequacy of network segregation, ensuring that the LAYER 4 network did not have unintended access to the underlying networks, including the LAYER 2.5 and LAYER 2 networks. While the team was unable to gain unintended access to these networks, they identified vulnerabilities of significant importance, which will be reported.

The most critical issue, classified as "High", involves a Directory Traversal vulnerability that allowed the team to read and download contents from the target machine. A more detailed analysis of this vulnerability will be provided in the next chapter, along with a Proof of Concept (PoC) for better understanding of the issue.

Another significant discovery relates to the possibility of obtaining password hashes for valid accounts, affecting the IPMI 2.0 protocol. The ability to retrieve password hashes for valid accounts can have serious security implications, as these hashes could be subject to cracking attempts by attackers.
## Finding Summary
- DIR Traversal
- IPMI 2.0 Hash Disclosure
- Telnet opened without credentials
## Risk Impact Graph with CVSS Scores


## Vulnerability Types Distribution

![](https://raw.githubusercontent.com/blitz0p3rations/blitz0p3rations.github.io/master/uploads/id4.png)

## Attack storyline and findings
### DIR Traversal
- CVSS Vector: High
#### Proof of Concept (PoC) 
After analyzing the target 172.16.111.16, using nmap, the team discovered an open port 3000. Upon visiting, it was found to host the configuration manual for the DeltaV product. Subsequently, the team employed Burp Suite to scrutinize the web page, utilizing a payload that applied double URL encoding on all characters of "../".

During the analysis, a vulnerability known as "Directory Traversal" was identified. This vulnerability allowed access to the server's content, enabling the team to download documents and Excel files and to identify users present on the server. The team also managed to download several Excel files and other documents found during the investigation.
#### Remediations
1. **Input Validation and Sanitization**: It is critical to validate and sanitize all inputs, particularly those containing a sequence of dots (..), which are commonly used in Directory Traversal attacks. This process involves checking inputs against a set of rules or patterns to ensure they are secure and do not contain malicious content.
    
2. **Use of Whitelists**: Implementing a whitelist approach can significantly enhance security. This involves defining a list of approved inputs or resources that the system can accept or access. By allowing only pre-approved inputs, the system can effectively prevent unauthorized access or retrieval of files, as any input or request not on the whitelist would be rejected.
### IPMI 2.0 Hash Disclosure
- CVSS Vector: High
#### Proof of Concept (PoC) 

During the discovery phase, the team detected the presence of UDP ports 623 and 664 on the targets listed under "Affected Machine." Subsequent targeted research and the use of Metasploit enabled the team to determine that the service running on these ports was identified as IPMI 2.0.

Further utilizing Metasploit, the team successfully executed a "dump" of the hash for the "Administrator" user account. Once these hashes were obtained, the team conducted attacks known as "Offline Dictionary Attacks." This type of attack involves attempts to decipher the password using a predefined list of potential candidates. This method is particularly effective against weak or commonly used passwords, as it leverages the probability of matching a password with one of the listed candidates in the dictionary.
#### Remediations

1. **Disable IPMI if Not Necessary**: If the Intelligent Platform Management Interface (IPMI) is not essential for your operations, it's advisable to disable it. Disabling unnecessary services reduces the attack surface and prevents potential vulnerabilities from being exploited.
    
2. **Use Strong Passwords**: Implementing strong, complex passwords is crucial to limit the effectiveness of offline dictionary attacks. Strong passwords typically include a mix of uppercase and lowercase letters, numbers, and special characters. They should be of considerable length and not contain common phrases or easily guessable information. The complexity and uniqueness of passwords make them less susceptible to being cracked through dictionary attacks.

### Telnet Opened port without authentication
- CVSS Vector: High
#### Proof of Concept (PoC) 

During the testing phase, a telnet service on port 23 was discovered on the indicated hosts. When connecting via Telnet, no credentials were required for access. This lack of authentication presents a significant security risk, as it allows anyone who connects to potentially modify the configuration of the machines, including setting the Administrator password.

This vulnerability exposes the system to unauthorized access and control, making it imperative to address this security flaw promptly to protect against potential exploitation and compromise of the system's integrity.
#### Remediations
- **Implement SSH**.
- **Use Strong Passwords**: Implementing strong, complex passwords is crucial to limit the effectiveness of offline dictionary attacks. Strong passwords typically include a mix of uppercase and lowercase letters, numbers, and special characters. They should be of considerable length and not contain common phrases or easily guessable information. The complexity and uniqueness of passwords make them less susceptible to being cracked through dictionary attacks.

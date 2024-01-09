---
layout: post
title: Hospital Internal PT via Assume Breach
tags:
  - internal-network
  - AD
  - real-activity
hero: https://images.unsplash.com/photo-1495149905644-c9f27692c2c3?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1475&q=80
overlay: red
---

 {: .lead} <!–-break-–>

# Hospital Internal network via assume breach 

## Type of activity and objectives
The objective of this activity is to conduct a penetration test on the target system, utilizing a machine within the same network. This test aims to assess the security posture of the target, identify vulnerabilities, and potentially exploit them to simulate real-world attack scenarios. 
By performing this penetration test from within the same network, we can assess the effectiveness of the network segmentation and security controls while identifying potential risks that an insider threat might exploit. 
The results of this test will provide valuable insights into the overall security of the target system and guide the implementation of necessary remediation measures to enhance its defences.
## Scope of evalutaion
The scope of evaluation for this assessment encompasses the target network and specific IP address. During this evaluation, we will focus on assessing the security of the designated network and the identified IP address. Our analysis will include identifying potential vulnerabilities, weaknesses, and areas of concern within the given network and IP range. Through thorough testing and analysis, we aim to provide valuable insights into the security posture of the target network and IP, highlighting any potential risks that may need to be addressed.
## Executive Summary
During the enumeration of the Active Directory environment, the team identified a Domain Admin account vulnerable to Kerberoasting, attributed to the configuration of its Service Principal Name (SPN). After obtaining and cracking the account's ticket, the team gained Administrative access to the entire domain, effectively compromising the whole hospital network.

The simulation also included stress-testing the hosts to evaluate the effectiveness of existing detection measures. The results indicated almost no detection capabilities, as every step attempted by the team was completed without encountering any issues. This finding highlights significant deficiencies in the network's intrusion detection and response mechanisms, pointing to the need for substantial improvements in the hospital's cybersecurity posture.
## Finding summary
- Kerberoasting to Domain Admin

## Risk Impact Graph Severity Scores

![](https://raw.githubusercontent.com/blitz0p3rations/blitz0p3rations.github.io/master/uploads/ad1.png)

## Vulnerability Types Distribution

![](https://raw.githubusercontent.com/blitz0p3rations/blitz0p3rations.github.io/master/uploads/ad2.png)  

## Attack storyline and findings

The team's approach and findings align with various tactics and techniques identified in the MITRE ATT&CK framework, particularly concerning privilege escalation and credential access within an Active Directory environment.

1. **Command and Control with explorer.exe**: Utilizing `explorer.exe` to execute system commands or executables for information extraction aligns with the MITRE ATT&CK technique T1106 (Native API). This technique involves the use of native processes to interact with the system and gather valuable data.
    
2. **Bloodhound Analysis for Privilege Escalation**: The use of Bloodhound for analyzing paths to elevate privileges is indicative of the MITRE ATT&CK technique T1068 (Exploitation for Privilege Escalation). This approach aims to identify exploitable vulnerabilities in systems or applications that can grant higher-level permissions.
    
3. **Kerberoasting**: The process of Kerberoasting, targeting Domain Admins with the SPN set, falls under the MITRE ATT&CK technique T1558.003 (Kerberoasting). This technique involves requesting service tickets for service accounts and then attempting to crack them offline to reveal plaintext passwords.
    
4. **Targeting the sql-admin User**: Cracking the password of the `sql-admin` user, who had high privileges including Domain Admin, is an example of the MITRE ATT&CK technique T1003 (OS Credential Dumping). Specifically, this involves the extraction of credentials from the memory of the `lsass.exe` process.
    
5. **Compromise of the AD Domain**: Obtaining a Domain Admin's credentials allowed for complete compromise of the AD domain, aligning with MITRE ATT&CK's T1078 (Valid Accounts) technique. This technique entails using legitimate credentials to gain wide-ranging access across the network.
    
6. **Next Steps for Credential Collection**:
    
    - Cracking hashes with a local cracking station corresponds to MITRE ATT&CK’s T1003 (OS Credential Dumping).
    - Dumping the `lsass.exe` process memory to collect cleartext credentials aligns with the same technique, T1003.

The lack of detection during these activities points to a need for improved security monitoring and response systems within the network, in line with MITRE ATT&CK’s detection techniques. This includes enhancing intrusion detection systems, implementing anomaly detection algorithms, and regularly auditing logs for suspicious activities.


### Remediations

1. **Restrict and Monitor the Use of Powerful Accounts**: Ensure that Domain Admin accounts and other high-privilege accounts are used sparingly and monitored closely. Regularly review and update account privileges to adhere to the principle of least privilege.
    
2. **Implement Strong Password Policies**: Enforce complex password requirements to mitigate the risk of password cracking, particularly for service accounts vulnerable to Kerberoasting attacks. Consider using a password manager for generating and storing strong, unique passwords.
    
3. **Regularly Patch and Update Systems**: Keep all systems, particularly those running critical services, regularly updated and patched to reduce the likelihood of exploitation through known vulnerabilities.
    
4. **Enhance Monitoring and Logging**: Improve detection capabilities by implementing robust logging and monitoring systems. Regularly review security logs for unusual activities, especially access to sensitive systems and data.
    
5. **Implement Network Segmentation and Access Controls**: Segment the network to limit lateral movement within the domain. Implement strict access controls to sensitive areas of the network.
    
6. **Use Advanced Threat Detection Tools**: Employ tools like Bloodhound judiciously and ensure that threat detection systems are in place to identify unusual network patterns or behaviors indicative of an attack.
    
7. **Regular Security Audits and Penetration Testing**: Conduct periodic security audits and penetration tests to identify and address new vulnerabilities.
    
8. **Educate and Train Staff**: Regularly train staff on security best practices and awareness to prevent social engineering attacks.
    
9. **Secure Management of Service Principal Names (SPNs)**: Carefully manage and monitor SPNs, especially for accounts with high-level privileges, to prevent Kerberoasting.
    
10. **Credential Guard**: Implement Credential Guard in Windows environments to protect credentials stored in memory from being harvested.

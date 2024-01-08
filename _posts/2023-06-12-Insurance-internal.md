---
layout: post
title: 'Insurance Internal PT via Assume Breach'
tags:
  - internal-network
  - AD
  - real-activity
hero: https://images.unsplash.com/photo-1541955193702-9ca03b1bb11a?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1470&q=80
overlay: red
---

 {: .lead} <!–-break-–> 

# Insurance Internal network via assume breach 

## Type of activity and objectives
The objective of this activity is to conduct a penetration test on the target system, utilizing a machine within the same network. This test aims to assess the security posture of the target, identify vulnerabilities, and potentially exploit them to simulate real-world attack scenarios. 
By performing this penetration test from within the same network, we can assess the effectiveness of the network segmentation and security controls while identifying potential risks that an insider threat might exploit. 
The results of this test will provide valuable insights into the overall security of the target system and guide the implementation of necessary remediation measures to enhance its defences.
## Scope of evalutaion
The scope of evaluation for this assessment encompasses the target network and specific IP address. During this evaluation, we will focus on assessing the security of the designated network and the identified IP address. Our analysis will include identifying potential vulnerabilities, weaknesses, and areas of concern within the given network and IP range. Through thorough testing and analysis, we aim to provide valuable insights into the security posture of the target network and IP, highlighting any potential risks that may need to be addressed.
## Executive Summary
During the enumeration of the initial machine and the Active Directory (AD) domain, the team was able to gather information regarding:

- Local users and domain users who had access to the same workstation.
- Multiple shares containing various documents, some of which were sensitive. Within these shares, old credentials and user details were recovered.
- Remote Desktop Protocol (RDP) access to a Windows Server 2012 within the target domain. Using the recent PrintNightmare exploit, the team obtained reverse shells. Due to administrative privileges and the absence of local defensive systems, credential hashes were extracted from memory using Mimikatz. One of these hashes, belonging to the Administrator account, was successfully cracked. The information gathered allowed the team to impersonate users by utilizing the hashes and Pass the Hash (PTH) technique or to check if the cracked credential was reused elsewhere.

The outcome was administrative access to several domain servers, facilitated by the reuse of a simple password.
## Finding summary
- PrintNightmare to local admin
- PTH to admin on juicy machines
## Attack storyline and findings


The activities described align with various tactics and techniques in the MITRE ATT&CK framework, illustrating a sophisticated approach to network compromise:

1. **Exploitation of 'PrintNightmare' for Reverse Shell (T1190)**: The utilization of the 'PrintNightmare' vulnerability to gain a reverse shell on the target machine is an example of Exploit Public-Facing Application (T1190). This technique involves taking advantage of vulnerabilities in public-facing applications to gain unauthorized access.
    
2. **Information Gathering with Bloodhound (T1087, T1069)**: Using Bloodhound for enumeration purposes aligns with techniques like Account Discovery (T1087) and Permission Groups Discovery (T1069) within the Discovery tactic. Bloodhound is particularly effective in mapping out relationships and permissions within an Active Directory environment.
    
3. **Credential Dumping with Mimikatz (T1003)**: Employing Mimikatz to extract credential hashes from memory is indicative of the OS Credential Dumping technique (T1003). This tactic is commonly used to gather credentials for further lateral movements or escalation of privileges.
    
4. **Pass the Hash for Lateral Movement (T1550.002)**: Using the obtained hashes to perform lateral movement to more sensitive or 'juicy' machines is an example of the Pass the Hash (T1550.002) technique. It allows attackers to authenticate to remote servers or services using the underlying NTLM or LanMan hash of a user's password, bypassing the need for the plaintext password.


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

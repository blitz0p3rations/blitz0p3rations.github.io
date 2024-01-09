---
layout: post
title: 'Builder Internal PT via Assume Breach'
tags:
  - internal-network
  - AD
  - real-activity
hero: https://images.unsplash.com/photo-1541955193702-9ca03b1bb11a?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1470&q=80
overlay: red
---
 {: .lead} <!–-break-–> 

# Builder Internal network via assume breach 

## Type of activity and objectives
The objective of this activity is to conduct a penetration test on the target system, utilizing a machine within the same network. This test aims to assess the security posture of the target, identify vulnerabilities, and potentially exploit them to simulate real-world attack scenarios. 
By performing this penetration test from within the same network, we can assess the effectiveness of the network segmentation and security controls while identifying potential risks that an insider threat might exploit. 
The results of this test will provide valuable insights into the overall security of the target system and guide the implementation of necessary remediation measures to enhance its defences.
## Scope of evalutaion
The scope of evaluation for this assessment encompasses the target network and specific IP address. During this evaluation, we will focus on assessing the security of the designated network and the identified IP address. Our analysis will include identifying potential vulnerabilities, weaknesses, and areas of concern within the given network and IP range. Through thorough testing and analysis, we aim to provide valuable insights into the security posture of the target network and IP, highlighting any potential risks that may need to be addressed.
## Executive Summary
During the initial analysis, the starting workstation was found to lack useful information for executing lateral movement attempts, and the presence of some locally mapped shares did not yield additional usable attack vectors. However, moving on to list the Service Principal Names (SPNs) present in the infrastructure, the team was able to request several related Ticket Granting Services (TGS) and successfully crack them, obtaining cleartext credentials of various Service Accounts.

Once the Service Accounts were compromised, the Red Team conducted lateral movements towards achieving the main objectives set by the client. Specifically, the team gained access to the Business Intelligence within the company's SharePoint with the highest possible privileges, SYSTEM.

In the second kill chain, the team managed to obtain Domain Admin privileges and potentially take control of the infrastructure. This multi-faceted approach underscores the importance of securing both user workstations and the broader network infrastructure to protect against sophisticated cyber threats.
## Finding summary
- Kerberoasting to accessing Business Intelligence (Sharepoint)
- Kerberoasting to Domain Admin

## Risk Impact Graph Severity Scores

![](https://raw.githubusercontent.com/blitz0p3rations/blitz0p3rations.github.io/master/uploads/ad1.png)

## Vulnerability Types Distribution

![](https://raw.githubusercontent.com/blitz0p3rations/blitz0p3rations.github.io/master/uploads/ad2.png)

## Attack storyline and findings

1. **Information Gathering with Bloodhound and ADExplorer (T1087, T1069)**: Using tools like Bloodhound and ADExplorer to gather information about the infrastructure aligns with Discovery techniques in MITRE, specifically Account Discovery (T1087) and Permission Groups Discovery (T1069). These techniques involve identifying user accounts and understanding group memberships within an Active Directory environment.
    
2. **Kerberoasting (T1558.003)**: The act of obtaining and cracking the Ticket Granting Service (TGS) hashes of service accounts is known as Kerberoasting, a Credential Access technique. This approach exploits the Kerberos protocol's functionality to crack the hashes offline and retrieve plaintext credentials.
    
3. **Analysis of Compromised Service Accounts (T1069)**: Analyzing compromised service accounts to confirm their membership in sensitive groups like FINANCES, PURCHASE, SALES, and OPERATION falls under the Permission Groups Discovery technique. This analysis helps identify high-value targets for further exploitation.
    
4. **Accessing SharePoint (T1078, T1021)**: Using compromised accounts to access SharePoint, despite their lack of interactive login permissions, involves Valid Accounts (T1078) and Remote Services (T1021). These techniques focus on using valid credentials to gain access and leverage different protocols for lateral movement within the network.
    
5. **Command Execution as Administrator (T1078, T1053)**: The ability of the compromised user Y to execute commands as an administrator on various servers aligns with the Valid Accounts and Scheduled Task/Job techniques. This capability indicates elevated privileges across multiple systems.
    
6. **Domain Admin Privileges (T1003, T1069)**: Successfully obtaining credentials for a highly privileged domain admin account through various credential dumps aligns with OS Credential Dumping (T1003) and Permission Groups Discovery (T1069). These tactics indicate a significant compromise of the network, allowing broad access and control.


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

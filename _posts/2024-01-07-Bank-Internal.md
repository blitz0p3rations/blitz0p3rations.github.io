 {: .lead} <!–-break-–> 

# Bank Internal network via assume breach 

## Type of activity and objectives
The objective of this activity is to conduct a penetration test on the target system, utilizing a machine within the same network. This test aims to assess the security posture of the target, identify vulnerabilities, and potentially exploit them to simulate real-world attack scenarios. 
By performing this penetration test from within the same network, we can assess the effectiveness of the network segmentation and security controls while identifying potential risks that an insider threat might exploit. 
The results of this test will provide valuable insights into the overall security of the target system and guide the implementation of necessary remediation measures to enhance its defences.
## Scope of evalutaion
The scope of evaluation for this assessment encompasses the target network and specific IP address. During this evaluation, we will focus on assessing the security of the designated network and the identified IP address. Our analysis will include identifying potential vulnerabilities, weaknesses, and areas of concern within the given network and IP range. Through thorough testing and analysis, we aim to provide valuable insights into the security posture of the target network and IP, highlighting any potential risks that may need to be addressed.
## Executive Summary

The security assessment conducted by our team followed two effective attack paths, both yielding significant insights into the network's vulnerabilities. These paths are closely aligned with established tactics and techniques within the MITRE ATT&CK framework, emphasizing the sophistication of the approach.

1. **User Enumeration and Kerberoasting**: The first approach involved enumerating users with Service Principal Names (SPNs) and executing Kerberoasting. This strategy falls under Account Discovery (T1087) and Kerberoasting (T1558.003) in the MITRE framework. By exploiting the Kerberos protocol, our team was able to force the issuance of service tickets, which were then cracked offline to reveal plaintext credentials of accounts with administrative or high privileges. This method highlighted a key vulnerability in credential management and access control within the network.
    
2. **Exploiting Local Vulnerabilities for Privilege Escalation**: The second approach focused on local vulnerabilities that enabled standard users to elevate their privileges to NT AUTHORITY/SYSTEM. Classified under the Exploitation for Privilege Escalation technique (T1068) in MITRE, this method exploited system weaknesses to gain higher-level permissions. This was a pivotal step in demonstrating the depth of potential system compromise and underscored the need for robust local security measures.

## Finding summary
- Kerberoasting to Domain Admin
## Attack storyline and findings

The team's approach, which followed two distinct attack paths, both proved to be effective. This approach aligns with several techniques outlined in the MITRE ATT&CK framework:

1. **User Enumeration and Kerberoasting (T1087, T1558.003)**: Enumerating users with Service Principal Names (SPNs) and performing Kerberoasting to crack the tickets of accounts with administrative or high-level privileges involves Account Discovery (T1087) and Kerberoasting (T1558.003). These techniques are part of the Discovery and Credential Access tactics, respectively. Kerberoasting exploits the Kerberos protocol to force the service to provide a ticket, which can then be cracked offline to reveal plaintext credentials.
    
2. **Exploiting Local Vulnerabilities for Privilege Escalation (T1068)**: The focus on local vulnerabilities that allow standard users to elevate their privileges to NT AUTHORITY/SYSTEM corresponds with the Exploitation for Privilege Escalation technique (T1068). This involves taking advantage of system weaknesses to gain higher-level permissions, a critical step in deepening system compromise.

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
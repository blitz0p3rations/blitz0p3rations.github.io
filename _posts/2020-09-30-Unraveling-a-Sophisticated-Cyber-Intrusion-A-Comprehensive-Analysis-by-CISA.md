---
layout: post
title: 'Unraveling a Sophisticated Cyber Intrusion: A Comprehensive Analysis by CISA'
tags:
  - apt
  - intelligence
hero: https://images.unsplash.com/photo-1550751827-4bd374c3f58b?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1470&q=80
overlay: blue
---

The Cybersecurity and Infrastructure Security Agency (CISA) recently disclosed an intricate cyber intrusion that targeted a government agency's critical infrastructure. This article provides a detailed breakdown of the attack, as documented by CISA analysts, and sheds light on the attacker's methods, techniques, and potential motivations. {: .lead} <!–-break-–> 

# Initial Access and Credential Exploitation

The cyber threat actor gained entry into the agency's network by leveraging valid access credentials belonging to multiple Microsoft Office 365 (O365) and domain administrator accounts. The initial access was achieved through "Valid Accounts" [T1078], highlighting the importance of robust access control and monitoring mechanisms. The threat actor logged into a user's O365 account from IP address 91.219.236[.]166 and accessed a SharePoint site, downloading a file in the process.

CISA analysts were unable to ascertain how the attacker initially acquired the credentials. However, it is plausible that the attacker exploited a known vulnerability in the agency's unpatched VPN server—CVE-2019-11510 in Pulse Secure—to gain unauthorized access [T1212]. Pulse Secure had released patches for critical vulnerabilities, including CVE-2019-11510, but it appears that the agency had not applied these updates. Widespread exploitation of this vulnerability across the federal government further underscores the importance of timely patch management.

# Exploration and Account Manipulation

After gaining entry, the threat actor engaged in "Discovery" [TA0007] by logging into an O365 email account from IP address 91.219.236[.]166. Here, they viewed and downloaded attachments from the help desk's emails, seeking information related to "Intranet access" and "VPN passwords." Despite already possessing privileged access, the actor utilized Remote Desktop Protocol (RDP) from IP address 207.220.1[.]3 to log into the same email account.

The attacker then proceeded to enumerate the Active Directory and Group Policy key and made changes to a registry key for the Group Policy [T1098]. Employing common Microsoft Windows command line processes, such as conhost, ipconfig, net, query, netstat, ping, and whoami, along with plink.exe, the attacker extensively probed the compromised system and network, as part of "Command and Scripting Interpreter" and "System Network Configuration Discovery" [T1059, T1016].

# Establishing Persistence and Command and Control

To ensure prolonged access, the cyber threat actor set up "Persistence" [TA0003] and "Command and Control" [TA0011] within the victim network. They achieved this by creating a persistent Secure Socket Shell (SSH) tunnel/reverse SOCKS proxy, running inetinfo.exe (a unique, multi-stage malware used to drop files), and setting up a locally mounted remote share on IP address 78.27.70[.]237 [T1090]. These maneuvers enabled the attacker to move discreetly during their operations, leaving fewer artifacts for forensic analysis.

# Data Collection and Exfiltration

Having established a foothold, the threat actor created a local account, which they employed for "Data Collection," "Exfiltration," "Persistence," and "Command and Control" [T1136]. Utilizing this account, the attacker browsed directories on a victim file server, copied files to their locally mounted remote share, and interacted with PowerShell module Invoke-TmpDavFS.psm.

Exfiltration of data from an account directory and file server directory was conducted using the Microsoft Windows Terminal Services client, tsclient, making detection more challenging [T1005, T1039]. Additionally, the actor created compressed Zip files to potentially exfiltrate data. However, the actor skillfully masked their activities, making it difficult for analysts to confirm the extent of data exfiltration.

# Conclusion

The CISA's detailed analysis of this sophisticated cyber intrusion provides critical insights into the tactics, techniques, and procedures employed by the threat actor. The attack highlights the importance of proactive cybersecurity measures, including timely patching, access control, network monitoring, and incident response planning. Organizations, both in the public and private sectors, can learn valuable lessons from this incident to bolster their defense against ever-evolving cyber threats and secure their critical infrastructure effectively.

### References
1. https://content.govdelivery.com/accounts/USDHSCISA/bulletins/2a25e26
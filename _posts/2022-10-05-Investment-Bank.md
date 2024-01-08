---
layout: post
title: 'Investment Bank Wireless PT'
tags:
 - wireless
 - real-activity
hero: https://images.unsplash.com/photo-1501167786227-4cba60f6d58f?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxzZWFyY2h8Mnx8YmFua3xlbnwwfHwwfHx8MA%3D%3D&auto=format&fit=crop&w=400&q=60
overlay: blue
---

Please note that for this proof of concept, while images and step-by-step reproduction tips are fundamental for evidentiary purposes, they will not be supplied. Furthermore, in adherence to our commitment to privacy and compliance with non-disclosure agreements, all URLs and functionalities within this assessment have been anonymized. {: .lead}
 <!--break-->

# Investment Bank

## Type of activity and objectives
The objective of this engagement was to conduct a wireless penetration assessment for the organization. The aim was to identify potential vulnerabilities that could potentially be exploited by an attacker nearby, to prevent unauthorized access, compromise and data exfiltration.
## Scope of evaluation
The evaluation was focused on the SSID and guest network of the organization. This scope encompassed assessing the security and potential vulnerabilities within this surface.
## Executive Summary
The conducted network assessment revealed several concerning findings in the target environment. The vulnerabilities and weaknesses identified could potentially lead to unauthorized access, data breaches, and compromised security. The main findings include:

Leak of Guest Network Segmentation: The assessment detected a leakage in the segmentation of the guest network. This misconfiguration could allow unauthorized users to gain access to sensitive internal resources, leading to data exposure and potential unauthorized activities.

WPA2 Handshake Captures: During the assessment, three instances of full WPA2 4-way handshake captures were identified. This indicates potential security gaps in the wireless network infrastructure, making it susceptible to unauthorized access or eavesdropping.

Domain Credential Obtained from WPA2EAP: The assessment also revealed the acquisition of domain credentials from a WPA2 Enterprise network. This security breach can allow attackers to impersonate legitimate users and potentially gain unauthorized access to critical systems and data.
## Finding Summary
- Leak of Guest network segmentation 
- 3x WPA2 Full 4-way handshake captured
- 1x Domain credential obtained from WPA2EAP

## Risk Impact Graph with CVSS Scores

![](https://raw.githubusercontent.com/blitz0p3rations/blitz0p3rations.github.io/master/uploads/id31.png)

## Vulnerability Types Distribution

![](https://raw.githubusercontent.com/blitz0p3rations/blitz0p3rations.github.io/master/uploads/id32.png)

## Attack storyline and findings### Leak of Guest network segmentation
- CVSS Vector: None
#### Proof of Concept (PoC) 
After gaining access to the Guest network, default IP addresses were found to be assigned as 172.18.18.18 and 172.18.18.16. This analysis indicates the potential to identify certain devices that should not be accessible from the Guest network. On some of these devices, it was possible to successfully log in using easily obtainable default credentials. Notably, this issue affected devices in the New York office and other locations.

Some devices that anybody in the guest network coul reach, in a few of them the team got access via default credentials.

- Forcepoint security solution identified as vulnerable.
- Cisco conference phone exploited for unauthorized access.
- Brother MFC-L2710DW series printer compromised in the New York location.
- HP LaserJet printer compromised.
- IBM Guardium security system encountered vulnerabilities.
- IBM Storwize Assistant Tool exposed to exploitation.
- Successful login to a custom third-party system.
- Seven instances of Tomcat servers were identified.
- Three instances of directory listing vulnerabilities.
- Canon cameras in the Luxembourg office were compromised.
- GlassFish server found to be vulnerable.
- HP LaserJet printer in the Luxembourg office compromised.
- Four instances of JBoss servers were detected.
- IIS web server identified as vulnerable.
- VPN login cloned.
- Jenkins server found to have vulnerabilities.
#### Remediations
- Network Segmentation: Separate the guest network from the internal network by creating dedicated VLANs and subnets for each network. This prevents unauthorized access to sensitive resources.

- Firewall Rules: Deploy a firewall between the guest network and the internal network. Configure strict firewall rules that allow only necessary traffic from the guest network to the internal network and vice versa.

### 3x WPA2 Full 4-way handshake captured
- CVSS Vector: None
#### Proof of Concept (PoC) 
In the initial phase, the team's objective was to capture the data exchange between the victim and the access point by obtaining the 4-way handshake. This involved monitoring each access point of various devices. This method proves to be effective and reliable as it can be applied in various scenarios to capture authentication attempts, which can later be subjected to offline brute-force attacks. However, during this phase, the team was unsuccessful in achieving this goal due to a significant number of employees accessing the network through company-provided wired connections.

In the second phase of the attack, two additional different attack techniques were employed:

1. **Rogue Captive Portal Creation:** This technique involves creating a fake Access Point that emulates an arbitrary Wi-Fi network controlled by the attackers. Once the connection is established, the device redirects the victim to a login page where they are prompted to enter their credentials, falling into the attacker's trap. However, similar to the previous phase, the results were not satisfactory as no user connected to the Captive Portal.

Despite the team's efforts to employ these attack techniques, the results did not yield the desired outcome. This highlights the challenges posed by employee behaviour and network dynamics in successfully executing such tactics. Further refinement and adaptation of strategies may be required to effectively carry out such attacks in the future.

The only success the team achieved was acquiring three WPA2 full 4-way handshakes; however, we were unable to crack them.
#### Remediations
- None
### 1x Domain credential obtained from WPA2EAP
- CVSS Vector: None
#### Proof of Concept (PoC) 
An effective result was achieved by setting up a RADIUS server using Eaphammer as a third phase, aimed at intercepting WPA Enterprise credentials entered by the user while attempting to connect to our specially configured access point. This approach successfully intercepted valid domain credentials.
#### Remediations
- Rogue AP Detection: Deploy wireless intrusion detection systems (WIDS) to identify unauthorized or rogue access points and take appropriate action.
- Deauth Prevention: These routers are designed to detect and block unauthorized deauth packets, ensuring that devices remain connected to the network and reducing the chances of disruptions.

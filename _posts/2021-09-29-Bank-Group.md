---
layout: post
title: 'Bank Group VA'
tags:
 - vulnerability-assessment
 - real-activity
hero: 
overlay: red
---

Please note that for this proof of concept, while images and step-by-step reproduction tips are fundamental for evidentiary purposes, they will not be supplied. Furthermore, in adherence to our commitment to privacy and compliance with non-disclosure agreements, all URLs and functionalities within this assessment have been anonymized. {: .lead}
 {: .lead} <!--break-->

# Disclaimer 
In this report, a deliberate approach will be taken to avoid discussing specific vulnerabilities and the detailed intricacies of banks' infrastructure. This decision is rooted in the sensitive nature of such information and the potential risks associated with its disclosure. The primary objective is to safeguard the confidentiality of this data, thereby upholding the security of these institutions.

Given the importance of preventing any adverse outcomes that might result from revealing detailed information, the focus will instead be on outlining a range of common vulnerabilities. While this selection is not exhaustive, it is based on insights gained from conducting over 70 bank network assessments. The aim is to provide valuable information while ensuring the utmost protection of sensitive data.

# Bank Group

## Type of activity and objectives
The primary objective of this engagement was to conduct bi-annual vulnerability assessments on the network infrastructure across over 70 branches of a major banking group. Each branch operates autonomously, managed by distinct executive teams and staff. The scope of this activity encompassed not only the execution of vulnerability assessments but also the subsequent presentation of findings. These findings were tailored to the unique needs of both technical staff and bank executives. Accordingly, each branch was provided with a customized executive report detailing the high-level insights, as well as a more technical report outlining specific remediation strategies.
## Scope of evaluation
The scope of the evaluation encompassed a list of internal subnets within the infrastructure of each target bank.
## Executive Summary
The recent Vulnerability Assessment conducted on the bank's infrastructure focused significantly on Cash-In-Cash-Out (CICO) machines and Automated Teller Machines (ATMs). These areas are particularly prone to critical vulnerabilities, such as EternalBlue. Additionally, the widespread use of default credentials across various assets, including printers, cameras, VNC servers, and remote vulnerable NAS, was identified as a considerable security risk.

A notable concern was the network infrastructure related to surveillance. Many devices, including those from brands like Hikvision and Xiaomi, were found to be vulnerable. This sector, in particular, appeared to be inadequately updated and maintained by the bank staff.

Furthermore, the assessment highlighted the prevalence of outdated Network Attached Storage (NAS) devices and obsolete switches within the network. This finding underscores the potential security risks and emphasizes the need for regular updates and maintenance in the network environment.

## Risk Impact Graph with CVSS Scores

![](https://raw.githubusercontent.com/blitz0p3rations/blitz0p3rations.github.io/master/uploads/va1.png)

## Vulnerability Types Distribution

![](https://raw.githubusercontent.com/blitz0p3rations/blitz0p3rations.github.io/master/uploads/va2.png)

## Finding Summary
- EternalBlue Exploitation: The presence of systems vulnerable to EternalBlue exploitation poses a significant risk. This exploit allows unauthorized access to systems and potentially enables lateral movement within the network.

- BlueKeep Vulnerability: The BlueKeep vulnerability was detected, which can potentially lead to remote code execution on vulnerable systems. Immediate patching is recommended to mitigate this risk.

- Ricoh Default Credentials: The use of default credentials in Ricoh devices introduces a security gap, allowing unauthorized access and potential compromise of sensitive information.

- Outdated Network Attached Storage (NAS): The existence of outdated NAS devices exposes the organization to known vulnerabilities. Attackers could exploit these vulnerabilities to gain unauthorized access or disrupt operations.

- Vulnerable Cameras: Vulnerable cameras within the network pose a risk of unauthorized access and unauthorized surveillance, potentially leading to privacy breaches and unauthorized data collection.

- Outdated Switch: The presence of outdated switches introduces security risks as these devices may have known vulnerabilities that can be exploited by malicious actors.
#### Remediations
To address these findings and enhance the overall security posture, the following actions are advised:

- Patch Management: Swiftly apply patches and updates to systems vulnerable to EternalBlue and BlueKeep to prevent potential unauthorized access.

- Credential Management: Replace default credentials in Ricoh devices with strong, unique passwords to prevent unauthorized access.

- Device Upgrades: Update or replace outdated NAS devices and Aruba switches to mitigate the risk of known vulnerabilities.

- Camera Security: Secure vulnerable cameras by updating firmware, changing default passwords, and implementing network segmentation to prevent unauthorized access.

- Vulnerability Management: Continuously monitor and assess the network for vulnerabilities, applying patches and updates as required.

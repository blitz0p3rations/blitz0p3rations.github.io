---
layout: post
title: 'Bank Group VA'
tags:
 - va
 - real-engagement
hero: 
overlay: red
---

No images (image for the step by step PoC are essential as evidence but will not be provided
) or references will be provided, as this assessment was a real engagement. Additionally, all URLs and functionalities have been anonymized to ensure privacy and compliance with non-disclosure agreements (NDAs). {: .lead} <!--break-->

# Bank Group
In this "report based article", I will refrain from delving into the specifics of particular vulnerabilities and the intricate details of banks' infrastructure. Given the sensitive nature of this information and the potential for misuse, I aim to maintain its confidentiality.
It is essential to prioritize the security of these institutions and prevent any unintended negative consequences that could arise from exposing intricate details.
Instead, I will highlight a selection of common vulnerabilities, though not an exhaustive list, founded throughout my experience conducting over 70 bank network assessments.
## Type of activity and objectives
The primary objective of this engagement was to perform bi-annual vulnerability assessments on the network infrastructure of over 70 banks within the same group, each managed autonomously. The scope of the activity involved both the execution of vulnerability assessments and the subsequent presentation of findings to both technical staff and bank executives, each bank will receive his custom executive report and the more technical remediaitons report.
## Scope of evaluation
The scope of the evaluation was centered on the internal infrastructure of each target bank.
## Executive Summary
Throughout the comprehensive Vulnerability Assessment conducted on the bank's infrastructure, particular emphasis was directed towards Cash-In-Cash-Out (CICO) machines and Automated Teller Machines (ATMs), which frequently exhibit critical vulnerabilities like EternalBlue. Moreover, the presence of default credentials for various assets, such as printers and cameras, poses a significant risk to the organization's security posture.
The assessment also revealed the prevalence of outdated Network Attached Storage (NAS) devices and obsolete switches, reflecting potential security concerns within the network environment.
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
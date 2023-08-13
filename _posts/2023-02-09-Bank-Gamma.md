---
layout: post
title: 'Bank Gamma IOS mobile PT'
tags:
 - mobile
 - real-engagement
hero: https://images.unsplash.com/photo-1501167786227-4cba60f6d58f?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxzZWFyY2h8Mnx8YmFua3xlbnwwfHwwfHx8MA%3D%3D&auto=format&fit=crop&w=400&q=60
overlay: red
---

No images (image for the step by step PoC are essential as evidence but will not be provided
) or references will be provided, as this assessment was a real engagement. Additionally, all URLs and functionalities have been anonymized to ensure privacy and compliance with non-disclosure agreements (NDAs). {: .lead} <!--break-->

# Bank Gamma

## Type of activity and objectives
The objective of this engagement was to conduct a mobile penetration assessment for the organization. The aim was to identify potential vulnerabilities that could potentially be exploited from the mobile app, with the goal of preventing unauthorized access, compromise and data exfiltration.
## Scope of evaluation
The evaluation was focused on the Bank Account IOS Mobile app of the organization. This scope encompassed assessing the security and potential vulnerabilities within this surface.
## Executive Summary
The assessment of the Android bank account app revealed two significant findings: a root detection bypass vulnerability and the absence of certificate pinning. These vulnerabilities could expose the app and its users to potential security risks, including unauthorized access and data interception. It is crucial that these issues are addressed promptly to ensure the security and integrity of the app and the sensitive financial data it handles.
## Finding Summary
- Lack of certificate pinning
- IDOR
## Attack storyline or vulnerabilities with CVSS,CVE and remedations
The assessment revealed two significant findings in the target application. Firstly, there was a lack of certificate pinning, which could expose the application to potential man-in-the-middle attacks, compromising the security and integrity of data transmitted between the app and its servers. Secondly, an Insecure Direct Object Reference (IDOR) vulnerability was identified, leading to the leakage of SWIFT codes and bank account information belonging to other users. These findings highlight the importance of implementing proper security measures, including certificate pinning and access control mechanisms, to mitigate these vulnerabilities and protect sensitive user data.
### Lack of certificate pinning
- CVSS Vector: None
#### Proof of Concept (PoC) 
The mobile app lacked certificate pinning, which allowed interception of requests and traffic. By exploiting this vulnerability, an attacker could potentially intercept and manipulate the app's communication with external servers. This underscores the importance of implementing proper certificate pinning to ensure the integrity and security of data exchanged between the app and its backend servers.
#### Remediations
- Implement certificate pinning

### IDOR
- CVSS Vector: CVSS:3.0/AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:H
#### IDOR 
#### Proof of Concept (PoC)
During the testing phase, leveraging the user account obtained upon opening a bank account in the branch, it was possible to achieve unauthorized access to information related to bank accounts, SWIFT codes, transactions, and mandates belonging to other users. This action violated data confidentiality and compromised the privacy of Banca Gamma's clients. Insecure Direct Object Reference (IDOR) is a vulnerability in which unvalidated user input can be exploited to access resources or perform unauthorized operations. This type of vulnerability exploits implementation and design flaws in the application, allowing potential attackers to perform unintended actions. For instance, attackers manipulate legitimate functionalities to access information by bypassing authorization controls.

Exploiting this vulnerability could allow attackers to extract personal data of Banca Gamma's clients. The unauthorized exposure of such data could significantly damage the bank's reputation and trust with its clients. Additionally, the obtained information might be exploited for phishing and vishing activities targeting clients. The identified vulnerability could have serious reputational, financial, and legal consequences.

To reproduce the vulnerability, the following steps were taken:

1. Access specific paths within the application:
   - `rest-mobile/v5.0/utente/conti/1814477`
   - `rest-mobile/v5.0/utente/mandatisdd/1844177/delegations`
   - `rest-mobile/v5.0/utente/conti/1844177/transactions`
   - `rest-mobile/v5.0/utente/rapporti/1814477/max`

2. After logging into the application, intercept requests using a proxy tool like Burp Suite. Notice the presence of a unique ID value associated with the user session.

3. Exploit the vulnerability by configuring the request using the "Intruder" functionality in Burp Suite. Modify the ID value to access information related to other clients' bank accounts.

4. Run the attack using payload manipulation techniques, revealing information about other clients' bank accounts.

The potential attacker could gather information about accounts, transactions, mandates, and maximums of other clients by manipulating the ID parameter. In addition, it's recommended to review the request related to transactions, as it could also be vulnerable. 

The team demonstrated the existence of the vulnerability by enumerating a limited quantity of accounts and SWIFT codes as a proof of concept. In a real scenario, this vulnerability could potentially expose data of all Banca Gamma clients.

#### Remediations
- Role-Based Access Control (RBAC): Implement proper access controls based on user roles and permissions. Ensure that users can only access the data and resources that they are authorized to.

- Server-Side Validation: Implement server-side validation to ensure that user requests are properly authenticated and authorized before granting access to sensitive data or resources.

- Use Unique Identifiers: Avoid using predictable or sequential identifiers for sensitive data or resources. Use unique, non-guessable identifiers that cannot be easily manipulated by attackers.
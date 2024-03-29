---
layout: post
title: 'Freeze Company External PT'
tags:
 - web
 - real-activity
hero: https://images.unsplash.com/photo-1545769392-290199b65c80?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1470&q=80
overlay: red
---

No images (image for the step by step PoC are essential as evidence but will not be provided
) or references will be provided, as this assessment was a real engagement. Additionally, all URLs and functionalities have been anonymized to ensure privacy and compliance with non-disclosure agreements (NDAs). {: .lead} <!–-break-–>

# Freeze Company

## Type of activity and objectives
The objective of this engagement was to conduct an external penetration assessment for the organization. The aim was to identify potential vulnerabilities that could potentially be exploited from outside sources, to prevent unauthorized access and compromise.
## Scope of evaluation
The evaluation was focused on the specific website of the organization. This scope encompassed assessing the security and potential vulnerabilities within this website.
## Executive Summary
The assessment conducted on the target website revealed two findings regarding the exposure of the mailman and the presence of third-party arbitrary content after a specific path.
## Finding Summary
- Arbitrary content after /~admin/
- Exposed /mailman/admin
## Risk Impact Graph with CVSS Scores

![](https://raw.githubusercontent.com/blitz0p3rations/blitz0p3rations.github.io/master/uploads/id23.png)

## Vulnerability Types Distribution

![](https://raw.githubusercontent.com/blitz0p3rations/blitz0p3rations.github.io/master/uploads/id24.png)

## Attack storyline and findings### Arbitrary content after /~admin/ 
- CVSS Vector: None
#### Proof of Concept (PoC) 
In the web application after the path **/~admin/** there are third-party website not inherent within the original application.
This unexpected behaviour could potentially expose users to malicious or unauthorized content that is not inherent to the original application.
#### Remediations
- Restrict access to the directory
- Eliminate third-party content
### Exposed /mailman/admin
- CVSS Vector: None
#### Proof of Concept (PoC) 
During the evaluation, it was identified that the **/mailman/admin** directory is publicly exposed on the website. This exposure potentially allows unauthorized individuals to access administrative functionalities of the Mailman software. The exposure of administrative interfaces poses a significant security risk, as it could lead to unauthorized configuration changes, data exposure, or even potential compromise of the system. To mitigate this risk, it is recommended to restrict access to the /mailman/admin directory only to authorized personnel through proper access controls and security configurations.
#### Remediations
- Restrict access to the directory
- Implement a layer of authentication

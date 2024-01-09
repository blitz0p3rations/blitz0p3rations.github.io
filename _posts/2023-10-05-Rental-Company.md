---
layout: post
title: Rental Company Web PT
tags:
  - web
  - real-activity
hero: https://images.unsplash.com/photo-1462206092226-f46025ffe607?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1474&q=80
overlay: blue
---

Please note that for this proof of concept, while images and step-by-step reproduction tips are fundamental for evidentiary purposes, they will not be supplied. Furthermore, in adherence to our commitment to privacy and compliance with non-disclosure agreements, all URLs and functionalities within this assessment have been anonymized. {: .lead} <!–-break-–>

# Rental Company Web PT

## Type of activity and objectives
The objective of this engagement was to conduct an external penetration assessment for the organization. The aim was to identify potential vulnerabilities that might be exploited by external sources, with the ultimate goal of preventing unauthorized access and compromise.
## Scope of evaluation
The evaluation was focused on the outside surface of the organization. This scope encompassed assessing the security and potential vulnerabilities within this external surface.
## Executive Summary
The Web Application Penetration Test conducted within the defined scope revealed the presence of a Snapshot authentication bypass vulnerability, an HTML Injection vulnerability, and a Broken Access Control (IDOR) scenario.

The first vulnerability, if exploited, allows an unauthenticated malicious actor to view and potentially delete snapshots on the Grafana platform. However, since this target is internally exposed, the impact of this detected vulnerability is significantly reduced.

The second vulnerability, if exploited, enables a potential attacker to embed custom HTML elements within the application. This can be used to redirect or deceive users, especially when combined with social engineering techniques.

Additionally, on the target, a Broken Access Control scenario (IDOR) was detected. This allows users with the "Investor" profile to access a functionality that is disabled in their menu but available in the "Applicant" and "Partner" user profiles. This vulnerability highlights a significant flaw in access controls, where user roles are not properly segregated, leading to unauthorized access to functionalities not intended for their profile.

## Finding Summary
- HTML Injection
- IDOR
- CVE-2021-39226 (Snapshot authentication bypass)
## Risk Impact Graph with CVSS Scores


## Vulnerability Types Distribution




## Attack storyline and findings
### HTML Injection
- CVSS Vector: AV:N/AC:L/PR:N/UI:N/S:U/C:N/I:L/A:N
#### Proof of Concept (PoC) 

To confirm the presence of the vulnerability, the team conducted an arbitrary link insertion within the application using the injection process. To replicate the described scenario, the following payload `<a href=https://redacted.it>` was inserted as the value for “term”. As observed from the response, it appeared that the field did not accept the entered values, resulting in an error with a status code of 400.

However, it is crucial to note that the content of the payload was still correctly interpreted as HTML. This was confirmed by subsequent screenshots, which showed that the inserted link was indeed present on the dashboard. This evidence thus confirms the existence of the vulnerability.
#### Remediations
- Input Validation and Sanitization: Implement rigorous input validation and sanitization to prevent malicious data from being processed. This is particularly important for mitigating risks associated with HTML Injection and Cross-Site Scripting (XSS).

### IDOR
- CVSS Vector: AV:N/AC:L/PR:N/UI:N/S:U/C:N/I:L/A:N](AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:N/A:N
#### Proof of Concept (PoC) 
To replicate the scenario described, the team initially logged in using all three types of user accounts. It was observed that the "Pay with account X" functionality was exclusively disabled in the investor user profile. However, by accessing the system with the other two types of user accounts, the team gained access to the "Pay with account X" feature and noted the specific path where this functionality was available. Upon identifying the path, the team successfully accessed it using the investor user's session. As demonstrated by subsequent evidence, the "Pay with account X" direct transfer functionality was indeed available, confirming the presence of a Broken Access Control vulnerability. This allowed the investor user profile to access a feature that was meant to be restricted, highlighting a critical oversight in user role management and access control within the application.

#### Remediations
Data-level access controls should be implemented such that the server verifies whether the current user account has the necessary permissions for the requested functionality. Consequently, resource access should only be allowed after the server has performed a check on the user's privileges.
Include session and authorization controls to confirm that users are authenticated and authorized to access specific resources.


### Snapshot authentication bypass (CVE-2021-39226)
- CVSS Vector: AV:N/AC:L/PR:N/UI:N/S:U/C:L/I:L/A:L
#### Proof of Concept (PoC) 
.
To confirm the presence of the vulnerability, as a Proof of Concept (PoC), the team verified the accessibility of snapshots by an unauthenticated user. Evidence was gathered demonstrating access to the snapshot by an unauthenticated user, which is detailed below:

- `/api/snapshots/:key`

The team refrained from further actions to avoid causing potential service disruptions or data loss situations. However, to confirm the potential data loss impact associated with the vulnerability, it's sufficient to access the following path:

- `/api/snapshots-delete/:deleteKey`

This approach underscores the vulnerability's severity, allowing unauthenticated access to sensitive functionalities, and suggests the need for immediate remediation to safeguard the system against unauthorized access and potential data manipulation or deletion.
#### Remediations

1. **Update Grafana**: Implement the latest available release of Grafana, or install a version between 8.1.6 and 7.5.11. Updating to these versions ensures that the system is equipped with the latest security patches and fixes.
    
2. **Mitigation Measures**: If it is not feasible to install a patched version of Grafana immediately, consider implementing additional security measures such as:
    
    - Establishing a whitelist: Define and enforce a list of permitted entities that can access specific resources, particularly the vulnerable paths.
    - Setting up a reverse proxy: Use a reverse proxy to protect the following paths by controlling and filtering the incoming traffic:
        - `/api/snapshots/:key`
        - `/api/snapshots-delete/:deleteKey`
        - `/dashboard/snapshot/:key`

`



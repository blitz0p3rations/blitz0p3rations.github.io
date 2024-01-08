---
layout: post
title: Election System Back Office Web PT
tags:
  - web
  - real-activity
hero: https://images.unsplash.com/photo-1462206092226-f46025ffe607?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1474&q=80
overlay: blue
---
Please note that for this proof of concept, while images and step-by-step reproduction tips are fundamental for evidentiary purposes, they will not be supplied. Furthermore, in adherence to our commitment to privacy and compliance with non-disclosure agreements, all URLs and functionalities within this assessment have been anonymized. {: .lead}
 <!--break-->

# Election Back Office

## Type of activity and objectives
The objective of this engagement was to conduct an external penetration assessment for the organization. The aim was to identify potential vulnerabilities that might be exploited by external sources, with the ultimate goal of preventing unauthorized access and compromise.
## Scope of evaluation
The evaluation was focused on the outside surface of the organization. This scope encompassed assessing the security and potential vulnerabilities within this external surface.
## Executive Summary

During the tests, several significant vulnerabilities were identified, including clickjacking, Insecure Direct Object Reference (IDOR), and unrestricted file download.

Clickjacking, if exploited, can manipulate a user to perform actions beyond their control by redirecting clicks intended for the original page to another application or domain under the attacker’s control. This type of attack requires careful preparation and the use of Social Engineering techniques for effective exploitation, but it should not be overlooked due to its potential impact.

The IDOR vulnerability allows users with limited privileges to access functionalities reserved for users with higher privileges. A specific scenario was identified where a user with lower privileges can list registered users in the application and modify their passwords and assigned roles.

The final vulnerability discovered allows an unauthenticated user to access documentation within the application, which should only be available post-authentication. This exposes sensitive information and potentially compromises the security of the application.
## Finding Summary
- Clickjacking
- IDOR
- Unrestricted File Download
## Risk Impact Graph with CVSS Scores


## Vulnerability Types Distribution

![](https://raw.githubusercontent.com/blitz0p3rations/blitz0p3rations.github.io/master/uploads/id4.png)

## Attack storyline and findings
### Clickjacking
- CVSS Vector: None
#### Proof of Concept (PoC) 
The Proof of Concept (PoC) demonstrates the identification of a security issue in the "main.js" file of the application. By analyzing this file, sensitive credentials were discovered, which were then exploited to gain unauthorized access to the medical factory.
#### Remediations
- Never expose hardcoded secrets](<A missing HTTP header (X-Frame-Options) in the target web application has left customers vulnerable to clickjacking. Clickjacking is an attack that occurs when an attacker uses a transparent iframe in a window to trick a user into clicking on an actionable item, such as a button or link, to another server in which they have an identical webpage. The attacker essentially hijacks the user activity intended for the original server and sends it to the other server. This is an attack on both the user and the server.

Here's a simple Proof of Concept (PoC) for the Clickjacking attack:

1. Create an HTML page that contains your legitimate content. Let's call it "legit.html":
`
%3C!DOCTYPE html%3E
<html>
<head>
    <title>Legitimate Page</title>
</head>
<body>
    <h1>Welcome to Our Website</h1>
    <p>This is some important content.</p>
</body>
</html>
`

1. Create another HTML page that contains an invisible iframe that overlays the legitimate content. Let's call it "malicious.html":
`
<!DOCTYPE html>
<html>
<head>
    <title>Malicious Page</title>
    <style>
        iframe {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            opacity: 0;
        }
    </style>
</head>
<body>
    <iframe src="legit.html"></iframe>
    <h1>Click Me!</h1>
    <button onclick="performAttack()">Click Here</button>

    <script>
        function performAttack() {
            alert("Clickjacking Attack Successful!");
        }
    </script>
</body>
</html>
`

In this PoC, the "malicious.html" page contains an invisible iframe that loads the "legit.html" page. The attacker overlays a button on top of the iframe that seems harmless to the user. When the user clicks the button, they are clicking on the button in the overlaying "malicious.html" page, triggering the "performAttack()" function that shows an alert.


#### Remediations
- X-Frame-Options Header: Set the X-Frame-Options HTTP response header to prevent your website from being displayed within a frame or iframe on another site.

- Content Security Policy (CSP): Implement a CSP that restricts the domains that can embed your site's content. This helps prevent unauthorized embedding.

- Frame-Busting Scripts: Include frame-busting scripts in your web pages to break out of frames if your site is being framed by malicious sites.>)


### IDOR
- CVSS Vector: AV:N/AC:L/PR:N/UI:N/S:U/C:N/I:L/A:N](AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:N/A:N
#### Proof of Concept (PoC) 

During the testing process, several scenarios were identified where users with lower privileges could access features reserved for higher privilege users. One particular scenario was especially critical, as it allowed for password changes on arbitrary accounts.

Another equally critical scenario involved the ability to upload configuration strings. The team reported this potential issue without making any changes, to avoid causing service disruptions or configuration alterations. Using a lower privilege account, the team accessed features exclusively reserved for higher privilege users, with evidence provided below.

It was noted that the menu of a higher privilege account includes a section on personal data, unlike the account with lower privileges. Importantly, it's possible to access items in the submenu even using a lower privilege account. The configuration feature allows for adding a configuration string, but the team reported the possibility of accessing this feature via a lower privilege account, to avoid potential issues or undesired changes in the original application configuration.

Subsequently, a scenario was reported where lower privilege users could successfully enumerate all users in the application and change passwords for specific users, effectively enabling account takeover. In the first step, the team identified a serial number in the following API request. It was found that the same response could be obtained with both a basic user account and a higher privilege account.

In the second step, aiming to enumerate all users within the application, the team used the "Intruder" feature of Burp Suite Professional and configured the request as follows. After launching the attack, results were filtered by status code 200. The response obtained allowed a potential attacker to enumerate application users. Using this information, an attacker could change enumerated users' passwords and subsequently log in with those accounts.

Particular attention was given to information regarding assigned roles and the reference id values associated with each user. Using the same request, it was possible to modify the roles assigned to users, with the team adding administrator permissions to the user shown in the figure. The entire scenario was executed using a session of a user with basic privileges. It is important to note that password and role changes during the tests were performed only on accounts provided to the team.
#### Remediations
Data-level access controls should be implemented such that the server verifies whether the current user account has the necessary permissions for the requested functionality. Consequently, resource access should only be allowed after the server has performed a check on the user's privileges.
Include session and authorization controls to confirm that users are authenticated and authorized to access specific resources.


### Unrestricted file download
- CVSS Vector: (AV:N/AC:L/PR:N/UI:N/S:U/C:L/I:N/A:N)
#### Proof of Concept (PoC) 

During the Web Application Penetration Test, a vulnerability of unrestricted file download was identified in the target under analysis. This vulnerability allows an unauthenticated user to download documentation files that are normally accessible only after authentication.

To replicate the described scenario, it is sufficient to open the documentation file through a browser without logging into the application. This method demonstrates the application's failure to enforce authentication checks before allowing access to documentation files, thereby exposing sensitive information to unauthorized users.
#### Remediations
1. **API Privilege Checks**: Ensure that all API calls related to functionalities are designed to verify whether the user has the necessary privileges to perform the specific operation. This step involves validating the user's permissions before allowing access to any functionality, thereby preventing unauthorized actions.
    
2. **Authenticated File Downloads**: Restrict file downloads to authenticated users only. This means that the system should uniquely allow the downloading of files after successful authentication has been completed. By implementing this measure, unauthorized access to files, especially sensitive documentation, will be effectively prevented.
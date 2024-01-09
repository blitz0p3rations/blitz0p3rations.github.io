---
layout: post
title: 'Password spraying blacklist bypass'
tags:
  - web
hero: https://images.unsplash.com/photo-1541955193702-9ca03b1bb11a?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1470&q=80
overlay: red
---

Password spraying is a type of brute force attack where an attacker will use a small list of commonly used passwords, that may match the complexity policy of the domain. {: .lead} <!–-break-–>

# Password spraying blacklist bypass

In order to bypass common blacklist features that nowadays obstacle the attacks of a potential attacker, we need to use AWS IAM proxy so that every request made by us will be passed from different regions netblock.

Be sure to set up a user with these roles:
- AWSServiceRoleForOrganizations
- AWSServiceRoleForSupport
- AWSServiceRoleForTrustedAdvisor

After that, we can use [credmaster] (https://github.com/knavesec/CredMaster). 

It supports different modes, such as OWA, O365 and others, in this example, I performed the attack on the O365 of the company I work for in order to test the detection of the SOC.

To perform the attack, just insert your AWS access keys and prepare two wordlists, one with email addresses and one with a list of passwords (remember to consider the PSW policy of the domain).

- `python3 credmaster.py --plugin 0365 --access_key XYZ --secret_access_key XYZ -u emails.txt -p passwords.txt -t 10`

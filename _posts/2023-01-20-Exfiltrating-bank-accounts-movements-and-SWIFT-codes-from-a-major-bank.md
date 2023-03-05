---
layout: post
title: 'Exfiltrating bank accounts movements and SWIFT codes from a major bank'
tags:
  - Hacking

hero: https://images.unsplash.com/photo-1501167786227-4cba60f6d58f?ixlib=rb-4.0.3&ixid=MnwxMjA3fDB8MHxzZWFyY2h8Mnx8YmFua3xlbnwwfHwwfHw%3D&auto=format&fit=crop&w=400&q=60
overlay: green
---

Exfiltrating bank accounts movements and SWIFT codes from a major bank, I can not disclose the details of obvios reasons so a general explainantion is sufficient. {: .lead} <!–-break-–> 

## Exfiltrating bank accounts movements and SWIFT codes from a major bank

During an IOS penetration test engagement on a banking app via 
the api endpoint it was possible through a simple IDOR to enumerate all customers and 
their personal information, including critical data such as the SWIFT code and all movements made,
the impact of a vulnerability of this kind is critical, if the bank were exploited it would be in
trouble with the sanctions of the GDPR and with the damage to its image, moreover it exposes itself 
to the risk of hopefully targeted and authoritative phishing/vishing thanks to the amount of information obtained, 
I still don't know Regardless of how easy it was to cause them such potential damage, the error was the constructive
logic of the REST API endpoints.

## Extra making wire transfer
knowing the vulenrbailta I immediately set to work to make
transfers using the account of the other users, obviously for ethical reasons
I was not allowed to do so and for this very reason I asked the customer to open a second current account,
the request was denied because they they were too afraid of the potential results,
being  security of a major bank their position could be endangered, the request to make wire transfers 
is 100% vulnerable, after which confirmation via OTP comes into play but easily bypassable via targeted 
phishing, in one real scenario an APT would have devastated and destroyed them, 
setting fire to their ashes and their credibility, I was satisfied with their 
frightened faces but I wanted to continue to hurt them but unfortunately I don't have all this power hahaha.

<script>
    document.getElementsByTagName('body')[0].classList.add('glitch');
</script>

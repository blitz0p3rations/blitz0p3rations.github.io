---
layout: page
title: About
permalink: /about/
published: true
---

<div class="page" markdown="1">

{% capture page_subtitle %}
<img
    class="me"
    alt="{{ author.name }}"
    src="{{ site.author.photo | relative_url }}"
    srcset="{{ site.author.photo2x | relative_url }} 2x"
/>
{% endcapture %}

{% include page/title.html title=page.title subtitle=page_subtitle %}

Welcome to BLITZ 0p3rations ⚡!

"The credit belongs to the man who is actually in the arena, whose face is marred by dust and sweat and blood."

"The only way to deal with an unfree world is to become so absolutely free that your very existence is an act of rebellion."

I am a highly motivated 22-year-old Penetration Tester with a strong passion for physical red teaming operations and geopolitical intelligence. My career objective is to provide red team engagements that accurately emulate the tactics, techniques, and procedures of real threat actors. 

I aspire to reach a level of expertise where I can effectively emulate advanced persistent threats, similar to nation-state actors or well-funded groups. Currently, I find great satisfaction in the reconnaissance phase and obtaining initial access, mirroring the actions of adversaries who sell initial access on forums. My deep interest in intelligence and geopolitical analysis through open-source intelligence techniques drives me to continuously expand my knowledge and skillset.

This is a place where I share knowledge, tactical techniques and deal with various topics related to Intelligence, Cyberwar, Hacking and other stuffs that interest me.

Please note that the views and opinions expressed here are solely my own and do not represent the perspectives of any affiliations or the company I work for.

In the evening I enjoy:
- Learning new techniques and attacks (including studying for certifications).
- Emulate and replicate OSINT investigations in the Geopolitical field.
- Studying APT groups and State sponsored operations.
- Reading books.

The informations in this blog are provided for research and educational purposes only. BLITZ 0p3rations does not accept any liability in any form for any direct or indirect damages resulting from the use of or reliance on the information contained in this blog.


</div>

<script>
    document.getElementsByTagName('body')[0].classList.add('glitch');
</script>

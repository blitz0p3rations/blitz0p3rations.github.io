---
layout: post
title: 'Phishing Credentials and bypass 2FA'
tags:
 - social-engineering
hero: https://plus.unsplash.com/premium_photo-1673543763969-1d54002352d0?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1470&q=80
overlay: red
---

Phishing is a type of social engineering attack often used to steal user data, including login credentials and credit card numbers.

It occurs when an attacker, masquerading as a trusted entity, dupes a victim into opening an email, instant message, or text message. {: .lead} <!–-break-–>

Before setting up a phishing campaign, it's crucial to assess misconfigurations within the targeted domains. Exploiting these misconfigurations can make the phishing setup more effective. Here are some steps to consider:

### Domain SPF Validation:
To identify whether a domain is vulnerable to spoofing attacks, you can check its SPF (Sender Policy Framework) record. SPF helps prevent email spoofing by specifying authorized mail servers for sending emails on behalf of the domain. Follow these steps to check the domain's SPF record using MXToolbox's SPF Record Lookup:

1. Go to the MXToolbox website (https://mxtoolbox.com/).
2. In the search bar, enter "SPF Record Lookup" and press enter.
3. Enter the domain you want to check in the text field.
4. Click the "SPF Record Lookup" button.

The tool will retrieve and display the domain's SPF record. If the record includes a "v=spf1 -all" directive, the domain is protected against spoofing. If it's blank or includes a "v=spf1 ?all" directive, the domain may be vulnerable to spoofing.

### Gathering Subdomain List:
Compile a list of subdomains related to the target organization. Tools like Sublist3r, Subfinder, and Findomain can assist in subdomain enumeration. Identifying relevant subdomains can enhance the authenticity of your phishing attempt.

### Domain Purchase:
When acquiring a domain for phishing, consider the reputation of the domain provider. Reputable providers may have security measures against phishing domains. Opt for providers with a lower reputation to bypass such measures.

Choose a domain name thoughtfully:
- Avoid using typos or misspelt versions of the target organization's name, as they might be monitored.
- Instead, use generic names related to your phishing goal (e.g., "email.domain.com" for targeting email credentials).
- Expired domain names can help evade email reputation checks.

By examining domain misconfigurations and using appropriate domain-related strategies, you can enhance the success of your phishing campaigns while minimizing the chances of detection and mitigation.

Indeed, purchasing an expired domain can be an effective strategy for phishing campaigns, as these domains often come with a pre-existing reputation and may have been verified in the past. Expired domains can make it easier to bypass email reputation checks and other security measures. Here are the steps to consider when using an expired domain for your phishing campaign:

1. **Domain Research:** Visit websites like [ExpiredDomains.net](https://www.expireddomains.net/) to search for expired domains that fit your criteria. You can filter domains based on various parameters such as domain name, keywords, extension, and more.

2. **Domain Reputation:** Look for expired domains with a good reputation and a history of legitimate use. Check for domains that have not been used for malicious activities in the past.

3. **Domain History:** Investigate the history of the expired domain. Check for any signs of previous abuse or suspicious activity associated with the domain. Use tools like [Wayback Machine](https://archive.org/web/) to view the historical context of the domain.

4. **Purchase Domain:** Once you find a suitable expired domain, follow the process to purchase it. Some domain providers specialize in selling expired domains, and they often provide details about the domain's history and reputation.

5. **Domain Transition:** After acquiring the expired domain, make sure to transfer ownership to your account and update the domain's DNS settings to point to your hosting environment.

6. **Phishing Setup:** Set up your phishing content (e.g., landing pages, emails) on the acquired expired domain. Customize the content to match the context and target of your phishing campaign.

7. **Campaign Execution:** Launch your phishing campaign using the acquired expired domain. Monitor the campaign's performance and gather the desired information from your targets.

8. **Post-Campaign:** After the campaign is completed, you might choose to dispose of the expired domain or keep it for future campaigns. Be aware of the ethical and legal implications of using expired domains for malicious purposes.

Using an expired domain can provide you with an advantage in terms of domain reputation and avoiding email reputation checks. 

## Setting Up Evilginx2 on AWS

Setting up Evilginx2 on AWS involves creating an instance, configuring security groups, launching the instance, and then installing and using Evilginx2 for phishing purposes. Here's a step-by-step guide:

### Creating the Instance on AWS

1. **Create a Security Group:**
   - Go to AWS Management Console.
   - Navigate to EC2 > Network & Security > Security Groups.
   - Click on "Create security group."
   - Provide a name and description for the security group.

   ![](https://raw.githubusercontent.com/blitz0p3rations/blitz0p3rations.github.io/master/uploads/aws1.png)

2. **Launch an Instance:**
   - Navigate to EC2 > Instances.
   - Click on "Launch Instances."
   - Choose an Amazon Machine Image (AMI), e.g., Ubuntu.
   - Configure the instance details (name, instance type, etc.).
   - Configure the "Security Group" using the one you created earlier.

   ![](https://raw.githubusercontent.com/blitz0p3rations/blitz0p3rations.github.io/master/uploads/aws2.png)

1. **Generate and Download a Key Pair:**
   - In the "Key pair" section, click on "Create a new key pair."
   - Enter a name for the key pair.
   - Choose an encryption type and format.
   - Click "Create key pair" and download the .pem file.

2. **Launch the Instance:**
   - Review your instance details and configurations.
   - Click on "Launch instance."
   - Select the key pair you created and launch the instance.

3. **Set DNS Records for Your Domain:**
   - Buy a domain from a registrar or Route53.
   - Add "A" records to your domain's DNS settings, pointing to your AWS instance's public IP address.

### Accessing the Instance 

1. **SSH into the Instance:**
   - Open your terminal.
   - Use the SSH command provided in AWS to connect to your instance:
     `
     ssh -i path/to/your/key.pem ubuntu@your-instance-public-ip
     `
## Installing Evilginx2 on AWS: Configuration Steps

Setting up Evilginx2 on AWS involves installing, configuring, and customizing the tool for phishing purposes. Here's a step-by-step guide on how to do it:

1. **Install Golang and Download Evilginx2:**
   - Run the command `sudo apt install golang` to install Golang.
   - Download the Evilginx2 package. You can choose from these two recommended packages:
     - [Optiv's Evilginx2](https://github.com/optiv/evilginx2)
     - [aalex954's Evilginx2-tuned](https://github.com/aalex954/evilginx2-tuned)

2. **Compile Evilginx2:**
   - Navigate to the downloaded Evilginx2 package using the terminal.
   - Run `go build` to compile all the packages.

3. **Configure DNS Settings:**
   - Remove the existing resolv.conf file: `sudo rm /etc/resolv.conf`
   - Create a symbolic link to resolve.conf: `sudo ln -s /run/systemd/resolve/resolv.conf /etc/resolv.conf`

4. **Modify /etc/hosts:**
   - Add the internal IP address and your domain to the `/etc/hosts` file:
     `
     [internal IP] yourdomain.com
     `

5. **Stop Local DNS Server:**
   - Stop the local DNS server to avoid conflicts with Evilginx2:
     `
     sudo systemctl stop systemd-resolved.service
     `

6. **Edit Blacklist:**
   - Open the `blacklist.txt` file located in `~/.evilginx/`.
   - Add IPs from these sources:
     - [Custom Blacklist](https://github.com/aalex954/evilginx2-tuned/blob/master/Custom/blacklist.txt)
     - [Microsoft IP Tracker](https://github.com/aalex954/MSFT-IP-Tracker/releases/latest/download/msft_asn_ip_ranges.txt)

7. **Start Evilginx2:**
   - Run Evilginx2 with debugging enabled: `./evilginx2 -p /phishlets/ -debug`

8. **Configure Evilginx2:**
   - Set the domain, external IP, and redirect URL:
     `
     : config domain yourdomain.com
     : config ip XX.XX.XX.XXX
     : config redirect_url https://url.for.the.redirect
     `

9. **Configure Phishlets:**
   - Set up the o3652 phishlet to use the configured domain:
     `
     : phishlets hostname o365 yourdomain.com
     : phishlets enable o3652
     `

10. **Blacklist Setup:**
    - Add blacklist rules to prevent scanning: `: blacklist unauth`

11. **Create Lures:**
    - Create a lure using the command: `: lures create O3652`
    - Edit the lure's parameters, title, URL, image, and redirect URL as needed:
      `
      : lures edit 0 path /something/that/seems/legit
      : lures edit 0 redirect_url https://something.com
      `

12. **Generate Lure URL:**
    - Generate the URL for your lure: `: lures get-url 0`

## Scenario: Testing Evilginx2 and Token Theft

To test the correct functionality of Evilginx2 and understand the process of token theft, follow this scenario:

1. **Choose a Valid Account:**
   - To properly test Evilginx2, use a valid account that corresponds to the phishlet you are testing. For example, if you're testing the Office 365 phishlet, use an account that is associated with Office 365.

2. **Access the Phishing Site:**
   - Use the lure URL you generated in Evilginx2.
   - Enter the valid credentials of the chosen account (username and password).

3. **Evaluate Site Response:**
   - Depending on whether you used a valid account, the site's response will differ.
   - If the account is meant for the targeted service (e.g., Office 365), the site may prompt you for additional information, like a 2FA token.
   - If the account isn't relevant to the targeted service, the site might display an error or other feedback.

4. **Check Captured Sessions:**
   - Inside the Evilginx2 terminal, type `: sessions` to see captured sessions.
   - Examine the information that has been captured from the phishing attempts.

5. **Inspect Specific Session:**
   - To examine a specific captured session, use `: session session_ID`.

6. **Review Captured Credentials and Tokens:**
   - If Evilginx2 has successfully captured credentials and a 2FA token, you'll see relevant information in the captured session details.
   - The details might include the captured username, password, and token.

   ![](https://raw.githubusercontent.com/blitz0p3rations/blitz0p3rations.github.io/master/uploads/aws3.png)

7. **Use Captured Token:**
   - Install a cookie editor extension in your browser.
   - Navigate to the targeted service's login page (e.g., Office 365).
   - Click on the login form, and then open the cookie editor extension.
   - Import the captured token using the "Import JSON" feature of the cookie editor.
   - Reload the page.
   
   ![](https://raw.githubusercontent.com/blitz0p3rations/blitz0p3rations.github.io/master/uploads/aws4.png)
8. **Access the Compromised Account:**
   - If the process is successful, the compromised token will grant you access to the targeted service (e.g., Office 365) without requiring additional authentication steps.
   - This demonstrates how an attacker can gain unauthorized access using stolen tokens.


## Hiding Evilginx2 and Taking Precautions

When you're done using Evilginx2, it's crucial to take precautions to prevent unauthorized access and protect against potential security risks. Here's what you should do before and after using Evilginx2:

1. **Hiding the Phishlet:**
   - After you've finished your testing or engagement, use the following command to hide the phishlet you created:
     `
     : phishlets hide phishlet_name
     `
   - This action will remove the phishlet from being accessible, reducing the risk of accidental or unauthorized access.

2. **Enabling the Blacklist:**
   - If you temporarily disabled the blacklist for testing purposes, you should re-enable it to prevent scanning or unauthorized access:
     `
     : blacklist unauth
     `

3. **Secure Credentials and Data:**
   - Ensure that any captured credentials or data are properly managed and securely stored. Do not leave sensitive information exposed or accessible.

4. **Terminate the Instance (If Applicable):**
   - If you were using Evilginx2 on an AWS instance, consider terminating the instance when it's no longer needed. This will help minimize security risks and costs.

5. **Monitor for Suspicious Activity:**
   - Continuously monitor your environment for any signs of suspicious activity or unauthorized access, especially if you are running Evilginx2 on a live network.

## Setting Up WorkMail and Amazon SES for Phishing

To simulate phishing attacks, you need to set up Amazon WorkMail (for email services) and Amazon SES (Simple Email Service) on AWS. Here's a step-by-step guide on how to configure these services for phishing purposes:

1. **Create Organization in Amazon WorkMail:**
   - Click "Create Organization."
   - Choose "Existing Route53 Domain."
   - Proceed by selecting the hosted zone and Alias, then confirm.

2. **Wait for WorkMail Setup:**
   - Wait a few minutes for the WorkMail environment to be ready.
   - Access WorkMail and click "Domains"; Route53 configurations will be automatically set.

3. **Create User in Amazon WorkMail:**
   - Go back and click "Users," then "Create User."
   - Fill in username, first name, last name, and display name.
   - These details are essential for creating a convincing entity that the victim will interact with.

4. **Configure User and Mail:**
   - Proceed to configure the user's domain and email settings.
   - Set a complex password and the email address that will be displayed.

5. **Access User's Mail:**
   - Visit "Organization Settings" and click the link under "Web Application" to access the user's mail.

6. **Configure SES for SMTP Server:**
   - Search for "ses" and select "Simple Email Service."
   - Choose "Create Identity."
   - Create a new identity with these details:
     - Domain: Your domain
     - Easy DKIM: RSA_2048_BIT

7. **Update DNS Records:**
   - Remember to update Route53 settings to configure SPF1 and DMARC1.
   - Go to WorkMail, click "Domains," select the domain, and update all in Route53.

8. **Create SMTP Credentials in SES:**
   - Go to the SES page and create SMTP credentials.
   - Give a username for the SMTP server, e.g., "SES IRELAND."
   - Save the SMTP credentials securely.

9. **Future Engagements:**
   - For future engagements, you don't need to create a new organization in WorkMail.
   - Simply go to "Phishing," then "Domains," and add the new domain.
   - Configure the new domain in Route53 as a new hosted zone.


## Installing and Running Sneaky Gophish

To proceed with your phishing simulation, you can set up and run Sneaky Gophish. Here's how you can do it:

1. **Install Sneaky Gophish:**
   - Clone the Sneaky Gophish repository from [GitHub](https://github.com/puzzlepeaches/sneaky_gophish).

2. **Download Ready-to-Use Docker:**
   - The repository provides a Dockerfile for Sneaky Gophish.
   - Build the Docker image from the provided Dockerfile: `docker build -t gophish:hardened .`

3. **Create a Folder for Sneaky Gophish:**
   - Create a folder named `/sneaky_gophish` within the `/opt` directory.

4. **Run the Docker Container:**
   - Start the Docker container and map the container's ports to your localhost's ports:
     `
     docker run -d --name gophish_hardened -p 127.0.0.1:6666:3333 -p 127.0.0.1:8888:80 gophish:hardened
     `

5. **Verify Container and Images:**
   - Check the status of running Docker containers: `docker ps`
   - List the available Docker images: `docker images`

6. **Access Sneaky Gophish:**
   - Sneaky Gophish should now be accessible through your web browser at `http://PUBLIC_IP:8888`.

## Configuring GoPhish for Phishing Campaign

To configure GoPhish for your phishing campaign, follow these steps:

1. **Add New Domain in GoPhish:**
   - Within GoPhish, add the new domain that you configured earlier for your phishing simulation.

2. **Add DNS Records:**
   - Make sure to add the necessary DNS records for the new domain to ensure emails are delivered correctly.

3. **Configure Sending Profile:**
   - Under the "Sending Profiles" section, insert the SMTP credentials of your mail server. In this case, use the Amazon SES credentials.
   - Enter the email address that the victim will see as the sender.

4. **Navigate to Users and Groups:**
   - Import the list of email addresses gathered from your target organization or the emails provided by the client.

5. **Create Pretext Email Template:**
   - Create a pretext email template. Clone it with a style that mimics the target organization's newsletter or communication style to make it look authentic.

6. **Configure and Customize Template:**
   - Customize the pretext email template with content that is likely to lure the target. Use social engineering techniques to create an enticing email.

7. **Launch the Campaign:**
   - When you're ready to launch the campaign, create the phishing email using the pretext template.
   - Ensure to use the URL provided by Evilginx2 (lures) as the link in your phishing email.
   - Adjust the launch time based on your campaign strategy.

#### EXTRA: Setting Up a Caddy Redirector and Configuring Custom Firewall Rules for Security

These rules will ensure that only authorized connections are allowed to various components of the system.

Here's how the firewall rules will be set up:

1. **SSH Access:**
   - Only the IP address of the operator (`operator_ip`) will be allowed to log in over SSH using the provided SSH keys.

2. **SMTP Traffic:**
   - The GoPhish server will be restricted to sending SMTP traffic only to the phishing server, preventing unauthorized outbound email communication.

3. **DNS Access:**
   - The servers will have unrestricted access to any DNS server to ensure seamless domain name resolution.

4. **HTTP/HTTPS Access:**
   - Open access will be granted to any IP for HTTP and HTTPS ports. However, for improved security, consider narrowing down this access to specific IP ranges if available.

5. **GoPhish Admin Port:**
   - Only the `operator_ip` will be able to access the GoPhish admin port, which will be configured on a custom port.

Here's how the flow will work:

1. **Operator Login:**
   - The operator will log in to the GoPhish dashboard via HTTPS on the designated custom port.

2. **Email Sending:**
   - Once the phishing campaign is ready, the GoPhish server will utilize Amazon SES to send out the phishing emails to the intended recipients.

3. **Phishing Link:**
   - Upon recipient interaction, such as opening an email or clicking a link, they will be directed to a custom subdomain. This subdomain will host the fake login page designed for the phishing attack.

Here's an example of how you can set up a Caddy server to serve as a redirector for your phishing infrastructure:

1. **Install Caddy:**

   You can use Caddy's official website to get the installation script:

   `
   curl https://getcaddy.com | bash -s personal
   `

   This command will automatically download and install Caddy with the personal license.

2. **Create a Caddy Configuration File:**

   Create a Caddy configuration file, typically named `Caddyfile`, in the directory where you have Caddy installed. You can use a text editor to create and edit this file.

   `
   sudo nano /etc/caddy/Caddyfile
   `

3. **Add Your Redirector Configuration:**

   Add the following lines to your `Caddyfile`, adjusting the domain and IP address:

   `
   your-subdomain.your-domain.com {
       reverse_proxy http://evilnginx-server-ip
   }
   `
   
   Replace `your-subdomain.your-domain.com` with the custom subdomain to use for your phishing. This configuration will instruct Caddy to act as a reverse proxy, redirecting incoming requests to the `evilnginx-server-ip` where the fake login page is hosted.

4. **Save and Close the File:**

   After making the necessary changes, save and close the file. In Nano, you can do this by pressing `Ctrl + O` to save and `Ctrl + X` to exit.

5. **Restart Caddy:**

   Restart Caddy to apply the new configuration:

   `
   sudo systemctl restart caddy
   `

6. **Check Caddy Status:**

   You can check the status of Caddy to make sure it's running without errors:

   `
   sudo systemctl status caddy
   `

   If everything is configured correctly, you should see that Caddy is active and running.

Please note that this is a simplified example, and you may need to adapt it to your specific setup and requirements. 
#### Creating Fake Alerts in Phishing Emails

Administrators of Microsoft 365 often implement rules to flag emails from external sources, aiming to highlight potential phishing attempts. This practice helps users identify potentially risky emails. 

For instance, we can strategically use a negative margin to position our desired alert on top of the injected alert, effectively covering it up, giving the appearance that the email originated from an internal source without any alerts or warnings.

This manipulation showcases the challenge of relying solely on visual indicators to determine the legitimacy of an email. It's a reminder that attackers can skillfully manipulate elements to deceive recipients and make phishing emails appear more convincing. As a result, user education, vigilant security practices, and multi-layered security solutions are crucial to mitigating the risks posed by such tactics.

### Other ways for delivering the phishing link

Methods involve leveraging legitimate platforms and notifications to deliver malicious content, as you mentioned with Google Docs notifications. Here are a few other ways attackers might use to deliver phishing links:

1. **Collaboration Platforms:** Attackers might send phishing links through collaboration platforms like Microsoft Teams, Slack, or other workplace communication tools. These platforms often send notifications to users when they receive messages or invitations, creating a sense of urgency that attackers exploit.

2. **Cloud Storage Services:** Attackers could use cloud storage services like Dropbox, OneDrive, or Google Drive to host phishing files and share them with victims. The platforms' notification systems might entice users to click on links under the guise of accessing shared documents.

3. **Social Media:** Phishing links can be distributed through social media platforms, direct messages, and comments. Cybercriminals can impersonate trusted contacts, enticing recipients to click on links that lead to malicious sites.

4. **Instant Messaging Apps:** Attackers could send phishing links through messaging apps like WhatsApp, Facebook Messenger, or Telegram. These apps often have push notifications that encourage users to engage with messages.

5. **Browser Notifications:** Some malicious websites may request permission to send browser notifications. Attackers can abuse this feature to push phishing links directly to users' devices.

6. **Email Forwarding:** Attackers might compromise a victim's email account and use it to forward phishing emails to their contacts. The emails appear to come from a familiar source, increasing the chances of recipients clicking on the links.

7. **QR Codes:** Phishers could distribute QR codes in physical locations or online. Scanning the code with a mobile device could lead to a phishing site.

8. **Voice and SMS:** Voice calls or SMS messages containing phishing links could be used to target mobile users.

### Domain Categorization and Anti-Spam Domain Checker

If you've recently acquired a domain and are looking to categorize it or assess its reputation, there are various online tools available to help you with this task. These tools can help you determine whether a domain has been categorized, potentially typo-squatted, involved in URL smuggling, and more. Here are some tools you can use:

- [**MultiRBL**](https://multirbl.valli.org/): MultiRBL checks if a domain is listed on multiple DNS blacklists. This can help you identify if a domain has been associated with spam or malicious activities.

- [**Barracuda**](https://www.barracudacentral.org/report/website-category/): Barracuda Central offers a website category check that helps you determine the categorization of a domain, helping you understand if it has been classified as potentially malicious.

- [**Bluecoat**](https://sitereview.bluecoat.com/sitereview.jsp): Bluecoat's Site Review allows you to check a domain's reputation and categorization, helping you assess its safety and legitimacy.

- [**BrightCloud**](https://www.brightcloud.com/tools/url-ip-lookup.php): BrightCloud provides a URL/IP lookup tool that helps you check the categorization and reputation of a domain.

- [**Forcepoint**](https://csi.forcepoint.com/): Forcepoint's Security Labs provides information about website categorization and reputation.

- [**Fortinet**](http://url.fortinet.net/): Fortinet's URL Lookup tool helps you determine the categorization of a domain and its potential risks.

- [**Juniper**](http://mtas.surfcontrol.com/mtas/JuniperTest-a-Site.php): Juniper's Site Review tool helps you understand a domain's categorization and potential risks.

- [**McAfee**](https://www.trustedsource.org/?p=mcafee): McAfee's TrustedSource allows you to check a domain's reputation and categorization.

- [**Palo Alto**](https://urlfiltering.paloaltonetworks.com/): Palo Alto's URL Filtering tool helps you assess the categorization of a domain and its potential risks.

- [**SonicWall**](http://cfssupport.sonicwall.com/Support/web/eng/newui/viewRating.jsp): SonicWall's CFS Support provides information about website categorization.

- [**TitanHQ**](https://tools.zvelo.com/): TitanHQ's URL/IP Lookup tool helps you determine a domain's categorization and reputation.

- [**Trend Micro**](https://global.sitesafety.trendmicro.com/): Trend Micro's Site Safety Center helps you assess the safety and categorization of a domain.

- [**WatchGuard**](http://mtas.surfcontrol.com/mtas/WatchGuardTest-a-Site.php): WatchGuard's Site Review tool helps you understand a domain's categorization.


### Email Anti-Spam Score Check

To evaluate the potential spam score of your email content and improve its deliverability, you can use various online tools. One such tool is **Mail Tester**:

- [**Mail Tester**](https://www.mail-tester.com/): Mail Tester allows you to send an email to a unique address they provide. They then analyze the content, headers, and other factors to assess the potential spam score of your email. You'll receive a detailed report with suggestions on how to improve your email's deliverability and reduce its chances of being flagged as spam.


## Email Reporting
Email reporting is a valuable tool for customers to monitor the effectiveness of their phishing campaigns and assess their overall security posture. These reports provide insights into recipient engagement and the impact of the campaign. Here are the key metrics typically included in email reporting:

1. **Number of Emails Sent:** This metric represents the total number of phishing emails that were sent to recipients as part of the campaign. It provides a baseline for understanding the campaign's reach.

2. **Number of Emails Opened:** The number of emails that were opened by recipients. This metric indicates the initial level of engagement with the phishing email.

3. **Number of Clicks:** This metric quantifies how many recipients clicked on the malicious link or interacted with the content in the email. It highlights how many individuals were potentially exposed to the threat.

4. **Conversion Rate:** The conversion rate calculates the percentage of recipients who completed the desired action, such as clicking on a link, providing sensitive information, or downloading a file. This metric helps evaluate the campaign's success in achieving its objectives.

5. **Geographical Distribution:** Geographical data provides insights into where the phishing emails were opened and clicked. This information can help identify regions that are more susceptible to phishing attacks and guide targeted security efforts.

6. **Time-based Metrics:** Reporting can also include time-based metrics, such as when most emails were opened or clicked. This data can reveal patterns in recipient behaviour and inform the timing of future campaigns.

7. **Engagement Rate:** The engagement rate combines the number of emails opened and the number of clicks to measure how actively recipients engaged with the phishing content.

8. **Email Client and Device Analysis:** Information about the email clients and devices used by recipients to open the emails can provide insights into potential vulnerabilities and attack vectors.

9. **Top Targeted Users:** Reporting can highlight the users who interacted most with the phishing email, helping organizations focus on additional training or precautions for these individuals.

10. **Response Time:** This metric indicates how quickly recipients engaged with the phishing email after receiving it. It can provide insights into the effectiveness of the email's subject line and content.


## Conclusion

In conclusion, modern phishing vectors have evolved significantly to capitalize on human vulnerabilities and technological advancements. Cybercriminals leverage sophisticated techniques to deceive individuals and organizations, making it crucial for individuals and businesses to stay vigilant and implement robust cybersecurity measures.

Some key takeaways from modern phishing vectors include:

1. **Social Engineering:** Phishing attacks heavily rely on social engineering tactics, exploiting human emotions, curiosity, and trust to manipulate victims into taking actions that compromise their security.

2. **Spear Phishing:** Targeted attacks, known as spear phishing, tailor messages to specific individuals using personal information, making them more convincing and increasing the likelihood of success.

3. **Credential Harvesting:** Phishers often seek usernames and passwords to gain unauthorized access. This information is then used for various malicious purposes, including identity theft and unauthorized account access.

4. **Business Email Compromise (BEC):** BEC attacks target employees with access to financial systems or sensitive information. Attackers impersonate executives, requesting fund transfers or sensitive data.

5. **Malware Delivery:** Phishing emails can contain malicious attachments or links that lead to malware-infested websites. Once opened or clicked, malware can compromise systems, steal data, or enable unauthorized access.

6. **URL Manipulation:** Phishers use URL manipulation techniques to mask malicious URLs with seemingly legitimate ones, increasing the likelihood of victims clicking on them.

7. **Brand Impersonation:** Attackers imitate trusted brands or services to deceive recipients into disclosing sensitive information or performing actions that compromise security.

8. **Mobile Phishing:** As mobile device usage grows, attackers increasingly target mobile users with SMS-based phishing (smishing) and malicious apps.

9. **Evading Security Measures:** Attackers constantly adapt to bypass security measures, using encryption, obfuscation, and evasion tactics to evade detection.

To defend against modern phishing vectors:

- **Education:** Regularly educate individuals about phishing risks, how to identify suspicious emails, and what steps to take if they encounter one.

- **Multi-Factor Authentication (MFA):** Implement MFA wherever possible to add an extra layer of security even if credentials are compromised.

- **Email Filtering:** Use advanced email filtering solutions that can identify and block phishing emails before they reach recipients' inboxes.

- **Security Updates:** Keep systems, software, and devices updated to patch vulnerabilities that attackers could exploit.

- **URL Analysis:** Use tools that analyze URLs for potential threats before clicking on them.

- **Employee Training:** Conduct ongoing cybersecurity training for employees to enhance their ability to recognize and report phishing attempts.

- **Strong Passwords:** Encourage the use of strong, unique passwords and discourage password sharing.

- **Domain Monitoring:** Monitor domain registrations and usage to prevent attackers from creating domains that impersonate your brand.

Modern phishing attacks require a multi-faceted approach, combining technological defences, user education, and proactive threat detection. Staying informed about the latest phishing trends and continuously adapting security practices is essential to effectively mitigate the risks posed by these evolving attack vectors. 


### References
1. https://thomfre.dev/post/2020/fake-microsoft-alerts/
2. https://www.optiv.com/insights/source-zero/blog/spear-phishing-modern-platforms
3. https://breakdev.org/evilginx-2-next-generation-of-phishing-2fa-tokens/
4. https://www.techrepublic.com/article/how-to-run-a-phishing-attack-simulation-with-gophish/
5. https://resources.hacware.com/gophish-demo/
6. https://medium.com/airwalk/practical-phishing-with-gophish-7dd384ad1840
7. https://www.youtube.com/watch?v=S6S5JF6Gou0
8. https://mikebosland.com/hello-world/
9. https://www.sprocketsecurity.com/resources/never-stop-frontin-how-to-quickly-setup-a-redirector-and-transparent-reverse-proxy

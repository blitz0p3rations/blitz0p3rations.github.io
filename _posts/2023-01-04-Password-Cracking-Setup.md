---
layout: post
title: 'Password Cracking setup'
tags:
 - infra
hero: https://plus.unsplash.com/premium_photo-1673543763969-1d54002352d0?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1470&q=80
overlay: red
---

Using cloud-rented GPUs (Graphics Processing Units) to perform highly resource-intensive tasks offers cost savings, scalability, accessibility, and reduced operational overhead. {: .lead} <!–-break-–>

## VAST AI connection and istance setup
![](https://raw.githubusercontent.com/blitz0p3rations/blitz0p3rations.github.io/master/uploads/img0.png)

The initial step involves setting up an account on https://cloud.vast.ai/. After you create your account, you can go ahead and log in and add credit to your account using Stripe as the chosen payment method.

Subsequently, on your local machine, generate an SSH key using the command:
`ssh-keygen -t rsa`
To ensure the secret key is actively loaded, employ the following commands:
`ssh-add; ssh-add -l`

Following this, copy the contents of the freshly generated public key and insert it into the designated public key section within the VAST AI platform.

Moving forward, the configuration of the instance must be addressed. It's imperative to allocate an ample amount of storage space, as some of the wordlists can be sizeable.

![](https://raw.githubusercontent.com/blitz0p3rations/blitz0p3rations.github.io/master/uploads/vast1.png)

Proceeding to the configuration step, select the provided Docker image that already incorporates fundamental tools.

![](https://raw.githubusercontent.com/blitz0p3rations/blitz0p3rations.github.io/master/uploads/vast2.png)

With these settings finalized, the subsequent task involves the selection of the appropriate GPU for rental. This choice should be based on a balance between hourly cost and processing capability. The reliable and capable RTX 4090 is often a solid choice for this purpose.

![](https://raw.githubusercontent.com/blitz0p3rations/blitz0p3rations.github.io/master/uploads/vast3.png)

Subsequent to making your choice, patiently await the instance's readiness, and upon confirmation, click the "connect" option to obtain the SSH command that facilitates the connection to the virtual machine.
![](https://raw.githubusercontent.com/blitz0p3rations/blitz0p3rations.github.io/master/uploads/vast4.png)


Upon successful connection, you'll find essential tools for password cracking, including Hashcat. Additionally, the presence of tmux allows for the efficient division of terminal sessions.

Feel free to proceed with your resource-intensive tasks armed with the tools and computing power at your disposal. This process, outlined step by step, ensures the effective setup and utilization of cloud-based GPUs for your computational needs.
## Password Cracking with Hashcat
### Identifying the Appropriate Mode

To pinpoint the suitable mode for your hash, you can utilize the following command to extract relevant information from the hashcat help documentation:

`hashcat --help | grep -i ntlm`

This command will search for instances of "ntlm" within the hashcat help output, aiding you in identifying the correct mode.

Afterwards, inspect your hash and compare it against the provided examples within the help output. This comparison will allow you to accurately ascertain the mode that corresponds to your hash. By following this process, you will be equipped with the knowledge needed to proceed with cracking the hash using the appropriate hashcat mode.

### Fundamental Syntax

The foundational syntax for executing hashcat commands follows this structure:

`hashcat -m X -a O -d 2 <hash(stdin/file)> <wordlist>`

Here's a breakdown of the elements involved:

- `-m X`: This flag designates the hash mode (`X` represents the specific hash mode number). The correct hash mode number should correspond to the type of hash you are attempting to crack (e.g., MD5, SHA-1, etc.).

- `-a O`: This flag determines the attack mode (`O` represents the specific attack mode number). Various attack modes are available, such as dictionary attacks, brute-force attacks, and more.

- `-d 2`: This flag indicates the device (GPU) to be used for the task. `2` represents the specific device ID. This is particularly useful when you have multiple GPUs and want to assign a specific one.

- `<hash(stdin/file)>`: Replace this placeholder with the actual hash you intend to crack. This hash can be provided either via standard input (stdin) or by specifying a hash file.

- `<wordlist>`: Replace this with the path to the wordlist you wish to use for the cracking attempt. The wordlist contains the potential passwords that hashcat will try against the hash.

The provided syntax gives you a basic structure for crafting your hashcat command. Make sure to replace the placeholders with the appropriate values specific to your situation.

### Leveraging Rules for Enhanced Success

Utilizing rules in hashcat can significantly enhance your success rate by considering common password substitutions and patterns. Hashcat offers multiple default rule sets to assist in this process. Here's how you can incorporate rules into your hashcat command:

`<hash> <wordlist> -r <rules>`
` <hash> <wordlist> -r <rules> -r <rules>`

In this structure:

- `<hash>`: Replace this with the hash you aim to crack.
- `<wordlist>`: Substitute this with the path to your wordlist file.
- `-r <rules>`: Use this flag to specify a rule file to apply during the cracking process. You can include multiple `-r <rules>` flags to apply multiple rule files.

The effectiveness of rules can significantly influence your outcomes. One notable collection of rules is the [One Rule To Rule Them All](https://github.com/stealthsploit/OneRuleToRuleThemStill) rule set. This rule set is a culmination of the top 25% of the best-performing rules, combined into a custom rule.

Employing these rules in your hashcat commands can improve your chances of successfully cracking passwords that feature common substitutions and patterns. By integrating rules, you're harnessing additional strategies to decipher passwords from the given hash, contributing to a more comprehensive approach to password cracking.

### Brute Force Attacks: Tailoring for Efficiency

Brute force attacks can be particularly effective for cracking passwords, especially when the password length is known. However, there are strategies to optimize the brute force process. Let's explore some techniques using hashcat:

1. **Using Incremental Mode with a Minimum Length:**
   Hashcat's `--increment` flag allows it to start guessing passwords with just one character and incrementally increase the length until it successfully cracks the hash. To save time and restrict the initial character count, you can use `--increment-min=5`.
   
   `hashcat -m X <hash> -a 3 ?a?a?a?a?a?a?a?a --increment`

   !![](https://raw.githubusercontent.com/blitz0p3rations/blitz0p3rations.github.io/master/uploads/vast5.png)

2. **Appending Known Characters:**
   If you have knowledge of specific characters that frequently appear at the end of passwords (e.g., "123!"), you can optimize the brute force process by appending these characters to your character set. This narrows down the possibilities for the preceding characters.

   `hashcat -m 1000 -a 3 18803562CC19899140CF4C91EA6A4F2B ?l?l?l?l?l?l?l?l123!`

   In this example, `?l` represents lowercase letters, and `?a` represents all characters. The provided hash is targeted with the specified character set and the known ending characters.


By employing these techniques, you can refine your brute force approach, optimizing your chances of successfully cracking passwords while making the process more efficient and effective.

### Mask Attacks: Efficient Customization

Mask attacks are a subset of brute force attacks that are particularly useful when you have partial knowledge about the password's elements. These attacks are especially effective for passwords containing mixed alphanumeric characters, where you know specific positions or patterns within the password.

Here's how to use mask attacks effectively with hashcat:

1. **Basic Mask Attack:**
   You can create a mask that specifies the position and character types using placeholders like `?u` for uppercase letters, `?l` for lowercase letters, and `?d` for digits.

   `hashcat -a 3 -m X <hash> ?u?l?l?l?l?l?l?d`

   This command applies a mask attack on the provided hash. It uses uppercase letters for the first position and lowercase letters for the next six positions, followed by a digit.

2. **Advanced Mask Attack with Positional Charset:**
   You can further customize your mask attack by assigning specific character sets to certain positions using `-1`, `-2`, `-3`, and so on.

   `hashcat -a 3 -m X <hash> -1 ?u?l -2 ?d?s P@sswr0rd?1?1?1?2`

   In this example, `-1 ?u?l` assigns the first character position to only test mixed case alphabetic characters, and `-2 ?d?s` assigns the second character position to only test numbers and special characters. The remaining part of the 
   mask (`P@sswr0rd?1?1?1?2`) is straightforward.

   This approach significantly narrows down the possibilities, increasing the efficiency of the attack.


By mastering mask attacks, you gain the ability to strategically target password patterns and increase your chances of successful password cracking, all while optimizing the use of computational resources.

### Hybrid Attacks: Combining Strategies

Hybrid attacks combine the strengths of both wordlist attacks and mask attacks, allowing you to leverage known patterns or partial information while benefiting from the diversity of a wordlist. Here's how you can effectively use hybrid attacks with hashcat:

1. **Wordlist + Mask Hybrid Attack:**
   You can combine a wordlist with a mask to create a potent hybrid attack. This approach targets the provided hash with the wordlist entries followed by a mask.

   `hashcat -a 6 -m X <hash> <wordlist> -1 ?d?s ?u?u?1?1`

   In this example, the `-a 6` flag indicates a hybrid attack mode, and `-1 ?d?s` specifies that the first position should include digits and special characters. The mask `?u?u?1?1` is then applied, targeting uppercase letters and digits in subsequent positions.

2. **Mask + Wordlist Hybrid Attack:**
   Alternatively, you can use a mask followed by a wordlist. This method first tests the mask pattern and then supplements it with wordlist entries.

   `hashcat -a 7 -m X <hash> ?d?d?d <wordlist>`

   Here, the `-a 7` flag designates the hybrid attack mode, and the mask `?d?d?d` is tested initially, followed by the wordlist entries.

  By blending the characteristics of both wordlist and mask attacks, hybrid attacks offer a versatile approach that considers known patterns and extensive wordlist coverage. This versatility increases your likelihood of successfully 
  cracking passwords by optimizing your search strategy. 


### Combinator Attacks: Expanding Wordlists

Combinator attacks provide a way to expand wordlists by combining entries from two separate wordlists, potentially uncovering additional password variations. Here's how you can employ combinator attacks with hashcat:

1. **Expanding Wordlists with Hashcat Utilities:**
   To facilitate combinator attacks, you can utilize the [hashcat-utils](https://github.com/hashcat/hashcat-utils) repository. This repository offers tools for creating combined wordlists. For instance, if you need more words for your wordlist, you can follow these steps:

   - Download or clone the hashcat-utils repository.
   - Use the `combinator` tool to combine entries from two wordlists:

     `./combinator wordlist.txt wordlist.txt > wordlist-combined`

   This process generates a new wordlist called `wordlist-combined` containing combinations of words from the input wordlist.

2. **Creating Delimiters for Combinator:**
   For effective combinator attacks, you might need to create delimiters. These delimiters separate the words and improve the effectiveness of the attack. You can achieve this using tools like `awk`:

   `awk '{print $0" "}' wordlist.txt > wordlist-space`

   Then, use the `combinator.bin` tool from hashcat-utils to combine entries from the two prepared wordlists:

   `./combinator.bin wordlist-space wordlist.txt > wordlist-combined`

3. **Applying Combinator Rules:**
   Additionally, combinator attacks can involve applying rules to each word from one or both dictionaries. You can achieve this using the `-j` (rule for left dictionary) and `-k` (rule for right dictionary) flags:

   `hashcat -a 1 -m X <hash> -j <rule_for_left> -k <rule_for_right>`

   This approach enhances the combinator attack by introducing rules that modify the words in the dictionaries before they are combined.

By utilizing combinator attacks and hashcat utilities, you can significantly broaden your approach to password cracking. The combination of wordlists and rule-based modifications increases your chances of successfully cracking passwords that might have otherwise remained hidden.

## Profiling the Target and Wordlist Permutation

Profiling your target organization is a crucial preliminary step in any penetration testing (PT) or password cracking endeavour. Understanding your target's history, products, and other relevant elements can significantly refine your attack strategies. Here's how to conduct profiling and create custom wordlists:

1. **Profile the Target Organization:**
   * Navigate their website and note down important details such as product names, historical events, abbreviations, and significant dates.
   * Identify subdomain names, which can help you identify service name patterns.
   * For internal penetration tests, gather information about Service Principal Names (SPNs), as passwords might include this information.

2. **Useful Tools:**
   - [DNSDumpster](https://dnsdumpster.com/): Helps in discovering subdomains.
   - [CUPP](https://github.com/Mebus/cupp): Creates custom wordlists based on target information.
   - [CeWL](https://github.com/digininja/CeWL): Generates custom wordlists from websites.
   - [WeakPass](https://weakpass.com/generate): Offers custom wordlist generation.
   - [WeakPass Wordlist](https://weakpass.com/wordlist): Provides public wordlists.

3. **Approaches to Wordlist Creation:**
   - **Custom Wordlist:** Create a wordlist based on target-specific information and incorporate patterns, historical elements, and abbreviations. Apply rules like [OneRuleToRuleThemAll](https://github.com/stealthsploit/OneRuleToRuleThemStill) or other patterns you've discovered.
   - **Public Wordlist:** Utilize publicly available wordlists that contain leaked passwords.
   - **Mix and Match:** Combine your custom wordlist with public wordlists to cover a broader range of possibilities.

By profiling your target and constructing custom wordlists based on their history, products, and patterns, you can create highly targeted password cracking strategies. This approach significantly improves your chances of successfully cracking passwords, especially when combined with rule-based permutations.

## Full Scenario: Cracking SPN Hash and Custom Wordlists

In a specific engagement, your team obtained a ticket through a Kerberoasting attack on a Service Principal Name (SPN) within the target customer's environment. Cracking these obtained hashes is essential to potentially uncover additional attack paths and reveal further security vulnerabilities.

The hash you obtained looks like this:
`$krb5tgs$23$*MSSQLSvc$CUSTOMERDOMAIN.LOCAL$MSSQLSvc/serversap00.CUSTOMERDOMAIN.local@CUSTOMERDOMAIN.local`
`*$blahblahblah$otherblahotherblahtoherblah...`

By analyzing the obtained SPN ticket, you can identify keywords that might prove valuable for conducting a more focused attack, such as "SAP," "SQL," "server," domain name, and others.

Here's a strategy for generating a custom wordlist using classic words and terminators:

`./psudohash.py -w domain,customer,sql,sap,server,qwerty,password --common-paddings-after -y 2020-2023`

After generating the custom wordlist, you can use hashcat to attempt to crack the hash:

`hashcat -m 13100 -a 0 ../hash.txt customwordlist.txt`

Additionally, consider employing an approach where you brute-force characters one by one, starting with a minimum of 8 characters as specified by the dumped password policy. For instance, you can attempt to brute-force characters with a known pattern at the end, such as **1914!!**:

`hashcat -m 13100 -a 3 ../2.hash '?u?h?l?l?h?l?l?h1914!!' -i --increment-min=8`

For information gathering, manual research and utilizing tools like DNS Dumpster or CeWL can be helpful:

`cewl -d 2 -m 5 -w output.txt https://target.com`

If you happen to have the hash of a specific user, like "Carlos Surname," you can search for this user's profiles on social media and create a customized wordlist using CUPP:

`python3 cupp.py`

It's important to remember that when using generated and public wordlists, it's beneficial to apply different rules if the initial attempts fail. Incorporating public rules such as "OneRuleToRuleThemAll" or creating custom rules can greatly enhance your chances of successfully cracking the passwords. By employing a combination of these strategies, you'll be well-equipped to efficiently and effectively crack SPN hashes and uncover potential attack paths.

## Conclusion
In conclusion, the process of password cracking is a complex and multifaceted endeavor. While not every password can be cracked due to factors like length, complexity, and hashing algorithms, significant success can still be achieved in the modern landscape. This success is largely attributed to the persistence of users and organizations using passwords that lack entropy, are easily guessable, or adhere to common patterns.


### Refernces
1. https://infinitelogins.com/2020/04/24/transferring-files-via-base64/
2. https://weakpass.com/
3. https://in.security/technical-training/password-cracking/
4. https://vast.ai/
5. https://github.com/stealthsploit/OneRuleToRuleThemStill
6. https://contest-2010.korelogic.com/rules.html

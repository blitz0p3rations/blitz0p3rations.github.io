---
layout: post
title: 'Wi-Fi Segregation Test for Hotels,Airports and Organizations'
tags:
 - wireless
hero: https://images.unsplash.com/photo-1583602621722-cbd1130b210b?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1470&q=80
overlay: red
---

These assessments aim to uncover misconfigurations and vulnerabilities that could compromise network segmentation and allow attackers to move laterally between networks.  {: .lead} <!–-break-–>

## Firewall Misconfigurations and Network Vulnerabilities Assessment

Misconfigured firewall rules or vulnerabilities in devices that span multiple network segments can provide attackers with an opportunity to leverage cross-network attacks between sections of the network that are intended to be isolated. Depending on the network architecture in use, this could pose a significant risk to an organization, potentially allowing attackers to pivot between trusted and untrusted networks.

### Requirements
There isn't a significant difference in terms of execution between white-box and black-box modes. In white-box, you might have the ability to be more precise and targeted, avoiding the discovery phase and thus reducing the required time. 

#### White-box Assessment

- Architectural diagram of the network (or networks) under assessment.
- List of IP ranges used within each network to be tested. Include a pingable device within each network as a reference point for testing purposes.
- Separate access to each network under examination.

#### Black-box Assessment

- None, attackers must figure out by themself.

### Test Types

#### Active Firewall Rule Assessment

This test involves an automatic scanning of ports from each network to all other adjacent networks against a target host installed in an adjacent network. The network device is configured to listen on all TCP and UDP ports. Any network port reported as "open" during the port scan indicates that segregation is not effective, and the test identifies the network ports allowed through the firewall or VLAN.

#### Network Traffic Capture

In this exercise, network traffic is passively captured from all networks to identify if broadcast or multicast network traffic is allowed to pass through the firewall. If firewalls are not configured to provide complete network isolation, broadcast traffic may pass through, potentially allowing attackers to gather useful information such as host names or IP address ranges. The presence of network protocols (such as Cisco Discovery Protocol or VLAN Trunking Protocol) that might assist attackers in identifying VLAN-related information will also be verified.

#### VLAN Hopping

An attempt is made to bypass VLAN segregation in network switches through a process known as "VLAN Hopping." Although VLAN hopping is rarely possible today, incorrect configurations (such as allowing trunk negotiation) in network switches could enable an attacker to access other VLANs they shouldn't have access to. This could allow the attacker to access other network subnets, potentially exploiting vulnerable hosts and advancing their attack.

#### Vulnerabilities in Multi-Homed Devices

Multi-homed devices have multiple network interfaces, often connected between adjacent networks. If vulnerabilities are present in these devices (such as port forwarding), an attacker can use the multi-homed device as a router and access hosts on other adjacent networks. Specific tests will be conducted to identify potentially multi-homed hosts and to discover any exploitable vulnerabilities in them.

## Active Firewall Rule Assessment

1. **Connect to the Network:**
   - Establish a connection to the network under assessment.

2. **Analyze Network Settings and DNS:**
   - Obtain network configuration information from your physical machine and associate it with the relevant virtual machine.
   - Identify the DHCP server's placement.
   - Determine the size of the netblock and whether it's a segregated network with limited hosts or a complete /24 subnet.
   - Identify the DNS server, its origin (internal or external), and its relation to the network.
   - Recognize the default Gateway (GW) and differentiate it from DNS or DHCP servers.
`ipconfig /all`



3. **Host Discovery:**
   - Create an Excel spreadsheet to list potential IP addresses and mark their status as up or down.
   - Repeat this process for each network to be analyzed, creating a separate tab for each network in Excel.
   - Initiate ICMP requests to detect active hosts in the following private IP ranges:
     - 10.0.0.0 - 10.255.255.255 (10/8 prefix)
     - 172.16.0.0 - 172.31.255.255 (172.16/12 prefix)
     - 192.168.0.0 - 192.168.255.255 (192.168/16 prefix)
   - If certain networks block ICMP requests, move directly to port discovery.

**Private IP Ranges**
 ` 10.0.0.0 - 10.255.255.255 (10/8 prefix)`
 ` 172.16.0.0 - 172.31.255.255 (172.16/12 prefix)`
 ` 192.168.0.0 - 192.168.255.255 (192.168/16 prefix)`

 **Scanning 172.16.0.0/12 network for live hosts**
`fping --ipv4 -b 4 -r 1 -t 250 --alive -A -g 172.16.0.0/12 > 172.16.0.0_12_up`

**Scanning 10.0.0.0/8 network for live hosts**
**Note: This range is quite large and may require significant time/resources**
`fping --ipv4 -b 4 -r 1 -t 250 --alive -A -g 10.0.0.0/8 > 10.0.0.0_8`

**Scanning 192.168.0.0/16 network for live hosts**
`fping --ipv4 -b 4 -r 1 -t 250 --alive -A -g 192.168.0.0/16 > 192.168.0.0_16_up`

**Scanning 10.10.0.0/16 network for live hosts**
`fping --ipv4 -b 4 -r 1 -t 250 --alive -A -g 10.10.0.0/16 > 10.10.0.0_16`


These commands are using the `fping` tool to send ICMP echo requests (ping) to IP addresses within the specified address ranges. The `-g` flag specifies the IP range, and the `--alive` flag indicates that only live hosts should be listed. The results are being redirected to files with names indicating the range being scanned and the status of the hosts.

Please note that scanning large IP ranges, especially those like 10.0.0.0/8, can take a significant amount of time and generate a lot of network traffic, SOC or MDR must notice it so it's also an interesting test. 
4. **Port Enumeration:**
   - Run focused scans on potentially interesting ports.
   - Perform more accurate scans on ports associated with services you've already encountered.
   - Initiate fping scans for large IP ranges if feasible.
   - Common port ranges: 80, 443, 53, 445, 3389, 22, 25, 110, 139, 143.

   1. Port Scanning with Specific Ports:
   `80,443,53,445,3389`
   This is a list of specific port numbers you want to scan for on the target hosts. These ports are commonly associated with services like HTTP (80), HTTPS (443), DNS (53), SMB (445), and Remote Desktop Protocol (3389).

   2. Expanded Port Scanning:
   `80,23,443,21,22,25,3389,110,445,139,143,53
   80,23,443,21,22,25,3389,110,445,139,143,53,135,3306,8080,1723,111,995,993,
   5900`
   These are more comprehensive lists of port numbers for scanning. It covers a wider range of common ports, including those for HTTP (80), Telnet (23), FTP (21), SSH (22), SMTP (25), POP3 (110), NetBIOS (139), IMAP (143), DNS (53), RPC (135), MySQL (3306), HTTP Alt (8080), PPTP (1723), RPC Bind (111), and more.

   3. Scanning Specific IP Ranges with `masscan`:
   `
   masscan -p 80,443,53,445,3389 --rate 1000 -oG 192.168.0.0_16_discovery 192.168.0.0/16
   masscan -p 80,443,53,445,3389 --rate 1000 -oG 172.16.0.0_12_discovery 172.16.0.0/12
   masscan -p 80,443,53,445,3389 --rate 1000 -oG 10.0.0.0_discovery 10.0.0.0/8
   `
   These commands use the `masscan` tool to scan specific IP ranges for the listed ports. The `-p` flag specifies the ports to scan, the `--rate` flag sets the scanning rate, and the `-oG` flag specifies the output format and file name. The IP ranges include private network ranges (192.168.0.0/16, 172.16.0.0/12, 10.0.0.0/8), which are commonly used in local networks.


5. **Service Enumeration:**
   - Conduct targeted scans on ports of interest to identify active services.
     `nmap -sS -sV -Pn -p[port] <ip>`

6. **Attacks:**
   - Focus on exploiting low-hanging fruit vulnerabilities.
   1. Command to Identify EternalBlue Vulnerability (MS17-010) in SMB:
    `nmap -p445 --script smb-vuln-ms17-010 <target>`
   - `-p445`: Specifies that the scan should target port 445, which is the default port for SMB.
   - `--script smb-vuln-ms17-010`: This NSE script checks the target host for the presence of the MS17-010 vulnerability, commonly referred to as EternalBlue. This vulnerability affects the SMB protocol and was famously used in the WannaCry ransomware attack.

## Network Traffic Capture

1. **Open Wireshark:**
   - Launch Wireshark, a powerful network packet analysis tool.

2. **Apply Filters for Broadcast, Multicast, CDP, or VTP:**
   - Use Wireshark's filter capabilities to focus on specific types of network traffic.

3. **Filter for Broadcast and Multicast:**
   - To capture broadcast and multicast traffic, use the following filter:
     `(eth.dst[0] & 1)`
   - This filter captures traffic with the least significant bit of the destination MAC address set to 1, which indicates broadcast or multicast traffic.

4. **Filter for Multicast Only:**
   - To capture multicast traffic exclusively and exclude broadcast traffic, use the following filter:
     `(eth.dst[0] & 1) && !eth.dst==ff:ff:ff:ff:ff:ff`
   - This filter combines the multicast filter with a check to exclude the broadcast MAC address.

5. **Filter for VTP Traffic:**
   - To capture VLAN Trunking Protocol (VTP) traffic, use the following filter:
     `vtp`
   - This filter specifically captures VTP protocol packets.

6. **Filter for CDP Traffic:**
   - To capture Cisco Discovery Protocol (CDP) traffic, use the following filter:
     `cdp`
   - This filter captures CDP protocol packets.

Applying these filters in Wireshark allows you to focus on specific types of network traffic, making it easier to analyze and understand the behavior of your network. This can be particularly useful for identifying issues, misconfigurations, or potentially malicious activities on your network.

## VLAN Hopping
**Scenario:**
In a network environment where VLANs (Virtual Local Area Networks) are utilized, VLAN hopping is a technique used to attack a network by sending packets to a port that is not normally accessible from a given end system. This method takes advantage of vulnerabilities in VLAN configuration and can lead to unauthorized access to other VLANs.

**Requisites:**
To execute a VLAN hopping attack, you need to know the following:
1. The VLAN in which your attacking device is currently placed.
2. The VLAN name and IP address syntax of a device that you cannot ping within the target VLAN.

**Attack Steps:**
1. Identify the protocol used by the company's switches for trunking, such as DTP (Dynamic Trunking Protocol) for Cisco switches.
2. Launch the attack using a tool like Yersinia:
   - Select the protocol used by the switches.
   - Initiate the DTP attack to force trunking negotiation.

**Mitigations:**
To prevent VLAN hopping attacks, consider the following mitigations:
1. Disable DTP: Ensure that ports are not set to automatically negotiate trunks by disabling Dynamic Trunking Protocol (DTP) on switch interfaces.
2. Avoid VLAN 1: Never use VLAN 1 for active traffic, as it is often used as a default VLAN and can be more susceptible to VLAN hopping attacks.
3. Disable Unused Ports: Disable unused switch ports and assign them to an unused VLAN to prevent unauthorized access.
4. Use Dedicated VLAN IDs: Always use dedicated and unique VLAN IDs for all trunk ports. Avoid using common or default VLAN IDs.
5. Network Segmentation: Implement proper network segmentation and access control to isolate VLANs and limit the potential impact of a successful attack.

**Commands:**
Here are the commands for configuring VLAN hopping manually, if necessary:
1. Enable Trunking (Specific to Brand Switch):
   `modprobe 802q`
2. Add VLAN:
   `vconfig add [interface] [VLAN ID]
    vconfig add eth0 200`
3. Set Interface Up:
   `ifconfig [interface.VLAN ID] up
    ifconfig eth0.200 up`
4. Assign IP and Bring Interface Up:
   `ifconfig [interface.VLAN ID] [new IP with correct syntax of target VLAN] up
   ifconfig eth0.200 10.0.0.6 up`
## Vulnerabilities in Multi-Homed Devices
**Overview:**
Identify devices on the network, enumerate them, and attempt to exploit them to pivot towards devices that are only visible from the compromised asset. Alternatively, verify that the target is not conducting any port forwarding of a service.

**Exploitation Steps:**
1. Attempt to identify devices on the network that are "multi-homed," meaning they have multiple network interfaces connected to different networks.
2. Enumerate and gather information about these multi-homed devices to understand their capabilities, services, and possible vulnerabilities.
3. Attempt to exploit any vulnerabilities found on these devices to gain unauthorized access or control.
4. If successful, use these compromised devices as pivot points to access other devices or networks that are otherwise inaccessible from the initial compromised asset.

**Port Forwarding and Testing:**
As an alternative approach, if the target device is not conducting port forwarding, you can attempt the following steps:
1. Add a VLAN and assign it to your interface (specific to brand and switch configuration):
   `vconfig add [interface] [VLAN ID]
    vconfig add eth0 200`
2. Bring up the interface with the assigned VLAN:
   `ifconfig [interface.VLAN ID] up
    ifconfig eth0.200 up`
4. Assign an IP address to the interface on the new VLAN:
   ` ifconfig [interface.VLAN ID] [new IP with correct syntax of target VLAN] up
    ifconfig eth0.200 10.0.0.6 up`
5. Perform port forwarding of a service, setting the target IP as the gateway (DG) for your interface.
6. Attempt to identify the service running behind the port forwarding and verify if you can access the service fully, not just the forwarded port.

### Refernces
1. https://infinitelogins.com/2020/04/24/transferring-files-via-base64/
2. https://weakpass.com/
3. https://in.security/technical-training/password-cracking/
4. https://vast.ai/
5. https://github.com/stealthsploit/OneRuleToRuleThemStill

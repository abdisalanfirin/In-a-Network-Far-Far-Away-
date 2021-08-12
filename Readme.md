# Networks Fundamentals II Homework: In a Network Far, Far Away!


## Background


You are a Network Jedi working for the Resistance.
The Sith Empire recently carried out a DoS attack, taking out the Resistance's core network infrastructure, including its DNS servers.
This attack destroyed the Resistance's ability to communicate via email and retrieve other crucial information about each others' operations.
The Empire has taken advantage of this compromised availability by ambushing numerous Resistance outposts, all vulnerable because they can no longer call for help.
Your task is a crucial one: Restore the Resistance's core DNS infrastructure and verify that traffic is routing as expected.
Good luck and may the Force be with you!


## Your Objectives:


Review each network issue in the missions below.

Document each DNS record type found.

Take note of the DNS records that can explain the reasons for the existing network issue.

Provide recommended fixes to save the Galaxy!

Submit your results and findings in a document.

Topics Covered in Your Assignments

DNS
NSLOOKUP
DNS record types
A, PTR, MX, NS, SOA, SRV, TXT
Wireless
WEP, WPA
Aircrack-ng
Wireshark Wireless analysis and decryption


## Mission 1

Issue: Due to the DoS attack, the Empire took down the Resistance's DNS and primary email servers.

The Resistance's network team was able to build and deploy a new DNS server and mail server.

The new primary mail server is asltx.l.google.com and the secondary should be asltx.2.google.com.

The Resistance (starwars.com) is able to send emails but unable to receive any.


## Your mission:

Determine and document the mail servers for starwars.com using NSLOOKUP.

## Answer

command: - *nslookup type=mx starwars.com*

Explain why the Resistance isn't receiving any emails.

## Answer

the resistance is not receving emails becouse the new primary server mail asltx.1.google.com and the secondary sarver asltx.2.google.com is not part of the mail exchanger servers. 
i dont see the new mail sarvers inside the resistance DNS email servers.

Document what a corrected DNS record should be.

## Answer

the corrected DNS should be like this.
- *starwars.com     mail exchanger = 1 asltx.l.google.com*
- *starswars.com    mail exchanger = 2 asltx.2.google.com*

- *![MISSION ONE](./Images/snap_1.PNG)*

### Mission 2

Issue: Now that you've addressed the mail servers, all emails are coming through. However, users are still reporting that they haven't received mail from the theforce.net alert bulletins.
Many of the alert bulletins are being blocked or going into spam folders.
This is probably due to the fact that theforce.net changed the IP address of their mail server to 45.23.176.21 while your network was down.
These alerts are critical to identify pending attacks from the Empire.


## Your mission:

Determine and document the SPF for theforce.net using NSLOOKUP.

## Answer
 
 - *nslookup -type=TXT theforce.net*

Explain why the Force's emails are going to spam.

## Answer

becouse the IP for their mail server to 45.23.176.21 is not listed or included in their the theforce.net server.  

Document what a corrected DNS record should be.

## Answer

theforce.net	text = "v=spf1 a mx mx:smtp.secureserver.net include:aspmx.googlemail.com ip4:45.23.176.21"

- *![MISSION TWO](./Images/snap_2.PNG)*

### Mission 3
Issue: You have successfully resolved all email issues and the resistance can now receive alert bulletins. However, the Resistance is unable to easily read the details of alert bulletins online.
They are supposed to be automatically redirected from their sub page of resistance.theforce.net  to theforce.net.

## Your mission:

Document how a CNAME should look by viewing the CNAME of www.theforce.net using NSLOOKUP.

### Answer

- *nslookup -type=CNAME www.theforce.net*


Explain why the sub page of resistance.theforce.net isn't redirecting to 

## Answer

the alliance server shows wrong theforce.net and it  has the wrong canonical name.

Document what a corrected DNS record should be.

## Answer

resistance.theforce.net 	canonical name = theforce.net.

- *![MISSION THREE](./Images/snap_3.PNG)*

## Mission 4

Issue: During the attack, it was determined that the Empire also took down the primary DNS server of princessleia.site.
Fortunately, the DNS server for princessleia.site is backed up and functioning.
However, the Resistance was unable to access this important site during the attacks and now they need you to prevent this from happening again.
The Resistance's networking team provided you with a backup DNS server of: ns2.galaxybackup.com.


## Your mission:

Confirm the DNS records for princessleia.site.

## Answer

- *nslookup -type=NS princessleia.site*

- *![MISSION FOUR](./Images/snap_4.PNG)*

Document how you would fix the DNS record to prevent this issue from happening again.

## Answer

- *princessleia.site	nameserver = ns25.domaincontrol.com.*
- *princessleia.site	nameserver = ns26.domaincontrol.com.*
- *princessleia.site	nameserver = ns25.galaxybackup.com.*

### Mission 5
Issue: The network traffic from the planet of Batuu to the planet of  Jedha is very slow.
You have been provided a network map with a list of planets connected between Batuu and Jedha.
It has been determined that the slowness is due to the Empire attacking Planet N.

## Your Mission:

View the Galaxy Network Map and determine the OSPF shortest path from Batuu to Jedha.
Confirm your path doesn't include Planet N in its route.
Document this shortest path so it can be used by the Resistance to develop a static route to improve the traffic.

## Answer

The shortest bath between the Batuu and Jedha is as following
Batuu = D-C-E-F-J-K-O-R-Q-T-V = Jedha

- *![MISSION FIVE](./Images/snap_5.PNG)*

### Mission 6

Issue: Due to all these attacks, the Resistance is determined to seek revenge for the damage the Empire has caused.
You are tasked with gathering secret information from the Dark Side network servers that can be used to launch network attacks against the Empire.
You have captured some of the Dark Side's encrypted wireless internet traffic in the following pcap: Darkside.pcap.

## Your Mission:

Figure out the Dark Side's secret wireless key by using Aircrack-ng.
Hint: This is a more challenging encrypted wireless traffic using WPA.
In order to decrypt, you will need to use a wordlist (-w) such as rockyou.txt.
Use the Dark Side's key to decrypt the wireless traffic in Wireshark.
Hint: The format for they key to decrypt wireless is <Wireless_key>:<SSID>.

## Answer

- *aircrack-ng -w /usr/share/wordlists/rockyou.txt Darkside.pcap* 

- *aircrack-ng -w /usr/share/wordlists/rockyou.txt Darkside.pcap* 

- *![MISSION SIX](./Images/snap_6.PNG)*

Once you have decrypted the traffic, figure out the following Dark Side information:
Host IP Addresses and MAC Addresses by looking at the decrypted ARP traffic.

- *![MISSION SIX](./Images/snap_x.PNG)*

Document these IP and MAC Addresses, as the resistance will use these IP addresses to launch a retaliatory attack.

## Answer

MAC: address: Cisco-Li_e3:e4:01 (00:0f:66:e3:e4:01)
IP address: 172.16.0.1
MAC address : IntelCor_55:98:ef (00:13:ce:55:98:ef)
IP address : 172.16.0.101

- *![MISSION SIX](./Images/snap_Y.PNG)*

### Mission 7

As a thank you for saving the galaxy, the Resistance wants to send you a secret message!

## Your Mission:


View the DNS record from Mission #4.
The Resistance provided you with a hidden message in the TXT record, with several steps to follow.
Follow the steps from the TXT record.
Note: A backup option is provided in the TXT record (as a website) in case the main telnet site is unavailable
Take a screen shot of the results.

## Answer

- *![MISSION SEVEN](./Images/snap_7.PNG)*
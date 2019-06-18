![Cisco88xxSetup logo](https://github.com/bhdicaire/Cisco88xxSetup/raw/master/img/logo.png)

You’ve been there too — setting up a new IP Phone can be an ad-hoc, manual, and time-consuming process.

So you got your hands on a Cisco 88xx Third-Party Call Control Setup Phone and now you want to get it up and running in next to no time.
8800 Series Multiplatform IP Phone 
It took too much time too setup the phone especially the firmware update. The information available online was either overly complex and/or incomplete.

My objective is to fully document my installation and configuration with [VoIP.ms](https://VoIP.ms). Feel free to fork, and customize for your IP telephony ecosystem ...

The Cisco IP Phone is used as a part of a SIP network, because the phone supports Session Initiation Protocol (SIP). The Cisco IP Phone is compatible with other SIP IP PBX call control systems, such as BroadSoft, MetaSwitch, and Asterisk.
Configuration of these systems is not described in this document. For more information, see the documentation for the SIP PBX system to which you are connecting the Cisco IP Phone.
This document describes some common network configurations; however, your configuration can vary, depending on the type of equipment that your service provider uses.


## What problem does it solve and why is it useful?

CISCO ... are great but the configuration ...

Phones can be provisioned to download configuration profiles or updated firmware from a remote server when they are connected to a network, when they are powered up, and at set intervals. Provisioning is typically part of high-volume, Voice-over-IP (VoIP) deployments and is limited to service providers.
Web-Based Configuration Utility
Your phone system administrator can allow you to view the phone statistics and modify some or all the parameters. 

No default passwords are assigned to either the administrator or the user account. Only the administrator account can assign or change passwords.

## Procedure

<details>
<summary>Quick setup</summary>
<br>
1. Locate the phone that you need to set up.


 On the phone, press Settings > Status > Product Information, and look at the MAC address field.
 
 Access the Web-Based Configuration Utility
 Step 1 Step 2 Step 3
Access the Cisco IP Phone configuration utility from a web browser on a computer that can reach the phone on the subnetwork.

Determine the IP Address of the Phone
A DHCP server assigns the IP address, so the phone must be booted up and connected to the subnetwork.
Procedure
Step 1 Click Admin Login > advanced > Info > Status.
Step 2 Scroll to IPv4 Information. Current IP displays the IP address.

Allow Web Access to the Cisco IP Phone
To view the phone parameters, enable the configuration profile. To make changes to any of the parameters, you must be able to change the configuration profile. Your system administrator might have disabled the phone option to make the phone web user interface viewable or writable.
For more information, see the Cisco IP Phone 7800 Series and Cisco IP Phone 8800 Series Multiplatform Phones Provisioning Guide.
Procedure
Click Admin Login > Voice > System.
In the System Configuration section, set Enable Web Server to Yes.

To clear all changes that you made during the current session (or after you last clicked Submit All Changes), click Undo All Changes. Values return to their previous settings.
 
</details>

<details>

<summary>Upgrade IP Phone Firmware</summary>
1. https://www.ukvoipforums.com/viewtopic.php?f=21&t=1114

CISCO 8800 SERIES XMLDEFAULT.CNF.XML FILE

https://www.cisco.com/c/en/us/support/collaboration-endpoints/ip-phone-8800-series-multiplatform-firmware/tsd-products-support-series-home.html
You now have successfully upgraded the firmware on your Cisco IP Phone 7800 Series or Cisco IP Phone 8800 Series Multiplatform phone through the Upgrade Rule in the web-based utility.
</details>
<details>
<summary>SIP configuration</summary>
<br>
Connect your PC to the phone using its LAN side Ethernet port marked PC, in order to use the LAN gateway IP address into your Web Browser as the phone's ip address.

You can get the Phone's IP address via the configuration menu --> 8. Status. 

1. Connect and Login to the *CP-88xx-3PCC Configuration Utility*  Web Based Configuration Interface, in my case it's [192.168.168.99](http://192.168.168.99)
	* You have to use *HTTP* for now, we'll inject a certificate later in the procedure
	* By default, there are no **User** or **Admin** passwords required to connect and login
	* I had issues with Google Chrome & Microsoft Edge, I recommend Safari on MacOS

2. You will be landing on and viewing the "Info" page, in "Basic" view if you're not using [http://192.168.168.99/admin/advanced](http://192.168.168.99/admin/advanced)

3. In the web-based utility of your IP Phone, click Voice -> System

	**Under System Configuration**
	
	Item | Value
	---- | ----
	Change User Password| *Awesome*
	Change Admin Password | *Incredible*
	Phone-UI-user Mode | Yes	

	**Under Power Settings**

	Item | Value
	---- | ----
	Disable Back USB Port| Yes

	**Under IPv4 settings:**

	Item | Value
	---- | ----
	IP Mode| IPv4 Only	

	**Under Optional Network Configuration**

	Item | Value
	---- | ----
	Host Name| Phone
	Domain| Dicaire.com
	Primary NTP Server| pool.ntp.org
	Enable LLDP-MED| No
	Enable CDP | No		

	**Under Inventory Settings**
	
	Item | Value
	---- | ----
	Asset ID| Phone.Dicaire.com	
		
4. Click Submit All Changes.
	* The phone reboots and the changes are applied.

5. In the web-based utility of your IP Phone, click Voice -> Regional

	**Under Time**
	
	Item | Value
	---- | ----
	Time Zone| GMT-5

6. Click Submit All Changes.

7. In the web-based utility of your IP Phone, click Voice -> Phone

	**Under General**
	
	Item | Value
	---- | ----
	Station Name| bhdicaire
	Station Display Name| BH Dicaire	

	**Under Handsfree**
	
	Item | Value
	---- | ----
	Bluetooth Mode| Both
	Line| 7
	
	**Under Line Key**
	
	Line | Ext | Short Name | Share Call
	---- | ----|---- | ----
	1|1| Office | Private
	1|1| Office #2| Private
	1|1| Site #2| Private
	1|1| Site #3| Private			

	**Under Supplementary Services**
	
	Item | Value
	---- | ----
	Cfwd All Serv | No
	Secure Call Serv| Yes
	Cfwd Busy Serv| No
	Group Call Pick Up Serv| No
	DND Serv| No
	Cfwd All Serv| No
	Call Park Serv| No

	**Under Ringtone**
	
	Ring | Value
	---- | ----
	1| n=Sunrise;w=file://Sunrise.rwb;c=1
	2| n=Sunrise;w=file://Sunrise.rwb;c=1
	3| n=Sunrise;w=file://Sunrise.rwb;c=1
	4| n=Sunrise;w=file://Sunrise.rwb;c=1
	5| n=Sunrise;w=file://Sunrise.rwb;c=1
	6| n=Sunrise;w=file://Sunrise.rwb;c=1
	7| n=Sunrise;w=file://Sunrise.rwb;c=1
	8| n=Sunrise;w=file://Sunrise.rwb;c=1
	9| n=Sunrise;w=file://Sunrise.rwb;c=1
	10| n=Sunrise;w=file://Sunrise.rwb;c=1
		
8. Click Submit All Changes

9. In the web-based utility of your IP Phone, click Voice -> User

	**Under Supplementary Services**
	
	Item | Value
	---- | ----
	Secure Call Setting| yes

7. In the web-based utility of your IP Phone, click Voice -> Ext1 for Encrypted Call

	**Under NAT Settings**
	
	Item | Value
	---- | ----
	NAT Mapping Enable | Yes
	NAT Keep Alive Enable | Yes 
	
	**Under SIP Settings**
	
	Item | Value
	---- | ----
	SIP Transport| TLS
	SIP Port | 5060
	Ext SIP Port | 5061		
	
	**Under Call Feature Settings**
	
	Item | Value
	---- | ----
	Default ring | Mischief			

	**Under Proxy and Registration**

	Item | Value
	---- | ----
	Proxy | Chicago3.VOIP.ms
	Outbound Proxy | Chicago3.VOIP.ms 	
	Register Expire| 300
	Proxy Fallback Intvl|300
	DNS SRV Auto Prefix| No
	

	**Under Subscriber Information**

	Item | Value
	---- | ----
	Display Name | BH Dicaire
	User ID| xxxxxx60
	Password| Incredible

	**Under Dial Plan**

	Item | Value
	---- | ----
	Dial Plan | "(911S0|310xxxx|<:1514>[2-9]xxxxxx|1[2-9]xx[2-9]xxxxxxS0|[2-9]xx[2-9]xxxxxxS0|*xx|***xxx|*xx.|[3468]11|822|0|00|4xxx|**275*x.|xxxxxxxxxxxx.)"

8. In the web-based utility of your IP Phone, click Voice -> Ext2 for Encrypted Call

	**Refer to Ext1 configuration, except for the SIP Ports under SIP Settings**

	Item | Value
	---- | ----
	SIP Port | 5061
	Ext SIP Port | 5081	
	
	**Under Call Feature Settings**
	
	Item | Value
	---- | ----
	Default ring | Mischief	

9. Click Submit All Changes.

10. In the web-based utility of your IP Phone, click Voice -> Ext3 for Encrypted Call

	**Refer to Ext1 configuration, except for the SIP Ports under SIP Settings**

	Item | Value
	---- | ----
	SIP Port | 5062
	Ext SIP Port | 42873	
	
	**Under Call Feature Settings**
	
	Item | Value
	---- | ----
	Default ring | Ascent

11. Click Submit All Changes.
	
12. In the web-based utility of your IP Phone, click Voice -> Ext4

	**Under NAT Settings**
	
	Item | Value
	---- | ----
	NAT Mapping Enable | Yes
	NAT Keep Alive Enable | Yes 
	
	**Under SIP Settings**
	
	Item | Value
	---- | ----
	SIPO Port | 5063
		

	**Under Proxy and Registration s**

	Item | Value
	---- | ----
	Proxy | Chicago3.VOIP.ms
	Outbound Proxy | Chicago3.VOIP.ms 	
	Register Expire| 300
	Proxy Fallback Intvl| 300	
	DNS SRV Auto Prefix| No
	

	**Under Subscriber Information**

	Item | Value
	---- | ----
	Display Name | BH Dicaire
	User ID| xxxxxx60
	Password| Incredible

	**Under Dial Plan**

	Item | Value
	---- | ----
	Dial Plan | (911S0|310xxxx|<:1514>[2-9]xxxxxx|1[2-9]xx[2-9]xxxxxxS0|[2-9]xx[2-9]xxxxxxS0|*xx|***xxx|*xx.|[3468]11|822|0|00|4xxx|**275*x.|xxxxxxxxxxxx.)
	
</details>
<details>
<summary>4. Bluetooth configuration</summary>

 This is being accomplish with the use of [homebrew](https://github.com/Homebrew/homebrew), [homebrew-cask](https://github.com/caskroom/homebrew-cask), and the Mac Apple Store CLI [(MAS)](https://github.com/mas-cli/mas).
Press the Applications button on your IP Phone.
Select 5. Bluetooth
Change Bluetooth to ON and press Set button
	* The phone reboots and the changes are applied.
Press the Applications button on your IP Phone.
Select 5. Bluetooth
Press the scan button and then pair your phone



</details>


Applicable Devices
IP Phone 7800 Series
IP Phone 8800 Series

Software version
11.0.1
References

[Upgrade the Firmware on the Cisco IP Phone 7800 and 8800 Multiplatform Series through the Web Browser Command]
(https://www.cisco.com/c/en/us/support/docs/smb/collaboration-endpoints/cisco-ip-phone-7800-series/smb5431-upgrade-the-firmware-on-the-cisco-ip-phone-7800-and-8800-mul.html?referring_site=RE&pos=3&page=https://www.cisco.com/c/en/us/support/docs/unified-communications/unified-communications-manager-callmanager/213288-upgrade-ip-phone-firmware-individually.html)
Voip.MS configuration https://wiki.voip.ms/article/Cisco_SPA525G

## Licence

Cisco88xxSetup by Benoît H. Dicaire is shared under [CC-BY-SA-4.0](https://github.com/bhdicaire/solarized/raw/master/LICENCSE). This licence is recommended by [Choose a License.com](https://choosealicense.com/) for non-software material such as documentation and media.


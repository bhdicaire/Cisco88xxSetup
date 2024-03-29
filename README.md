![Cisco8861 image](https://github.com/bhdicaire/Cisco88xxSetup/raw/master/img/Cisco8861.jpg)

You’ve been there too — setting up a new IP Phone can be an ad-hoc, manual, and time-consuming process.

So you got your hands on a [Cisco IP Phone 88xx Series with Multiplatform Firmware](https://www.cisco.com/c/en/us/products/collateral/collaboration-endpoints/unified-ip-phone-8800-series/datasheet-c78-738030.pdf) and now you want to get it up and running encrypted voice call with your favorite Voice-over-IP (VoIP) Service Provider.

A Cisco IP Phone such as the [8861 aka part# CP-8861-3PCC-K9= ](https://www.cisco.com/c/en/us/products/collateral/collaboration-endpoints/unified-ip-phone-8800-series/datasheet-c78-731668.pdf) supports Session Initiation Protocol (SIP) with Third-Party Call Control Setup! It's a *great* phone with a ~~difficult~~ setup.

My objective is to document my configuration for encrypted calls with [VoIP.ms](https://VoIP.ms). Feel free to fork, and customize it for your IP telephony ecosystem.

## What problem does it solve and why is it useful?

I spent too much time upgrading the phone firmware :disappointed: Cisco does not include the [XMLDefault.cnf.xml](https://github.com/bhdicaire/Cisco88xxSetup/raw/master/XMLDefault.cnf.xml) required to upgrade the firmware nor identify that you'll not be able to complete the operation without it.

Provisioning is typically part of high-volume VoIP deployments thus most of the documentation focused on managing the phone via the call manager (Cisco Unified Communications Manager).  

This document describes some common configurations via the Web-Based Configuration Utility and a TFTP server.

## Procedure

Applicable Devices with software version 11.2.3MSR1-1
* IP Phone 7800 Series
* IP Phone 8800 Series

<details>
<summary>Quick setup</summary>
<br>
Locate the phone that you need to set up :stuck_out_tongue_winking_eye:

No default passwords are assigned to either the administrator or the user account. 

1. On the phone, press Settings > Status > Network Status > IPv4 Status
	* Look at current IP address
 
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

 
</details>

<details>

<summary>Upgrade IP Phone Firmware</summary>
1.
<br>
Phones can be provisioned to download configuration profiles or updated firmware from a TFTP server when they are powered up.

1. Obtain the current firmware files
	* Download from the Cisco web Site
2. Extract the .zip package to a folder on your computer
3. Setup a TFTP Server on the same subnet
	* I used the one included on macOS Mohave,  
	* Copy all files from the firmware archive in the root directory of the TFTP server, in my case /private/tftpboot/
4. Modify the [XMLDefault.cnf.xml](https://github.com/bhdicaire/Cisco88xxSetup/raw/master/XMLDefault.cnf.xml) to ensure your phone model is included (e.g Cisco 8861) and the firmware version to install (e.g. sip88xx.11-2-3MSR1-1)
5. Copy XMLDefault.cnf.xml in the root directory of the TFTP server




https://www.cisco.com/c/en/us/support/collaboration-endpoints/ip-phone-8800-series-multiplatform-firmware/tsd-products-support-series-home.html
You now have successfully upgraded the firmware on your Cisco IP Phone 7800 Series or Cisco IP Phone 8800 Series Multiplatform phone through the Upgrade Rule in the web-based utility.
</details>
<details>
<summary>SIP configuration</summary>
<br>
Connect your PC to the phone using its LAN side Ethernet port marked PC, in order to use the LAN gateway IP address into your Web Browser as the phone's ip address.

You can get the Phone's IP address via the configuration menu --> 8. Status. 

Enter the IP address of the Cisco IP Phone in a web browser and include the admin/ extension.

1. Login to the *CP-88xx-3PCC Configuration Utility* Web Based Configuration Interface with the IP address with the /admin/ extension. in your favorite web browser, in my case it's [192.168.168.99/admin](http://192.168.168.99/admin)
	* You have to use *HTTP* for now, we'll inject a certificate later in the procedure
	* By default, there are no **User** or **Admin** passwords required to connect and login
	* I had issues with Google Chrome & Microsoft Edge, I recommend Safari on MacOS

2. You will be landing on and viewing the "Info" page, in "Basic" view if you're not using the extension /admin/advanced/ [http://192.168.168.99/admin/advanced](http://192.168.168.99/admin/advanced)

3. In the web-based utility of your IP Phone, click Voice -> System

	**System Configuration**
	
	Item | Value
	---- | ----
	Change User Password| *Awesome*
	Change Admin Password | *Incredible*
	Phone-UI-user Mode | Yes	

	**Power Settings**

	Item | Value
	---- | ----
	Disable Back USB Port| Yes

	**IPv4 settings:**

	Item | Value
	---- | ----
	IP Mode| IPv4 Only	

	**Optional Network Configuration**

	Item | Value
	---- | ----
	Host Name| CiscoPhone
	Domain| Dicaire.com
	Primary NTP Server| pool.ntp.org
	Enable LLDP-MED| No
	Enable CDP | No		

	**Inventory Settings**
	
	Item | Value
	---- | ----
	Asset ID| Phone.Dicaire.com	
		
4. Click Submit All Changes.
	* The phone reboots and the changes are applied

5. In the web-based utility of your IP Phone, click Voice -> Regional

	**Time**
	
	Item | Value
	---- | ----
	Time Zone| GMT-5

6. Click Submit All Changes.

7. In the web-based utility of your IP Phone, click Voice -> Phone

	**General**
	
	Item | Value
	---- | ----
	Station Name| bhdicaire
	Station Display Name| BH Dicaire	

	**Handsfree**
	
	Item | Value
	---- | ----
	Bluetooth Mode| Both
	Line| 7
	
	**Line Key**
	
	Line | Ext | Short Name | Share Call
	---- | ----|---- | ----
	1|1| Office | Private
	2|1| Office #2| Private
	4|2| Site #2| Private
	6|3| Site #3| Private			

	**Supplementary Services**
	
	Item | Value
	---- | ----
	Cfwd All Serv | No
	Secure Call Serv| Yes
	Cfwd Busy Serv| No
	Call Pick Up Serv| No
	Group Call Pick Up Serv| No
	DND Serv| No
	Cfwd All Serv| No
	Call Park Serv| No

	**Ringtone**
	
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

7. In the web-based utility of your IP Phone, click Voice -> Ext1

	**NAT Settings**
	
	Item | Value
	---- | ----
	NAT Mapping Enable | Yes
	NAT Keep Alive Enable | Yes 
	
	**SIP Settings**
	
	Item | Value
	---- | ----
	SIP Transport| TLS
	SIP Port | 5060
	Ext SIP Port | 5061		
	
	**Call Feature Settings**
	
	Item | Value
	---- | ----
	Default ring | Mischief			

	**Proxy and Registration**

	Item | Value
	---- | ----
	Proxy | Chicago3.VOIP.ms
	Outbound Proxy | Chicago3.VOIP.ms 	
	Register Expire| 300
	Proxy Fallback Intvl|300
	DNS SRV Auto Prefix| No
	

	**Subscriber Information**

	Item | Value
	---- | ----
	Display Name | BH Dicaire
	User ID| xxxxxx60
	Password| Incredible

	**Dial Plan**
 `(911S0|310xxxx|<:1514>[2-9]xxxxxx|1[2-9]xx[2-9]xxxxxxS0|[2-9]xx[2-9]xxxxxxS0|*xx|***xxx|*xx.|[3468]11|822|0|00|4xxx|**275*x.|xxxxxxxxxxxx.)`

8. In the web-based utility of your IP Phone, click Voice -> Ext2

	**Refer to Ext1 configuration**

	Item | Value
	---- | ----
	SIP Port | 5061
	Ext SIP Port | 5081	
	
	**Call Feature Settings**
	
	Item | Value
	---- | ----
	Default ring | Mischief	

9. Click Submit All Changes.

10. In the web-based utility of your IP Phone, click Voice -> Ext3

	**Refer to Ext1 configuration**

	Item | Value
	---- | ----
	SIP Port | 5062
	Ext SIP Port | 42873	
	
	**Call Feature Settings**
	
	Item | Value
	---- | ----
	Default ring | Ascent

11. Click Submit All Changes.
	
12. In the web-based utility of your IP Phone, click Voice -> Ext4 for unencrypted call

	**NAT Settings**
	
	Item | Value
	---- | ----
	NAT Mapping Enable | Yes
	NAT Keep Alive Enable | Yes 
	
	**SIP Settings**
	
	Item | Value
	---- | ----
	SIPO Port | 5063
		

	**Proxy and Registration s**

	Item | Value
	---- | ----
	Proxy | Chicago3.VOIP.ms
	Outbound Proxy | Chicago3.VOIP.ms 	
	Register Expire| 300
	Proxy Fallback Intvl| 300	
	DNS SRV Auto Prefix| No
	

	**Subscriber Information**

	Item | Value
	---- | ----
	Display Name | BH Dicaire
	User ID| xxxxxx60
	Password| Incredible

	**Dial Plan**
 `(911S0|310xxxx|<:1514>[2-9]xxxxxx|1[2-9]xx[2-9]xxxxxxS0|[2-9]xx[2-9]xxxxxxS0|*xx|***xxx|*xx.|[3468]11|822|0|00|4xxx|**275*x.|xxxxxxxxxxxx.)`

</details>
<details>
<summary>Bluetooth configuration</summary>

1. Press the Applications button on your IP Phone
2. Select 5. Bluetooth
3. Change Bluetooth to ON and press [SET] button
	* The phone reboots and the changes are applied
4. Press the Applications button on your IP Phone
5. Select 5. Bluetooth
6. Press the scan button and then pair your phone
</details>

### Secure voice (SRTP) call set-up diagram

Insert diagram

## References

1.[CISCO 8800 SERIES XMLDEFAULT.CNF.XML FILE](https://www.ukvoipforums.com/viewtopic.php?f=21&t=1114)
2. [UK VoIP Forums's guide for upgrading a Cisco 8811 IP Phone SIP Firmware](https://www.ukvoipforums.com/downloads/cisco-8800-series.html)
3, [SUPPORT: Cisco IP Phone 8800 Series with Multiplatform Firmware](https://www.cisco.com/c/en/us/support/collaboration-endpoints/ip-phone-8800-series-multiplatform-firmware/tsd-products-support-series-home.html)


[Upgrade the Firmware on the Cisco IP Phone 7800 and 8800 Multiplatform Series through the Web Browser Command](https://www.cisco.com/c/en/us/support/docs/smb/collaboration-endpoints/cisco-ip-phone-7800-series/smb5431-upgrade-the-firmware-on-the-cisco-ip-phone-7800-and-8800-mul.html?referring_site=RE&pos=3&page=https://www.cisco.com/c/en/us/support/docs/unified-communications/unified-communications-manager-callmanager/213288-upgrade-ip-phone-firmware-individually.html)
2. [Voip.MS — sample CISCO phone configuration](https://wiki.voip.ms/article/Cisco_SPA525G)
3. [VoIP.ms — Call Encryption with TLS/SRTP](https://wiki.voip.ms/article/Call_Encryption_-_TLS/SRTP)
## Licence

Cisco88xxSetup by Benoît H. Dicaire is shared under [CC-BY-SA-4.0](https://github.com/bhdicaire/solarized/raw/master/LICENCSE). This licence is recommended by [Choose a License.com](https://choosealicense.com/) for non-software material such as documentation and media.


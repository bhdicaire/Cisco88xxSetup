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
<summary>1. Quick setup</summary>
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

<summary>2. Upgrade IP Phone Firmware</summary>
1. https://www.ukvoipforums.com/viewtopic.php?f=21&t=1114

CISCO 8800 SERIES XMLDEFAULT.CNF.XML FILE

https://www.cisco.com/c/en/us/support/collaboration-endpoints/ip-phone-8800-series-multiplatform-firmware/tsd-products-support-series-home.html
You now have successfully upgraded the firmware on your Cisco IP Phone 7800 Series or Cisco IP Phone 8800 Series Multiplatform phone through the Upgrade Rule in the web-based utility.
</details>
<details>
<summary>3. SIP configuration</summary>
<br>
Connect your PC to the phone using its LAN side Ethernet port marked PC, in order to use the LAN gateway IP address into your Web Browser as the phone's ip address. Of course, you can get the Phone's IP address via the configuration menu --> 8. Status. 

1. Connect and Login to the *CP-88xx-3PCC Configuration Utility*  Web Based Configuration Interface, in my case it's [192.168.168.99](http://192.168.168.99)
	* You have to use *HTTP* for now, we'll inject a certificate later in the procedure
	* By default, there are no **User** or **Admin** passwords required to connect and login
	* I had issues with Google Chrome & Microsoft Edge, I recommend Safari on MacOS
2. You will be landing on and viewing the "Info" page, in "Basic" view if you're not using [http://192.168.168.99/admin/advanced](http://192.168.168.99/admin/advanced)

4. In the web-based utility of your IP Phone, click Voice > System

	**Under System Configuration**
	a. Change User and Admin passwords
	b. Phone-UI-user Mode, choose Yes

	**Under Power Settings:**
	1. Disable Back USB Port, choose Yes

	**Under IPv4 settings:**
	1. IP mode, choose IPv4 Only

	**Under Optional Network Configuration:**
	1. Host Name: 
5. To update the configuration profile, click Submit All Changes after you modify the fields in the phone web user interface.
	* The phone reboots and the changes are applied.

 in the Phone-UI-User-Mode field, choose Yes. Click Submit All Changes.





Step 2	


Step 3	
Navigate to the Product Specific Configuration area and set the following fields:

Days Display Not Active

Display On Time

Display On Duration

Display Idle Timeout
</details>
<details>
<summary>4. Bluetooth configuration</summary>

 This is being accomplish with the use of [homebrew](https://github.com/Homebrew/homebrew), [homebrew-cask](https://github.com/caskroom/homebrew-cask), and the Mac Apple Store CLI [(MAS)](https://github.com/mas-cli/mas).

</details>


Applicable Devices
IP Phone 7800 Series
IP Phone 8800 Series

Software version
11.0.1
References

[Upgrade the Firmware on the Cisco IP Phone 7800 and 8800 Multiplatform Series through the Web Browser Command]
(https://www.cisco.com/c/en/us/support/docs/smb/collaboration-endpoints/cisco-ip-phone-7800-series/smb5431-upgrade-the-firmware-on-the-cisco-ip-phone-7800-and-8800-mul.html?referring_site=RE&pos=3&page=https://www.cisco.com/c/en/us/support/docs/unified-communications/unified-communications-manager-callmanager/213288-upgrade-ip-phone-firmware-individually.html)

## Licence

Cisco88xxSetup by Benoît H. Dicaire is shared under [CC-BY-SA-4.0](https://github.com/bhdicaire/solarized/raw/master/LICENCSE). This licence is recommended by [Choose a License.com](https://choosealicense.com/) for non-software material such as documentation and media.


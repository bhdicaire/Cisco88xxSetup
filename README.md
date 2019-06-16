![Cisco88xxSetup logo](https://github.com/bhdicaire/Cisco88xxSetup/raw/master/img/logo.png)

You’ve been there too — setting up a new IP Phone can be an ad-hoc, manual, and time-consuming process.

So you got your hands on a Cisco 88xx MPP Phone and now you want to get it up and running in next to no time.

It took too much time too setup the phone especially the firmware update. The information available online was either overly complex and/or incomplete.

My objective is to fully document my installation and configuration with [VoIP.ms](https://VoIP.ms). Feel free to fork, and customize for your IP telephony ecosystem ...

## What problem does it solve and why is it useful?

CISCO ... are great but the configuration ...

## Procedure

<details>
<summary>1. Quick setup</summary>

 This is being accomplish with the use of [homebrew](https://github.com/Homebrew/homebrew), [homebrew-cask](https://github.com/caskroom/homebrew-cask), and the Mac Apple Store CLI [(MAS)](https://github.com/mas-cli/mas).

</details>

<details>

<summary>2. Update the firmware</summary>
1. https://www.ukvoipforums.com/viewtopic.php?f=21&t=1114

CISCO 8800 SERIES XMLDEFAULT.CNF.XML FILE

https://www.cisco.com/c/en/us/support/collaboration-endpoints/ip-phone-8800-series-multiplatform-firmware/tsd-products-support-series-home.html

</details>
<details>
<summary>3. SIP configuration</summary>
Connect and Login to the SPA504G Web Based Configuration Interface
Connect your PC to the SPA504G using its LAN side Ethernet port marked PC.
Login to the SPA504G web interface by entering its LAN gateway IP address into your Web Browser using its DHCP assigned address (In my case, it's 192.168.1.2).
By default, you will be landing on and viewing the SPA504G "Info" page, in "Basic" view. By default, there are no User or Admin passwords required to connect and login to the SPA504G

In Cisco Unified Communications Manager Administration, select Device > Phone.

Step 2	
Locate the phone that you need to set up.

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

## Licence

Cisco88xxSetup by Benoît H. Dicaire is shared under [CC-BY-SA-4.0](https://github.com/bhdicaire/solarized/raw/master/LICENCSE). This licence is recommended by [Choose a License.com](https://choosealicense.com/) for non-software material such as documentation and media.


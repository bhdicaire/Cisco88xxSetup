![Cisco88xxSetup logo](https://github.com/bhdicaire/Cisco88xxSetup/raw/master/img/logo.png)

Cisco IP Phone 8861 Setup

You’ve been there too — setting up a new computer can be an ad-hoc, manual, and time-consuming process.

So you got your hands on a Cisco SPA525G or SPA525G2 and now you want to get it up and running in next to no time.

I wasn't happy with any of the automated setup that I came across. They were either overly complex or were missing features that I really wanted.

My objective is to fully automate macOS installation and configuration using Ansible. Lots of stuff in here you probably don't need, and some that needs personalization for your system ... So feel free to fork, and customize.

## What problem does it solve and why is it useful?

Setup a Mac up with everything configured properly with easy-to-understand instructions that automate the installation and configuration from the [bare metal](https://github.com/bhdicaire/macSetup/blob/master/doc/bareMetal.md).

## Procedure

details>
<summary>Quick setup</summary>

 This is being accomplish with the use of [homebrew](https://github.com/Homebrew/homebrew), [homebrew-cask](https://github.com/caskroom/homebrew-cask), and the Mac Apple Store CLI [(MAS)](https://github.com/mas-cli/mas).

</details>

<details>

<summary>Update the firmware</summary>
1. https://www.ukvoipforums.com/viewtopic.php?f=21&t=1114

CISCO 8800 SERIES XMLDEFAULT.CNF.XML FILE

https://www.cisco.com/c/en/us/support/collaboration-endpoints/ip-phone-8800-series-multiplatform-firmware/tsd-products-support-series-home.html

</details>
<details>
<summary>Dock Configuration</summary>
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


## Licence

Cisco88xxSetup by Benoît H. Dicaire is shared under [CC-BY-SA-4.0](https://github.com/bhdicaire/solarized/raw/master/LICENCSE). This licence is recommended by [Choose a License.com](https://choosealicense.com/) for non-software material such as documentation and media.


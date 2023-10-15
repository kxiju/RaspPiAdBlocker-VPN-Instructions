# RaspPiAdBlocker-VPN-Tutorial
Minimal Setup Requirements
 - A computer connected to your local network
 - Access to your wifi-/ router (in my case it was, Google Nest Wifi)
 - Raspberry Pi 4 (preferably, 2GB or 4GB)
 - USB-C Charger (5.1V / 3.0A DC)
 - Raspberry Pi 4 Case
 - MicroSD Card (preferably, high endurance kind; 16GB or more) or, alternatively, USB Flash Drive

Required Skills
 - Install software on a Linux OS
 - Change the settings of your local wifi-router
 - Execute system commands on Terminal/Command-prompt

Step 1: Setup the MicroSD Card or USB Drive
  Connect the MicrosSD card or USB Flash Drive to a computer
  Download and install Raspberry Pi Imager to your computer with an SD card reader or USB Flash Drive: Windows | macOS | Ubuntu Linux
  Open Raspberry Pi Imager
  Click on “Choose OS”
  Click on “Rapberry Pi OS”
  Press Ctrl + Shift + X
  On Advance Options screen, select “Enable SSH” option. 
  Also, check “Use password authentication”. 
  “Set password for ‘pi’ user” as raspberry. Or, set a password that you can remember. We need the password to connect with the board. 
  *Note: we will be accessing Raspberry Pi using SSH (No separate monitor/display required to connect).
  Check Set Locale Settings. Enter the appropriate Time Zone and Keyboard layout information.
  Click on the “Save” button
  Click on “Choose Storage” and select the MicroSD card (or, USB Drive)
  After selecting the MicroSD card or USB Drive, Click on “Write” button. You may see a warning dialog “All existing data on … will be erased. Are you sure you want to continue?”. Click on the “Yes” button.
  You may notice a progress-bar. If everything goes well, you should see “Write Successful” dialog. Click on “Continue” button and remove the MicroSD card (or, USB Drive).

Step 2: Connect Raspberry Pi
  Insert the MicroSD Card containing Raspberry Pi OS image created in previous step. (or, connect USB Drive in USB Port — Only one of these is needed)
  Connect your router and Raspberry Pi board with Ethernet cable. 
    *In case if you doesn’t have a ethernet cable or, if your router doesn’t have empty ethernet port, you can utilize the wifi connection. To utilize wifi, you must have set wifi SSID and password credentials while creating the image.
  Connect Raspberry Pi with USB-C charger and then connect charger to a power supply. 
    *Note: you must not touch the Raspberry Pi board after it is connected to the USB-C charger to avoid electric shock unless you have turned off the power.
  Look at your router’s manual, and change the router settings to reserve an IP address for Raspberry Pi. Note down the IP address.
  Open your computer which should be on the same local network.
  Mac/Linux: Open terminal application. We will use ssh pi@<ip_address>for example pi@192.168.86.28command to connect to the Raspberry Pi. Replace <ip_address> with the IP address that you reserved in previous step. When the connection works, you will see a security/authenticity warning. Type yes to continue. You will only see this warning the first time you connect.
  Windows: Download and install Putty application. Enter pi@<ip_address> for example pi@192.168.86.28under Host Name field. Click “Open” button. Also, click on “Yes” button when Security alert dialog is presented. The default login for Raspberry Pi OS is pi with the password raspberry.

Step 3: Configure Raspberry Pi
  On first time login to Respberry Pi, you should see “Raspberry Pi configuration tool” with options. In case you don’t see it, simply run command sudo raspi-config after SSH login. When password is asked, enter the password as raspberry
  You may choose to configure Wireless settings: 1 System Options > S1 Wireless LAN if you want to give wireless access to Raspberry Pi
  (Optional) You may choose to set a new SSH/VNC password using: 1 System Options > S3 Password if you want to set a new password to Raspberry Pi. Note: After changing to the new password, you must use the same password for SSH/VNC connections. It’s a best practice to change the default password; please do it.
  Press Esc key a few times to exit from the Raspberry Pi System Configuration.

Step 4:Ad blocker setup on Raspberry Pi
  Run the following commands from SSH client. You will download AdGuard application and extract it.
    sudo apt update
    sudo apt full-upgrade
    wget https://static.adguard.com/adguardhome/release/AdGuardHome_linux_arm.tar.gz
    tar xvf AdGuardHome_linux_arm.tar.gz
  Install AdGuardHome
    cd ~/AdGuardHome
    sudo ./AdGuardHome -s install
  When you run AdGuard Home for the first time, it will start listening to 0.0.0.0:3000 and prompt you to open it in your browser:
    AdGuard Home is available on the following addresses:
    Go to http://127.0.0.1:3000
    Go to http://X.X.X.X:3000
  You will go through the initial configuration wizard. Note down the IP address of DNS server. It should be same as the reserved IP address that we have been using so far (for SSH access etc.)
  Set Username and Password for AdGuard Home application. Note: Don’t use the same username and password that you have used for Raspberry Pi system user pi (for security purposes).
  Open the preferences for your router. Usually, you can access it from your browser via a URL (like http://192.168.0.1/ or http://192.168.1.1/). You may be asked to enter the password. If you don’t remember it, you can often find the password on a sticker on the router. Some routers require a specific application, which in that case should be already installed on your computer/phone.
  Find the DHCP/DNS settings. Look for the “DNS” letters next to a field which allows two sets of numbers, each broken into four groups of one to three digits.
  Enter your AdGuard Home server IP addresses (Raspberry Pi IP address) there.
    *Note: Different for every router
  At this point you can access the AdGuard application by accessing link http://<raspberry_pi_ip_address>
  Enter the username and password. Update General Settings and DNS settings.
  For the Upstream DNS Servers, please review https://kb.adguard.com/en/general/dns-providers and use the appropriate Upstream DNS server. If you want to take simplest route, just enter
    1.1.1.1
    1.0.0.1
    208.67.222.222
    208.67.220.220
  For Malware and adult content blocking, enter the following IP addresses (or, the other such IP addresses listed here)
    1.1.1.3
    1.0.0.3
    208.67.222.123
    208.67.220.123
  Save it.
  Configure DNS blocklists. Click on Filters > DNS blocklists. Choose blocklists as per your need.


Congratulations! You have successfully achieved the goal. You would notice that most of Ads are gone from the websites. :)

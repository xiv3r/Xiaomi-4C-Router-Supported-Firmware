# Xiaomi-Router-4C-Firmwares
All firmwares that support Xiaomi Router 4C


# Process

1. Unpack OpenWRTInvasion and go to its folder, where we execute the command to install the necessary modules (I didn’t install anything new on Linux):

       pip install -r requirements.txt

And let's start hacking:
        
      python3 remote_command_execution_vulnerability.py

The script will ask for the ip of the router (192.168.31.1 - if you did not change the standard ip of the router to your own) and the current password, after which it will hack and upload the telnet server to the router.
If the utility reported that everything is fine, go to
the Firmware.

Rename the firmware file shorter (less typing), in all instructions it is firmware.bin and upload the resulting file using FileZilla to the / tmp folder on the router.

Connection parameters: ip 192.168.31.1 (if you did not change the standard ip of the router to your own) login: root password: root
We connect to the router via telnet (putty now rules), the connection parameters are the same.
In the terminal, execute 2 commands in sequence:
    
      cd /tmp
     
- to go to the folder with the firmware

      mtd -e OS1 -r write firmware.bin OS1
  
- the firmware itself, the process will take a few minutes, after which the router will reboot itself.
After the reboot, I turned off the power for a while and turned it on for a clean boot.
If the previous steps could be performed via wifi, now only the wire, wifi is turned off by default, the router address has changed to 192.168.1.1, you can also use https://openwrt
Next, go to the web interface without a password and make your settings. Setting up OpenWrt is not difficult and this is a separate issue.
For fine-tuning wifi, especially in apartment buildings, I recommend the article: How to set up Wi-Fi correctly

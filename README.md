# Xiaomi-Router-4C-Firmwares

Firmware Download: https://github.com/xiv3r/Xiaomi-Router-4C-Firmwares/releases/tag/v1


- Note: one mistake will bricked your router, do at your own risk!

  Recovery: https://github.com/xiv3r/Xiaomi-Router-4C-CH341A-flasher 
  
# Docker Build

    docker build -t openwrtinvasion https://github.com/acecilia/OpenWRTInvasion.git
    docker run --network host -it openwrtinvasion


- Note: Reset your router and configure connect the lan cable then proceed to the process
 

# Process

- Unpack OpenWRTInvasion and go to its folder, where we execute the command to install the necessary modules

      git clone https://github.com/acecilia/OpenWRTInvasion.git

      cd OpenWRTInvasion

      pip install -r requirements.txt

- And let's start Exploiting:
        
      python remote_command_execution_vulnerability.py

- Gateway IP: 192.168.31.1 enter and type 1 enter


- Connection for telnet
  
      telnet 192.168.31.1

login: root password: root

- After successful login
    
      cd /tmp

# Open new terminal

     python -m http.server

     ifconfig

![Screenshot_20230809_190816](https://github.com/xiv3r/Xiaomi-Router-4C-Firmwares/assets/117867334/0455d982-643c-443d-b995-3c25fd956a4d)

open chrome and type 192.168.1.211:8000 

right click the file and copy link address

![Screenshot_20230809_190932](https://github.com/xiv3r/Xiaomi-Router-4C-Firmwares/assets/117867334/9e490cf6-0626-47f0-b8e4-5cfc6493c559)

- Go back to the previous terminal

  cd /tmp
  
- now import the firmware file to the /tmp directory

      cd /tmp
  
      wget http://192.168.1.211:8000/Downloads/padavanklhjzlfhkjhdfjjsfdzfhjdxf.trx -O padavan.bin
 
- To flash the firmware

      ls

  for .bin
  
      mtd -e OS1 -r write padavan.bin OS1

  for .trx

      mtd -e OS1 -r write padavan.trx OS1
  
- The process will take a few minutes, after which the router will reboot itself. After the reboot, connect the lan and configure to your computer
![Screenshot_20230809_191639](https://github.com/xiv3r/Xiaomi-Router-4C-Firmwares/assets/117867334/335052dd-a7c4-4cb3-a03f-59b397f9bdb5)

- For switching padvan, xwrt, openwrt ,immortalwrt

      mtd -r write /tmp/openwrt/xwrt/padavan/immortal.bin firmware

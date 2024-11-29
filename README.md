# <h1 align="center"> Supported Firmware For Xiaomi 4C Router </h1>

[Firmware Download](https://github.com/xiv3r/Xiaomi-Router-4C-Firmwares/releases/tag/v1)

`Note:` One mistake will bricked your router forever, do at your own risk!

[Link for Recovery](https://github.com/xiv3r/Xiaomi-Router-4C-CH341A-flasher)
  

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

login: `root` password: `root`

- After successful login
    
      cd /tmp

# Open a new terminal

     python -m http.server

     ifconfig

![Screenshot_20230809_190816](https://github.com/xiv3r/Xiaomi-Router-4C-Firmwares/assets/117867334/0455d982-643c-443d-b995-3c25fd956a4d)

- Open chrome and type the ip like (192.168.1.211:8000)

- right click the file and copy link address

![Screenshot_20230809_190932](https://github.com/xiv3r/Xiaomi-Router-4C-Firmwares/assets/117867334/9e490cf6-0626-47f0-b8e4-5cfc6493c559)

- Go back to the previous terminal

  cd /tmp
  
- now import the firmware file to the /tmp directory

      cd /tmp
  
      wget http://192.168.1.211:8000/Downloads/padavanklhjzlfhkjhdfjjsfdzfhjdxf.trx -O padavan.bin

- Another method is using scp

      cd Download

      scp padavan.bin root@192.168.31.1:/tmp
 
- To flash the firmware

      ls

  for .bin
  
      mtd -e OS1 -r write /tmp/padavan.bin OS1

  for .trx

      mtd -e OS1 -r write /tmp/padavan.trx OS1
  
- The process will take a few minutes, after which the router will reboot itself. After the reboot, connect the lan and configure to your computer
![Screenshot_20230809_191639](https://github.com/xiv3r/Xiaomi-Router-4C-Firmwares/assets/117867334/335052dd-a7c4-4cb3-a03f-59b397f9bdb5)

- Switching to padvan, xwrt, openwrt, pcwrt, keenetic and immortalwrt

      cd /tmp

      wget https://192.168.1.xxx/padvan.bin
  
      mtd -e firmware -r write /tmp/openwrt|xwrt|padavan|immortal.bin firmware

- if the router will brick reflash to its stock 16mb firmware and invade again using openwrtinvasion

# Hardware Mod - USB Port

- See the photos for break down of where to solder etc. On picture are shown all soldier points for desired pins with markings. Also you must connect 15kOhm resistors to ground from D+ and D- lines.

![Download_mi_router_4c_usb_hardware_modifications](https://github.com/xiv3r/Xiaomi-Router-4C-Firmwares/assets/117867334/810a6404-0b83-47c2-829d-39629a64d1ca)

![Download_IMG_7995_12229](https://github.com/xiv3r/Xiaomi-Router-4C-Firmwares/assets/117867334/abdbfab0-59f9-473e-8d81-dce1699c161a)
![Download_IMG_7995_12225](https://github.com/xiv3r/Xiaomi-Router-4C-Firmwares/assets/117867334/ce678749-24d0-4cba-b57e-d34201118090)

![Download_IMG_7991_12223](https://github.com/xiv3r/Xiaomi-Router-4C-Firmwares/assets/117867334/89a233f3-cba0-4407-b28f-360a7052ea49)

![Download_IMG_7986_12230](https://github.com/xiv3r/Xiaomi-Router-4C-Firmwares/assets/117867334/19b0fcae-9a39-410c-832f-01a63738da2e)

![Download_IMG_7983_12218](https://github.com/xiv3r/Xiaomi-Router-4C-Firmwares/assets/117867334/93d2aaa8-3beb-44f8-83dc-580a7915c0aa)

- Software mod

Simple hardware mod does not enable USB, you must enable OHCI and AHCI in board description file and compile appropriate firmware. Board description file is on location

         /{your openwrt source location}/openwrt/target/linux/ramips/dts/mt7628an_xiaomi_mi-router-4c.dts

- In this file change:

      &ehci {
	  status = "disabled";
      };
      &ohci {
	  status = "disabled";
      };

  to

      &ehci {
      status = "okay";
      };
      &ohci {
      status = "okay";
      };

- Enable usb kernel module support in “make menuconfig”, compile firmware file and flash it.

- You can use 5V power supply from router for powering on USB, but take care because its only 1A of current charge if you connect some power hungry USB peripheral it will make router unstable.

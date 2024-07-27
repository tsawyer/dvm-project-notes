# DVMHost for DVM V24 Board 

This is how to build and configure DVMHost for use with the [DVM V24 board](https://store.w3axl.com/products/dvm-v24-usb-converter-for-v24-equipment) on a Quantar repeater.

Assumes:
* You have a Debian 12 OS install with root access on a computer which the DVM V24 board will plug into. 
* There is a known working ENF for DVMHost to login to either on this same or another computer. 

## Clone

As root:

```
apt install git g++ cmake
cd /usr/src
git clone https://github.com/DVMProject/dvmhost.git
git clone https://github.com/tsawyer/dvm-project-notes.git
cd dvmhost
```

## Compile and Install DVMHost

Follow the instructions at [DVMProject README.md](https://github.com/DVMProject/dvmhost/blob/master/README.md).

* Do install the dependicies.
* Don't install the cross compilers
* No options are needed for cmake. Just do `cmake ..` That compiles the project C code. It doesn't take long.
* The `make` command builds the project and may take a long time.
* Finally do `make strip` and `make old_install`. This removes debug code and copies the project to `/opt/dvm`.

This complete the build of DVMHost. Next  

## Compile V24 Board Firmware

These steps are from [github.com/DVMProject/dvmv24](https://github.com/DVMProject/dvmv24). Read that first then come back here.
If your DVM V24 board has current firmware skip down to **DVM Host Configuration**.
If the pre-built [binary firmware](https://github.com/DVMProject/dvmv24/releases) is current skip down to **Flash V24 Board Firmware**

### Compile Firmware
The ARM toolchain is needed to build the latest firmware.  for this: On Debian and derivatives, 
the package you’re looking for is gcc-arm-none-eabi:  Thank you [Stack Exchange](https://unix.stackexchange.com/questions/377345/installing-arm-none-eabi-gcc).

```
apt install gcc-arm-none-eabi
```

With the ARM tool chain installed, build the firmware:

```
cd /usr/src
git clone https://github.com/DVMProject/dvmv24.git
cd dvm24/fw
make
```

### Flash V24 Board Firmware

To flash the V24 board firmware a STlink programmer is needed. Programmers are inexpensive and available from Amazon, DigiKey, Mouser, eBay and etc. 

Connect the programmer to the V24 board. The V24 board pins are labled on the underside of the circuit board. 

Assuming the firmware was built as above: 
```
make flash
```


## The steps below are obsolete!

The DVM Project no longer builds dvmdfsi. DFSI has merged into dvmhost. 
DVMHost support for DFSI requires V24 board FM 2.0. It's not in your board unless it's been flashed.
This document will be updated once I get my STLink programmer and successfully flash a V24 board. 

## DMV Host Configuration

* Copy the configuration file `cp /usr/src/dvm-project-notes/config/dfsi.yml /opt/dvm/`.
* Edit the configuration file `nano /opt/dvm/dfsi.yml`.
  * Under `network:` change `identity: MYCALL-01` to your call sign-ssID or site name.
  * Under `network:` change `peerID: 1234` to a peer ID cordinated with your admin (may be you).
  * Under `network:` change `address: xxx.xxx.xxx.xxx` to the desired FNE IP address provided by your admin.
  * Under `network:` change `password: PASSWORD to the password provided by your admin.
  * Under `serial:` change the `port: "/dev/ttyACM0"`. To find port insure the V24 board is connected to a USB port. Then do `ls -l /dev/ttyAMC`. 
 
## Testing

Launch DFSI in the foreground `/opt/dvm/bin/dvmdfsi -f -c /opt/dvm/dfsi.yml`. You should see it login to the FNE after a few moments.

```
I: 2024-07-24 11:01:24.686
                                        .         .
8 888888888o.   `8.`888b           ,8' ,8.       ,8.
8 8888    `^888. `8.`888b         ,8' ,888.     ,888.
8 8888        `88.`8.`888b       ,8' .`8888.   .`8888.
8 8888         `88 `8.`888b     ,8' ,8.`8888. ,8.`8888.
8 8888          88  `8.`888b   ,8' ,8'8.`8888,8^8.`8888.
8 8888          88   `8.`888b ,8' ,8' `8.`8888' `8.`8888.
8 8888         ,88    `8.`888b8' ,8'   `8.`88'   `8.`8888.
8 8888        ,88'     `8.`888' ,8'     `8.`'     `8.`8888.
8 8888    ,o88P'        `8.`8' ,8'       `8        `8.`8888.
8 888888888P'            `8.` ,8'         `         `8.`8888.

Digital Voice Modem (DVM) DFSI V.24/UDP Peer 04.02C (R04C02 cd579eea) (built Jul 19 2024 21:17:24)
Copyright (c) 2024 Patrick McDonnell, W3AXL and DVMProject (https://github.com/dvmproject) Authors.
>> DFSI Network Peer

I: 2024-07-24 11:01:24.687 Network Parameters
I: 2024-07-24 11:01:24.687     Identity:  WD6AWP-01
I: 2024-07-24 11:01:24.687     Peer ID:   448040
I: 2024-07-24 11:01:24.687     Address:   149.248.19.173
I: 2024-07-24 11:01:24.687     Port:      62031
I: 2024-07-24 11:01:24.687     Encrypted: no
I: 2024-07-24 11:01:24.687 Serial Parameters
I: 2024-07-24 11:01:24.687     Port Type:   uart
I: 2024-07-24 11:01:24.687     Port:        /dev/ttyACM0
I: 2024-07-24 11:01:24.687     Baudrate:    115200
I: 2024-07-24 11:01:24.687     RT/RT:       Enabled
I: 2024-07-24 11:01:24.687     DIU Flag:    Disabled
I: 2024-07-24 11:01:24.687     Jitter Size: 200 ms
I: 2024-07-24 11:01:24.687     Debug:       Disabled
I: 2024-07-24 11:01:24.687     Trace:       Disabled
I: 2024-07-24 11:01:24.687 (SERIAL) Opening port /dev/ttyACM0 at 115200 baud
I: 2024-07-24 11:01:24.688 DFSI Parameters
I: 2024-07-24 11:01:24.688     Mode: 2 (V24 DFSI to FNE)
I: 2024-07-24 11:01:24.688     P25 Buffer Size: 3060 bytes
I: 2024-07-24 11:01:24.688     Call Timeout:    200 ms
I: 2024-07-24 11:01:24.688 (HOST) [ OK ] DFSI is up and running on Linux 6.1.0-23-amd64 x86_64
D: 2024-07-24 11:01:34.695 (NET) PEER 448040 RPTL ACK, performing login exchange, remotePeerId = 9000100
D: 2024-07-24 11:01:34.700 (NET) PEER 448040 RPTK ACK, performing configuration exchange, remotePeerId = 9000100
M: 2024-07-24 11:01:34.711 (NET) PEER 448040 RPTC ACK, logged into the master successfully, remotePeerId = 9000100
M: 2024-07-24 11:01:34.711 (NET) PEER 448040 RPTC ACK, master commanded alternate port for diagnostics and activity logging, remotePeerId = 9000100
```
If that looks good then control-c out of dfsi.

## Install DFSI Service

Install the service with these commands:

```
cp /usr/src/dvm-project-notes/config/dvmdfsi.service /etc/systemd/system/dvmdfsi.service
systemctl daemon-reload
systemctl enable dvmdfsi.service
systemctl start dvmdfsi.service
```
Use `systemctl status dvmdfsi.service` to see if dfsi is running.

Use `journalctl -u dvmdfsi -f` to monitor the log. 

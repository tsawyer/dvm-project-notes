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

or to update

```
cd /usr/src/dvmhost
git pull
```

## Compile and Install DVMHost

Follow the instructions at [DVMProject README.md](https://github.com/DVMProject/dvmhost/blob/master/README.md).

* Do install the dependicies.
* Don't install the cross compilers
* No options are needed for cmake. Just do `cmake ..` That compiles the project C code. It doesn't take long.
* The `make` command builds the project and may take a long time.
* Finally do `make strip` and `make old_install`. This removes debug code and copies the project to `/opt/dvm`.

This complete the build of DVMHost.

## Compile and Flash V24 Board Firmware

These steps are from [github.com/DVMProject/dvmv24](https://github.com/DVMProject/dvmv24). You should read it.

If your DVM V24 board has current firmware skip down to **DVM Host Configuration**.
If the pre-built [binary firmware](https://github.com/DVMProject/dvmv24/releases) is current skip down to **Flash Firmware**.
Chances are neither is true and you'll need to build and flash new firmware.

### Compile Firmware
The ARM toolchain is needed to build the latest firmware. On Debian and derivatives, 
the package you’re looking for is gcc-arm-none-eabi, thank you [Stack Exchange](https://unix.stackexchange.com/questions/377345/installing-arm-none-eabi-gcc).

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

### Flash Firmware

To flash the V24 board firmware a STlink programmer is needed. Programmers are inexpensive and available from Amazon, DigiKey, Mouser, eBay and etc. 

Connect four wires from the programmer to the V24 board. The V24 board pins are **labled on the underside** of the circuit board. 
 * 3.3 Volts
 * GND
 * DIO
 * CLK

Install the flash program: `apt install stlink-tools`

Assuming the firmware was built as above: 
```
/usr/src/dvmv24/fw/
make flash
```
You should see
```
st-flash write build/DVM-V24-stm32f103.bin 0x08000000
st-flash 1.7.0
2024-07-27T18:35:18 INFO common.c: F1xx Medium-density: 20 KiB SRAM, 64 KiB flash in at least 1 KiB pages.
file build/DVM-V24-stm32f103.bin md5 checksum: 11432cfce54d9407e80ef4ed7ce283, stlink checksum: 0x0034350d
2024-07-27T18:35:18 INFO common.c: Attempting to write 33804 (0x840c) bytes to stm32 address: 134217728 (0x8000000)
2024-07-27T18:35:18 INFO common.c: Flash page at addr: 0x08000000 erased
... <snip> ...
2024-07-27T18:35:19 INFO common.c: Flash page at addr: 0x08008400 erased
2024-07-27T18:35:19 INFO common.c: Finished erasing 34 pages of 1024 (0x400) bytes
2024-07-27T18:35:19 INFO common.c: Starting Flash write for VL/F0/F3/F1_XL
2024-07-27T18:35:19 INFO flash_loader.c: Successfully loaded flash loader in sram
2024-07-27T18:35:19 INFO flash_loader.c: Clear DFSR
 34/ 34 pages written
2024-07-27T18:35:21 INFO common.c: Starting verification of write complete
2024-07-27T18:35:21 INFO common.c: Flash written and verified! jolly good
```
# NOTICE
**Below here is still being updated!** Please ignore.

## DMV Host Configuration

* Copy the configuration file `cp /usr/src/dvm-project-notes/config/config.yml /opt/dvm/`.
* Edit the configuration file `nano /opt/dvm/config.yml`.

* Under `network:` change `identity: MYCALL-01` to your call sign-ssID or site name.
  * Under `network:` change `peerID: 1234` to a peer ID cordinated with your admin (may be you).
  * Under `network:` change `address: xxx.xxx.xxx.xxx` to the desired FNE IP address provided by your admin.
  * Under `network:` change `password: PASSWORD to the password provided by your admin.
  * Under `serial:` change the `port: "/dev/ttyACM0"`. To find port insure the V24 board is connected to a USB port. Then do `ls -l /dev/ttyAMC`. 
 
## Testing

Launch DVMHost in the foreground `/opt/dvm/bin/dvmhost -f -c /opt/dvm/config.yml`. You should see it login to the FNE after a few moments.

```
If that looks good then control-c out of dvmhost.

## Install DVMhost Service

Install the service with these commands:

```
cp /usr/src/dvm-project-notes/config/dvmdfsi.service /etc/systemd/system/dvmdfsi.service
systemctl daemon-reload
systemctl enable dvmdfsi.service
systemctl start dvmdfsi.service
```
Use `systemctl status dvmdfsi.service` to see if dfsi is running.

Use `journalctl -u dvmdfsi -f` to monitor the log. 

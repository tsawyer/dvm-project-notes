# DVMV24 Flash Firmware

To flash the V24 board firmware a ST-link V2 programmer is needed. Programmers are inexpensive and available from Amazon, DigiKey, Mouser, eBay and etc.

Connect four wires from the programmer to the V24 board. The V24 board pins are **labled on the underside** of the circuit board.
 * 3.3 Volts
 * GND
 * DIO
 * CLK

Do not connect V24 board USB-C or Quantar cables.

### If first time
If this it the first time you've flashed, install st-link flash programer: `apt install stlink-tools`

### If you compiled new firmware
Assuming the firmware was built in `/usr/src/dvmv24/fw/`:

```
cd /usr/src/dvmv24/fw/
```

### If you download the new firmware
If you downloaded new firmware from `https://github.com/DVMProject/dvmv24/releases/tag/v2.1`.

Put the new firmware in the build directory `/usr/src/dvmv24/fw/build`. 

### Flash
With your programmer connected
and the .bin file in the build directory above 

`cd /usr/src/dvmv24/fw/` and then do `make flash`

You should see:

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

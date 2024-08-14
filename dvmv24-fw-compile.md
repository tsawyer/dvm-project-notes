# Compile DVM V24 Board Firmware

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
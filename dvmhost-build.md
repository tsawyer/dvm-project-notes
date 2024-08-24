# DVMHost for DVM V24 Board

2024-08-18 0217Z

This is how to build and configure DVMHost for use with the [DVM V24 board](https://store.w3axl.com/products/dvm-v24-usb-converter-for-v24-equipment) on a Quantar repeater.

If you want to update see [dvmhost-update](dvmhost-update.md).

Assumes:
* You have a Debian 12 x86_64 install with root access on a computer which the DVM V24 board will plug into.
* There is a known working ENF for DVMHost to login to either on this same or another computer.

## Install Required Tools

```
apt install git g++ cmake
apt-get install libasio-dev libncurses-dev libssl-dev
```

## Clone

As root:

```
cd /usr/src
git clone https://github.com/DVMProject/dvmhost.git
git clone https://github.com/tsawyer/dvm-project-notes.git
cd dvmhost
```

## Compile and Install DVMHost

Follow the instructions at [DVMProject README.md](https://github.com/DVMProject/dvmhost/blob/master/README.md).

* Do install the dependicies (Required Tools)
* Don't install the cross compilers
* Run the following commands one at a time. Fix any errors before continuing.

```
cd /usr/src/dvmhost
mkdir build
cd build
cmake ..
make
make strip
make old_install
```

Explanation:
* The cmake followed by a space and two dots, like this `cmake ..` compiles the project C code. It doesn't take long.
* The `make` command builds the project and may take a long time.
* Finally `make strip` and `make old_install` removes debug code and copies the project to `/opt/dvm`.

This complete the build of DVMHost.

## DVM Host Configuration

First, change directory and copy two files:
```
cd /opt/dvm/
cp talkgroup_rules.example.yml talkgroup_rules.yml
cp /usr/src/dvm-project-notes/config/config.yml config.yml
```

Next, edit the configuration file `nano config.yml`.

You need to change only ***5 settings*** as indicated by **CHANGE** in bold uppercase.
Do not change any other settings.

### DMVHost Config File Notes

This documents the changes I've made from the DVM Project defaults as of 7/28/24.
Remember, you change the only bold uppercase **CHANGE** settings. I've already changed the other settings.

* Insure `daemon: true`
* Under `log:`
  * Change `fileLevel:` to 6
  * Change `filePath:` to /opt/dvm/log
  * Change `activityFilePath:` to /opt/dvm/log
* Under `network:`
  * **CHANGE** `id:` to admin provided peerID. Must be unique. Your freq may do.
  * **CHANGE** `address:` to the FNE IP address provided by your admin.
  * **CHANGE** `password:` to the FNE password provided by your admin.
* Under `protocols:`
  * Under `dmr:` change `enable:` to false
  * Under `p25:` insure `enable:` is true
  * Under `nxdn:` insure `enable:` is false
* Under `system:`
  * **CHANGE** `idenity:` to YOUR CALL SIGN
  * **CHANGE** `info:` optionally change the values.
* Under `cwId:`
  * Change `enable:` to false
* Under `modem:`
  * Under `protocol:` change `type:` to "uart"
  * Under `protocol:` change `mode:` to "dfsi"
  * Under `uart:` change the `port:` "/dev/ttyACM0" To find port insure the V24 board is connected to a USB port. Then do `ls -l /dev/ttyACM*`.
  * Under `dfsi:` change `diu:` to false
* Under `iden_table` change `file:` to /opt/dvm/iden_table.dat
* Under `radio_id:` change `file:` to /opt/dvm/rid_acl.dat
* Under `talkgroup_id:` change `file:` to /opt/dvm/talkgroup_rules.yml

## Testing

Launch DVMHost in the foreground `/opt/dvm/bin/dvmhost -f -c /opt/dvm/config.yml`. You should see it login to the FNE after a few moments.

If that looks good then control-c out of dvmhost.

## Install DVMhost Service

Install the service with these commands:

```
cp /usr/src/dvm-project-notes/config/dvmhost.service /etc/systemd/system
systemctl daemon-reload
systemctl enable dvmhost.service
systemctl start dvmhost.service
```
Use `systemctl status dvmhost.service` to see if dvmhost is running.

Use `tail -f /opt/dvm/log/DVM... ` to monitor operations.

# Quick Install

Quick install might be a stretch. This collects my other notes in to one place for what seems quicker to me. 

## Required Tools and libs

Must have:

`apt install git g++ cmake libasio-dev libncurses-dev libssl-dev`

## Optional Tools

My favorites, ymmv.

`apt install vim sudo htop zsh`

## Clone

Clone this repo. You need it locally. Notice we don't clone [DVMHost](https://github.com/DVMProject/dvmhost) because we install a prebuild binary and config. This version is for amd486.

```
cd /usr/src
git clone https://github.com/tsawyer/dvm-project-notes.git
```

## Install Binary and Config

Install the prebuild binaries and customized configuration. 

```
cd /usr/src/dvm-project-notes/tarball
tar xzvf dvmhost_R04Axx_amd64.tar.gz -C /opt
cp /usr/src/dvm-project-notes/config/config.yml /opt/dvm/

```

## Install udev rules 

This udev rule create an alias to /dev/ACM0 and /dev/ACM1 to work around a v.24 board reset issue. 

`cp /usr/src/dvm-project-notes/config/99_dvmv24.rules /etc/udev/rules.d/`

## DMVHost Configuration

Next, edit the custom configuration file with `nano /opt/dvm/config.yml` or your fav editor. These changes are needed to login to our FNE.

 * CHANGE `id:` to admin provided peerID. Must be unique. Your DMR ID (plus 2 digits if needed). Limit 9 characters. Numbers only.
 * CHANGE `address:` to the FNE IP address provided by your admin.
 * CHANGE `password:` to the FNE password provided by your admin.
 * CHANGE `identity:` to YOUR CALL SIGN or YOUR SITE (limit 8 characters)
 * Under `info:` optionally change the values.

## Test

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

Use `journalctl -u dvmhost -f` to monitor operations.



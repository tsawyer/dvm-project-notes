# WD6AWP dvm-project-notes
These notes are things I need to keep track of for the [DVM Project](https://github.com/DVMProject/dvmhost).
99.9% of this info was gleaned from the [DVM Project Discord Server](https://discord.gg/3pBe8xgrEz).
The folks on the DVM Discord and GitHub have nothing to do with what I have posted here and they don't support it.

## README Update 2026-01-29
README updated to install recent development DVM tarball and a development library.
 - Install development library `libdw-deb`.
 - Download and extract development tarball.
 - Install Wireguard per instructions.

# DVMHost Install
Do all this as root or with sudo.
 - The tarball name changes with updates. Grab the latest uncommented tarball.
```
cd ~
# Last known stable tarball. Use if the whole network converts.
# wget https://github.com/DVMProject/dvmhost/releases/download/2025-09-03/dvmhost-2025-09-03-amd64.tar.gz
# tar xzvf dvmhost-2025-09-03-amd64.tar.gz -C /opt

# We've had hosts stop receiving network traffic ("go to sleep")  with this tarball.
# wget https://github.com/DVMProject/dvmhost/releases/download/2025-12-03/dvmhost-2025-12-03-amd64.tar.gz
# tar xzvf dvmhost-2025-12-03-amd64.tar.gz

# We're currently using this tarball and additional library.
wget https://github.com/tsawyer/dvm-project-notes/raw/main/tarball/dvmhost_R05A04_dev_x86_64.tar.gz
tar xzvf dvmhost_R05A04_dev_x86_64.tar.gz -C /opt
apt install libdw-dev
```
 - Test for correct version installed.
```
/opt/dvm/bin/dvmhost -v
Digital Voice Modem (DVM) Host 05.04A (R05A04 a43efddc) (built Jan 26 2026 20:30:24)
Copyright (c) 2017-2026 Bryan Biedenkapp, N2PLL and DVMProject (https://github.com/dvmproject) Authors.
Portions Copyright (c) 2015-2021 by Jonathan Naylor, G4KLX and others
```
Make sure the version and hash are `R05A04 a43efddc`.

```
 - Copy examples:
```
cd /opt/dvm
cp rid_acl.example.dat rid_acl.dat
cp iden_table.example.dat iden_table.dat
cp talkgroup_rules.example.yml talkgroup_rules.yml
```
 - Contact author for DVMHost configuration boilerplate and instructions.
 - Contact author for Wireguard configuration boilerplate and instructions.
 - Create a place for the logs: `mkdir /var/log/dvm`
 - Normaly talkgroup rules come from the FNE so no changes to talkgroup_rules.yml are necessary.

 - Add udev rules:
```
cd /etc/udev/rules.d/
wget https://raw.githubusercontent.com/tsawyer/dvm-project-notes/main/config/99_dvmv24.rules
```
 - Reboot to activate these rules: `reboot`

 - Install the service:
```
cd /etc/systemd/system
wget https://raw.githubusercontent.com/tsawyer/dvm-project-notes/main/config/dvmhost.service
systemctl daemon-reload
```
 - Enable DVMhost to start at system boot: `systemctl enable dvmhost.service`.
 - Start DVMhost: `systemctl start dvmhost.service`.
 - View the DVMHost log: `journalctl -S today -u dvmhost -f`.
 - Add cron to remove logs older than 3 days: `crontab -e`
```
0 0 * * * /usr/bin/find /var/log/dvm/* -type f -mtime +3 -delete > /dev/null 2>&1
```
This completes the install. DVMHost should be running.

# DVMHost Troubleshoot
Stop the service and run in foreground and look for errors:
```
systemctl stop dvmhost
/opt/dvm/bin/dvmhost -f -c /opt/dvm/config.yml
```

# DVMHost Update
This updates the DVMProject amd64 binaries without having to compile it on each server.
 - If the tarball was previously downloaded the old tarball will not be overwritten. Instead the new tarball will be saved with a **.n** extension, where n equals the next higher download. Linux tar will extract the files with the .n extension if told to. For example `tar xzvf dvmhost_<CURRENT VERSION>.tar.gz<OPTIONAL .n> -C /opt`
 - The tarball name changes with updates. Be sure to check GitHub for the latest.
 - Grab the latest tarball and untar it per the install above. Then restart the service:
```
systemctl restart dvmhost.service
```
Tada!

# DVM-V24 Firmware
Latest [DVM V24 Board firmware](https://github.com/DVMProject/dvmv24) is required for DVMHost.

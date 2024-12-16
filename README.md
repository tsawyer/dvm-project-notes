# WD6AWP dvm-project-notes
These notes are things I need to keep track of for the [DVM Project](https://github.com/DVMProject/dvmhost).
99.9% of this info was gleaned from the [DVM Project Discord Server](https://discord.gg/3pBe8xgrEz).
The folks on Discord and GitHub have nothing to do with what I have posted here and they don't support it.

# DVMHost Install
Do all this as root or with sudo.
 - Grab the tarball, install the binaries and example configs:
```
cd ~
wget https://raw.githubusercontent.com/tsawyer/dvm-project-notes/main/tarball/dvmhost_R04Axx_amd64.tar.gz
tar xzvf dvmhost_R04Axx_amd64.tar.gz -C /opt
```
 - Copy examples and create a place for the logs:
```
cd /opt/dvm
cp config.example.yml config.yml
cp rid_acl.example.dat rid_acl.dat
cp talkgroup_rules.example talkgroup_rules.yml
mkdir /var/log/dvm
```
 - Edit [config.yml](https://github.com/tsawyer/dvm-project-notes/blob/main/config/config-edits.md).
 
 - Add udev rules: (reboot to activate these rules at some point)
```
cd /etc/udev/rules.d/
wget https://raw.githubusercontent.com/tsawyer/dvm-project-notes/main/config/99_dvmv24.rules
```

 - Install the service:
```
cd /etc/systemd/system
wget https://raw.githubusercontent.com/tsawyer/dvm-project-notes/main/config/dvmhost.service
systemctl daemon-reload
```
 - Enable DVMhost to start at system boot `systemctl enable dvmhost.service`.
 - Start DVMhost `systemctl start dvmhost.service`.
 - View the DVMHost log `journalctl -S today -u dvmhost -f`.
 - cron to remove logs older than 3 days:
```
crontab -e
0 0 * * * /usr/bin/find /var/log/dvm/* -type f -mtime +3 -delete > /dev/null 2>&1`
```
This complete the install. DVMHost should be running.

# DVMHost Troubleshoot
Stop the service and run in foreground and look for errors:
```
systemctl stop dvmhost
/opt/dvm/bin/dvmhost -f -c /opt/dvm/config.yml
``` 

# DVMHost Update
This updates the DVMProject amd64 binaries without having to compile it on each server.
 - Note: If the tarball was previously downloaded the old tarball will not be overwritten. Instead the new tarball will be saved with a **.n** extension, where n equales the next higher download. Linux tar will extract the files with the .n extension if told to. For example `tar xzvf dvmhost_R04Axx_amd64.tar.gz.1 -C /opt`
```
cd ~
wget https://raw.githubusercontent.com/tsawyer/dvm-project-notes/main/tarball/dvmhost_R04Axx_amd64.tar.gz
tar xzvf dvmhost_R04Axx_amd64.tar.gz -C /opt
systemctl restart dvmhost.service
```
Tada!

# DVM-V24 Firmware
Latest [DVM V24 Board firmware](https://github.com/DVMProject/dvmv24) is required for DVMHost.

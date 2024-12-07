# WD6AWP dvm-project-notes
These notes are things I need to keep track of for the [DVM Project](https://github.com/DVMProject/dvmhost).
99.9% of this info was gleaned from the [DVM Project Discord Server](https://discord.gg/3pBe8xgrEz).
The folks on Discord and GitHub have nothing to do with what I have posted here and they don't support it.

# DVMHost Install
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
 - Add [logrotate](https://github.com/tsawyer/dvm-project-notes/blob/main/config/logrotate.md) and [udev rules](https://github.com/tsawyer/dvm-project-notes/blob/main/config/udevrules.md).
 - Install the service:
```
cd /etc/systemd/system
wget https://raw.githubusercontent.com/tsawyer/dvm-project-notes/main/config/dvmhost.service
systemctl daemon-reload
```
 - Enable DVMhost to start at system boot `systemctl enable dvmhost.service`.
 - Start DVMhost `systemctl start dvmhost.service`.
 - View the DVMHost log `journalctl -S today -u dvmhost -f`.

This complete the install. DVMHost should be running.

# DVMHost Troubleshoot
Stop the service and run in foreground:
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

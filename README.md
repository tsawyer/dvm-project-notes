# WD6AWP dvm-project-notes
These notes are things I need to keep track of for the [DVM Project](https://github.com/DVMProject/dvmhost).
99.9% of this info was gleaned from the [DVM Project Discord Server](https://discord.gg/3pBe8xgrEz).
The folks on the DVM Discord and GitHub have nothing to do with what I have posted here and they don't support it.

# DVMHost Install
Do all this as root or with sudo.
 - The tarball name changes with updates. Be sure to check GitHub for the latest.
 - Grab the latest tarball, install the binaries and example configs:
```
cd ~
#wget https://github.com/DVMProject/dvmhost/releases/download/2025-09-03/dvmhost-2025-09-03-amd64.tar.gz
wget https://github.com/DVMProject/dvmhost/releases/download/2025-12-03/dvmhost-2025-12-03-amd64.tar.gz
tar xzvf dvmhost-2025-12-03-amd64.tar.gz -C /opt
```
 - Copy examples:
```
cd /opt/dvm
cp config.example.yml config.yml
cp rid_acl.example.dat rid_acl.dat
cp iden_table.example.dat iden_table.dat
cp talkgroup_rules.example.yml talkgroup_rules.yml
```
 - Create a place for the logs: `mkdir /var/log/dvm`
 - Edit [config.yml](https://github.com/tsawyer/dvm-project-notes/blob/main/config/config-edits.md). We typically provide a template config for our users requiring only minor changes.
 - Edit talkgroup_rules.yml to add and/or remove rules as desired. Normaly talkgroup rules come from the FNE so this step is optional.

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
 - If the tarball was previously downloaded the old tarball will not be overwritten. Instead the new tarball will be saved with a **.n** extension, where n equales the next higher download. Linux tar will extract the files with the .n extension if told to. For example `tar xzvf dvmhost_xxxxx_amd64.tar.gz.1 -C /opt`
 - The tarball name changes with updates. Be sure to check GitHub for the latest.
 - Grab the latest tarball and untar it per the install above. Then restart the service:
```
systemctl restart dvmhost.service
```
Tada!

# DVM-V24 Firmware
Latest [DVM V24 Board firmware](https://github.com/DVMProject/dvmv24) is required for DVMHost.

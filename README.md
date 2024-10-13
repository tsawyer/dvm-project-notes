# WD6AWP dvm-project-notes
This repo is for our group of [DVM Project](https://github.com/DVMProject/dvmhost) users.
99.9% of this info was gleaned from the [DVM Project Discord Server](https://discord.gg/3pBe8xgrEz).
The folks on Discord and GitHub have nothing to do with what I have posted here and don't support it.

## Quick Update
This updates the DVMProject binaries without having to compile it on each server. It's for adm64 systems only. 

Grab and install the tarball. For updating this is all that is needed.
```
wget https://raw.githubusercontent.com/tsawyer/dvm-project-notes/main/tarball/dvmhost_R04Axx_amd64.tar.gz
```
then
```
tar xzvf dvmhost_R04Axx_amd64.tar.gz -C /opt
systemctl restart dvmhost
```
That's it. Update is complete.

## New DVMHost Install

For new installs a few other steps are required. Grab config.yml and use it as a template for you own DVM host and FNE connection. 
```
wget https://raw.githubusercontent.com/tsawyer/dvm-project-notes/main/config/config.yml
```
You also need the service file... more on this later.

## Firmware
Latest [DVM V24 Board firmware](https://github.com/DVMProject/dvmv24) is required for DVMHost.

## Update 2024-08-17
Change service to **Type = forking**.

/etc/systemd/system/dvmhost.service
 * `Type: forking`

/opt/dvm/config.yml
 * `daemon: true`
 * log `fileLevel: 2` optional
 * log `useSyslog: true` optional, allows [journalctl](journalctl.md) log viewing on modern systemd systems.

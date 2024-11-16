# WD6AWP dvm-project-notes
These notes are things I need to keep track of for the [DVM Project](https://github.com/DVMProject/dvmhost).
99.9% of this info was gleaned from the [DVM Project Discord Server](https://discord.gg/3pBe8xgrEz).
The folks on Discord and GitHub have nothing to do with what I have posted here and they don't support it.

# DVMHost Install
 - First grab the tarball. Install the binaries and example configs in `/opt/dvm`:
```
cd ~
wget https://raw.githubusercontent.com/tsawyer/dvm-project-notes/main/tarball/dvmhost_R04Axx_amd64.tar.gz
tar xzvf dvmhost_R04Axx_amd64.tar.gz -C /opt
```
 - Rename config.example.yml to config.yml.
 - Edit config.yml for the DVMhost settings and FNE connection. See [config.yml edits](config-edits.md).
 - Install the service:
```
cd /etc/systemd/system
wget https://raw.githubusercontent.com/tsawyer/dvm-project-notes/main/config/dvmhost.service
systemctl daemon-reload
```
 - Start DVMhost `systemctl start dvmhost.service`.
 - View the DVMHost log `journalctl -S today -u dvmhost -f`.

# DVMHost Update
This updates the DVMProject amd64 binaries without having to compile it on each server.
These are also the first steps for a new install.
```
cd ~
wget https://raw.githubusercontent.com/tsawyer/dvm-project-notes/main/tarball/dvmhost_R04Axx_amd64.tar.gz
tar xzvf dvmhost_R04Axx_amd64.tar.gz -C /opt
systemctl restart dvmhost.service
```
Tada!

# DVM-V24 Firmware
Latest [DVM V24 Board firmware](https://github.com/DVMProject/dvmv24) is required for DVMHost.

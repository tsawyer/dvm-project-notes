# WD6AWP dvm-project-notes
These notes are things I need to keep track of for the [DVM Project](https://github.com/DVMProject/dvmhost).
99.9% of this info was gleaned from the [DVM Project Discord Server](https://discord.gg/3pBe8xgrEz).
The folks on Discord and GitHub have nothing to do with what I have posted here and they don't support it.

# DVMHost Install and Update
This updates the DVMProject amd64 binaries without having to compile it on each server.
These are also the first steps for a new install.

Grab and the tarball.
```
wget https://raw.githubusercontent.com/tsawyer/dvm-project-notes/main/tarball/dvmhost_R04Axx_amd64.tar.gz
```
Then use the "old install" procedure.
```
tar xzvf dvmhost_R04Axx_amd64.tar.gz -C /opt
systemctl restart dvmhost
```
For updating that is all that is needed.

# DVMHost Install
For new installs a few additional steps are required.
 - Do the above steps which installs the binaries and example configs in `/opt/dvm`.
 - Rename config.example.yml to config.yml.
 - Edit config.yml for you DVM host and FNE connection. See [config.yml edits](config-edits.md).
 - Install the [service file](install-dvmhost-service.md).

# DVM-V24 Firmware
Latest [DVM V24 Board firmware](https://github.com/DVMProject/dvmv24) is required for DVMHost.

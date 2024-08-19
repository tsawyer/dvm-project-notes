# dvm-project-notes
Stuff I need to keep track of for the DVM Project. 99.9% of this info was gleaned from [DVM Project Discord Server](https://discord.gg/3pBe8xgrEz).

## Update 2024-08-17
Change service to **Type = forking**.

/etc/systemd/system/dvmhost.service
 * `Type: forking`

/opt/dvm/config.yml
 * `daemon: true`
 * log `fileLevel: 2` optional
 * log `useSyslog: true` optional, allows [journalctl](journalctl.md) log viewing on modern systemd systems.

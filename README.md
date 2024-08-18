# dvm-project-notes
Stuff I need to keep track of for the DVM Project

## Update 2024-08-17
I found DVMHost runs much better and causes fewer (or possibly no) V.24 board crashes with the following changes.

/etc/systemd/system/dvmhost.service
 * `Type: forking`

/opt/dvm/config.yml
 * `daemon: true`
 * log `fileLevel: 2`
 * log `useSyslog: true` allows journal logging.

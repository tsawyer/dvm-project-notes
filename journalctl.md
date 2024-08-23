## DVMhost logs

The logs are located in `/opt/dvm/log`  with a file name format of `DVM-yyyy-mm-dd.log` and `DVM-yyyy-mm-dd.activity.log`. 

***Note:*** Since changing the service to run with `type=forking` and the config to `daemon: true`, logging must be changed to `useSyslog: true`.

Journalctl is a very useful tool for viewing logs, more functional than viewing text log files. Here are some of the ways I use journalctl to view dvmhost logs. 
1. View all log entries: `journalctl -u dvmhost`
2. View starting yesterday log: `journalctl -S yesterday -u dvmhost`
3. View starting today log: `journalctl -S today -u dvmhost`
4. View starting at 2 o'clock: `journalctl -S 14:00 -u dvmhost`
5. Tail (live view) all entries: `journalctl -u dvmhost -f`

Combine journalctl with grep and magic happens:

6. Tail (live view) errors and warnings: `journalctl -u dvmhost -f | grep -E ' E: | W: '`
7. Tail errors and warnings excluding peerId 310778140: `journalctl -S 09:00 -u dvmfne -f | grep -v 310778104 | grep -E ' E: | W: '`
8. Check V.24 board firmware date: `journalctl -u dvmhost | grep "DVM-V24 FW"`. Wait for the prompt. This takes a while to run all way to the last update.
9. Find my overflows in the FNE: `journalctl -S yesterday -u dvmfne -f | grep "AWP.*overflow"`

General info on [journalctl](https://www.digitalocean.com/community/tutorials/how-to-use-journalctl-to-view-and-manipulate-systemd-logs).

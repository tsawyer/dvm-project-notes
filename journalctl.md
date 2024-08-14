## DVMhost logs

Journalctl is a very useful tool for viewing logs, more functional than viewing text log files. Here are some of the ways I use journalctl to view dvmhost logs. 
1. View all log entries: `journalctl -u dvmhost`
3. View yesterday's log: `journalctl -S yesterday -u dvmhost`
4. View today's log: `journalctl -S today -u dvmhost`
7. View log after 2 o'clock: `journalctl -S 14:00 -u dvmhost`
2. Tail (live view) all entries: `journalctl -u dvmhost -f`
5. Tail (live view) errors and warnings: `journalctl -u dvmhost -f | grep -E ' E: | W: '`
6. Check V.24 board firmware date: `journalctl -S today -u dvmhost | grep "DVM-V24 FW"`

General info on [journalctl](https://www.digitalocean.com/community/tutorials/how-to-use-journalctl-to-view-and-manipulate-systemd-logs).

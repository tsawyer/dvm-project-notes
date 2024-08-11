## DVMhost logs

Journalctl is a very useful tool for viewing logs, more functional than viewing text log files. Here are some of the ways I use journalctl to dvmhost logs. 
1. View all log entries: `journalctl -u dvmhost`
2. Tail (live view) all entries: `journalctl -u dvmhost -f`
3. View yesterday's log: `journalctl -S yesterday -u dvmhost`
4. View today's log `journalctl -S today -u dvmhost`
5. Tail (live view) log for errors and warnings: `journalctl -u dvmhost -f | grep -E ' E: | W: '`

General info on [journalctl](https://www.digitalocean.com/community/tutorials/how-to-use-journalctl-to-view-and-manipulate-systemd-logs).

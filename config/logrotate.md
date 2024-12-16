## This is old. Don't use it. It will fill up your disk.

Edit `/var/logrotate.d/dvm`

```
/var/log/dvm/* {
    weekly
    rotate 5
    missingok
}
```

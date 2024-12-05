## Logrotate

Edit `/var/logrotate.d/dvm`

```
/var/log/dvm/* {
    weekly
    rotate 5
    missingok
}
```

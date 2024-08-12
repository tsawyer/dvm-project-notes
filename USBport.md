## USB Port Alias

2024-08-12 

Current DVM V.24 boards have an issue with USB serial port enumeration when the board resets. That is `/dev/ttyACM0` becomes `/dev/ttyACM1`.
This workaround creates an alias for the serial port. 

Add udev rule to create the alias:
```
cd /etc/udev/rules.d
nano 99_dvmv24.rules
```
Paste:
```
SUBSYSTEM=="tty", ATTRS{idVendor}=="0483", ATTRS{idProduct}=="5740", GROUP="users", MODE="0660", SYMLINK+="DVMV24"
```
Save and exit.

Next modify dvmhost config to use the port alias: 
```
cd /opt/dvm
nano config.yml
```
change the port to `port: /dev/DVMV24`

Save and exit.

Finally `reboot`.

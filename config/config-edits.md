## DMVHost Configuration

Edit the DVMHost configuration file with `nano /opt/dvm/config.yml` or your favorite editor. These changes are needed to login to the FNE and display the host information.

* Change `daemon:` to true
* Under `log:`
  * Change `fileLevel:` to desired level, see comments
  * Change `useSyslog:` to true
  * Change `filePath:` to /opt/dvm/log
  * Change `activityFilePath:` to /var/log/dvm
* Under `network:`
  * CHANGE `id:` to an **FNE wide unique number**. Use your DMR ID (plus 2 digits if needed, limit 9 characters).
  * CHANGE `address:` to the FNE admin provided IP address.
  * CHANGE `password:` to the FNE admin provided password.
  * Change `updateLookups:` to true.
  * Change `saveLookups:` to true.
* Under `protocols:`
  * Under `dmr:` Change `enable:` to false
  * Under `p25:` Insure `enable:` is true
  * Under `nxdn:` Change `enable:` is false
* Under `system:`
  * Change `idenity:` to *YOUR DVMHost SITE NAME* (limit 9 characters)
  * Change `fixedMode:` to true.
  * Change `rfTalkgroupHang` to 0. Prevents Talkgroup filtering on your DVMHost for duration after you unkey.
  * Under `info:` change to your site, etc.
* Under `cwId:`
  * Change `enable:` to false
* Under `modem:`
  * Under `protocol:` change `type:` to "uart"
  * Under `protocol:` change `mode:` to "dfsi"
  * Under `uart:` change the `port:` "/dev/DVMV24". Be sure to add the [udev rules file](https://github.com/tsawyer/dvm-project-notes/blob/main/config/99_dvmv24.rules) to `/etc/udev/rules.d/`.
  * Under `dfsi:` change `diu:` to false
* Under `iden_table` change `file:` to /opt/dvm/iden_table.dat
* Under `radio_id:` change `file:` to /opt/dvm/rid_acl.dat
* Under `talkgroup_id:` change `file:` to /opt/dvm/talkgroup_rules.yml


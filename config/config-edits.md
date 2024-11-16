## DMVHost Configuration

Next, edit the custom configuration file with `nano /opt/dvm/config.yml` or your fav editor. These changes are needed to login to the FNE.

 * CHANGE `id:` to admin provided peerID. Must be unique. Your DMR ID (plus 2 digits if needed). Limit 9 characters. Numbers only.
 * CHANGE `address:` to the FNE IP address provided by your admin.
 * CHANGE `password:` to the FNE password provided by your admin.
 * CHANGE `identity:` to YOUR CALL SIGN or YOUR SITE (limit 8 characters)
 * Under `info:` optionally change the values.
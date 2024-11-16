## DMVHost Configuration

Edit the DVMHost configuration file with `nano /opt/dvm/config.yml` or your favorite editor. These changes are needed to login to the FNE and display the host information.

 * CHANGE `id:` to admin provided peerID. Must be unique. Your DMR ID (plus 2 digits if needed). Limit 9 characters. Numbers only.
 * CHANGE `address:` to FNE admin provided IP address.
 * CHANGE `password:` to FNE admin provided password.
 * CHANGE `identity:` to YOUR CALL SIGN or YOUR SITE NAME (limit 8 characters)
 * Under `info:` optionally change the values.
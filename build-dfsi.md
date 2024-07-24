# DFSI for DVM V24

This is my howto build and configure DFSI for use with the DVM V24 board.

## Clone

As root:

```
apt install git g++
cd /usr/src
git clone https://github.com/DVMProject/dvmhost.git
git clone https://github.com/tsawyer/dvm-project-notes.git
cd dvmhost
```

## Compile and Install

Follow the instructions at [README.md](https://github.com/DVMProject/dvmhost/blob/master/README.md).

* Do install the dependicies.
* Don't install the cross compilers
* No options are needed for cmake. Just do `cmake ..` That compiles the project C code. It doesn't take long.
* The `make` command builds the project and may take a long time.
* Finally do `make strip` and `make old_install`. This copies the project to `/opt/dvm`.

## Configuration

* Copy the configuration file `cp /usr/src/dvm-project-notes/config/dfsi.yml /opt/dvm/`.
* Edit the configuration file `nano /opt/dvm/dfsi.yml`.
  * Under `network:` change `identity: MYCALL-01` to your call sign-ssID or site name.
  * Under `network:` change `peerID: 1234` to a peer ID cordinated with your admin (may be you).
  * Under `network:` change `address: xxx.xxx.xxx.xxx` to the desired FNE IP address provided by your admin.
  * Under `network:` change `password: PASSWORD to the password provided by your admin.
  * Under `serial:` change the `port: "/dev/ttyACM0"`. Find port with `ls -l /dev/ttyAMC`.
 
## Testing

Launch DFSI in the foreground `/opt/dvm/bin/dvmdfsi -f -c /opt/dvm/dfsi.yml`. You should see it login to the FNE after a few moment.

to be continued...

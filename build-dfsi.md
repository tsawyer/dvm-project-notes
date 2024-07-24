# DFSI for DVM V24

This is my howto build and configure DFSI for use with the DVM V24 board.

## Clone

As root or sudo:

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
* Finally do `make strip` and `make old_install`

## Configuration

To be continued...

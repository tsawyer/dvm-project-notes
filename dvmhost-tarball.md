# Setup DVMhost "build" server

This reminds me how to update the tarball on my repo.

A tarball build is pretty much just a normal build with two C librarys preloaded to speed up repeateaded builds.

Info on the two added libs:
 * [ASIO C library](https://think-async.com/Asio/)
 * [Finalcut C library](https://github.com/gansm/finalcut)

## Setup

```
# Normal setup
apt-get install libasio-dev libncurses-dev libssl-dev
cd /usr/src
git clone https://github.com/DVMProject/dvmhost.git

# Preload two libs
git clone https://github.com/chriskohlhoff/asio.git
git clone https://github.com/gansm/finalcut.git
```

## Build

```
cd /usr/src/dvmhost
git pull
make clean
mkdir build
cd build

# cmake with preloaded libs
cmake -DASIO_INCLUDE_DIR=/usr/src/libasio -DFINALCUT_INCLUDE_DIR=/usr/src/finalcut ..

make
make strip
make tarball
```

## Push to repo

I store the tarball tgz on my repo for easy download to sites.

```
cd /usr/src/dvm-project-notes
git pull
cd tarball
cp /usr/src/dvmhost/build/dvmhost_R04Axx_amd64.tar.gz .
git add dvmhost_R04Axx_amd64.tar.gz
git commit
git push
```

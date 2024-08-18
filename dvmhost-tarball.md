# Make DVM tarball for amd64 systems

On my "build" server: 

## Make tarball

Prereq:
```
cd /usr/src
git clone https://github.com/chriskohlhoff/asio.git
git clone https://github.com/gansm/finalcut.git
```

```
cd /usr/src/dvmhost
make clean
mkdir build
cd build
cmake .. -DASIO_INCLUDE_DIR=/usr/src/libasio -DFINALCUT_INCLUDE_DIR=/usr/src/finalcut
make
make strip
make tarball
```
## Push to my repo

```
cd /usr/src/dvm-project-notes
git pull
cd tarball
cp /usr/src/dvmhost/build/dvmhost_R04Axx_amd64.tar.gz .
git add dvmhost_R04Axx_amd64.tar.gz
git commit
git push
```

## Install tarball

On your own dmvhost server:
```
wget https://raw.githubusercontent.com/tsawyer/dvm-project-notes/main/tarball/dvmhost_R04Axx_amd64.tar.gz
tar xzvf dvmhost_R04Axx_amd64.tar.gz.2 -C /opt
systemctl restart dvmhost
```

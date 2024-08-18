# Make DVM tarball for amd64 systems

```text
cd /usr/src/
git clone https://github.com/chriskohlhoff/asio.git
git clone https://github.com/gansm/finalcut.git
cd dvmhost
make clean
mkdir build
cd build
cmake .. -DASIO_INCLUDE_DIR=/usr/src/libasio -DFINALCUT_INCLUDE_DIR=/usr/src/finalcut
make
make strip
make tarball
```

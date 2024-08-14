## DVMHost Update Steps

1. Pull new source and this repo.

Do as root or sudo.


```
cd /usr/src/dvmhost
git pull
cd /usr/src/dvm-project-notes
git pull
```

2. Clean up add the build dir (make clean removes it).

```
cd /usr/src/dvmhost
make clean
mkdir build
```

3. Build new source.

```
cd build
cmake ..
cd ..
make
```

4. Install files (in /opt/dvm).

```
make old_install
```

5. Restart DVMHost.

```
systemctl restart dvmhost
```
Jolly good

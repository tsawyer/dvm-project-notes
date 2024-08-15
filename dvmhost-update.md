# DVMHost Update Steps

Do as root or sudo.


## Pull

Pull new dvmhost source and this repo.

```
cd /usr/src/dvmhost
git pull
```
Optionally pull my repo.
```
cd /usr/src/dvm-project-notes
git pull
```

## Clean up

Remove files, old build and add a new empty build dir.

```
cd /usr/src/dvmhost
make clean
mkdir build
```

## Build new source

```
cd build
cmake ..
make
```

## Install Files

Copy new files to /opt/dvm.

```
make old_install
```

## Restart DVMHost

```
systemctl restart dvmhost
```

Jolly good

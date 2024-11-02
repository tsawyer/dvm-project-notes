# Install MS dotnet repo
I used these instructions and help from the guys on Discord. https://github.com/dotnet/docs/blob/main/docs/core/install/linux.md
```
wget https://packages.microsoft.com/config/debian/12/packages-microsoft-prod.deb -O packages-microsoft-prod.deb
dpkg -i packages-microsoft-prod.deb
```

## Install MS repo and gpg key
```
# wget and process MS gpg key
wget https://packages.microsoft.com/keys/microsoft.asc
cat microsoft.asc | gpg --dearmor -o microsoft.asc.gpg

#Add OS $ID and $VERSION to environment, then wget prod.list for this OS.
source /etc/os-release
wget https://packages.microsoft.com/config/$ID/$VERSION_ID/prod.list

# Install list
mv prod.list /etc/apt/sources.list.d/microsoft-prod.list

# These step might not work...
cp microsoft.asc.gpg $(cat /etc/apt/sources.list.d/microsoft-prod.list | grep -oP "(?<=signed-by=).*(?=\])")

# The goal is to end up with:
cat /etc/apt/sources.list.d/microsoft-prod.list
deb [arch=amd64,arm64,armhf signed-by=/usr/share/keyrings/microsoft-prod.gpg] https://packages.microsoft.com/debian/12/prod bookworm main

# However, this (no key) works on my Debian 11 system
cat /etc/apt/sources.list.d/microsoft-prod.list
deb [arch=amd64,armhf,arm64] https://packages.microsoft.com/debian/11/prod bullseye main#
```

# apt update and install dotnet
``` 
apt update
apt install dotnet-sdk-8.0     #Or desired version.
```

# Compile your project
```
cd /usr/src/dvmusrp  #Or your project.
dotnet build
```

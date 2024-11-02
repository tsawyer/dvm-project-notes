# Install MS dotnet repo
I used these instructions and help from the guys on Discord. https://github.com/dotnet/docs/blob/main/docs/core/install/linux.md
```
wget https://packages.microsoft.com/config/debian/12/packages-microsoft-prod.deb -O packages-microsoft-prod.deb
dpkg -i packages-microsoft-prod.deb
```

## Install gpg key
```
wget https://packages.microsoft.com/keys/microsoft.asc
cat microsoft.asc | gpg --dearmor -o microsoft.asc.gpg
source /etc/os-release #Adds $ID and $VERSION to environment.
wget https://packages.microsoft.com/config/$ID/$VERSION_ID/prod.list

# These two steps might not work...
cp prod.list /etc/apt/sources.list.d/microsoft-prod.list
cp microsoft.asc.gpg $(cat /etc/apt/sources.list.d/microsoft-prod.list | grep -oP "(?<=signed-by=).*(?=\])")

# ... If not, try this instead.
cp prod.list /etc/apt/sources.list.d/microsoft-prod.list
cp microsoft.asc.gpg /etc/apt/sources.list.d/microsoft-prod.list

```

# Update and install dotnet
``` 
apt-get update
apt install dotnet-sdk-8.0     #Or desired version.
```

# Compile your project
```
cd /usr/src/dvmusrp  #Or your project.
dotnet build
```

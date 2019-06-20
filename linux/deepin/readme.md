安装dotnet 
```
我们参考.net官方文档

https://dotnet.microsoft.com/download/linux-package-manager/debian9/sdk-current

的 debian

wget -qO- https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > microsoft.asc.gpg
sudo mv microsoft.asc.gpg /etc/apt/trusted.gpg.d/
wget -q https://packages.microsoft.com/config/debian/9/prod.list
sudo mv prod.list /etc/apt/sources.list.d/microsoft-prod.list
sudo chown root:root /etc/apt/trusted.gpg.d/microsoft.asc.gpg
sudo chown root:root /etc/apt/sources.list.d/microsoft-prod.list
--------------------- 
sudo apt-get update
sudo apt-get install dotnet-sdk-2.2



```

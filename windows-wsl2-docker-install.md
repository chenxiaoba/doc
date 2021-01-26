# windows10 2004 wsl2 docker


### reference
https://medium.com/@roccqqck/%E5%AE%89%E8%A3%9Dwsl2-%E8%88%87-docker-3e6403f0894e

1. 先更先windows到2004的版本(要等一陣子)
2. 以系統管理員身分執行powershell
```
dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
```
3. 重開機
4. 安裝WSL2 linux kernel (點開wsl_update_x64.msi 直接安裝)
https://wslstorestorage.blob.core.windows.net/wslblob/wsl_update_x64.msi
5. 針對已安裝的ubuntu
Powershell 將WSL預設版本調成WSL2
```
$ wsl -l -v // 查看目前wsl版本
  NAME                   STATE           VERSION
* Ubuntu-20.04           Stopped         1
  docker-desktop         Running         2
  docker-desktop-data    Running         2
$ wsl --set-version Ubuntu-20.04 2 // 將ubuntu設定成wsl2
```
如果還沒安裝就可以下這個指令，然後再去microsoft store安裝
```
$ wsl --set-default-version 2
```

6. Resources WSL Integration
Enable integration with additional distros:
將Ubuntu-20.04勾選後點選Apply&Restart

7. 限制記憶體
reference
https://docs.microsoft.com/zh-tw/windows/wsl/wsl-config
https://blog.csdn.net/fengke549015/article/details/106397903
```
$ sudo vim /etc/wsl.conf
[wsl2]
memory=4GB // 最少要4G
swap=8GB
localhostForwarding=true
$wsl --shutdown // 重開機
```

8. elasticsearch 開不起來時
: max virtual memory areas vm.max_map_count [65530] is too low, increase to at least [262144]
```
sysctl -w vm.max_map_count=262144
```

---
title: 'Script C# - 安裝篇'
date: 2016-09-26 12:28:27
tags:
---

這陣子因應公司需求，所以學了ScriptC#

大致上就是把C#當作Script Language寫XD

要安裝的話

可以從[chocolate](https://chocolatey.org/)安裝

``` shell
C:\> choco install scriptcs
```

預設安裝位置為：`%LOCALAPPDATA%\scriptcs\`

使用chocolate的好處是可以用它來update package

```
C:\> choco upgrade scriptcs
```

也可以從powershell裝

``` power shell
@powershell -NoProfile -ExecutionPolicy Unrestricted -Command "iex ((New-Object Net.WebClient).DownloadSt@powershell -NoProfile -ExecutionPolicy Unrestricted -Command "iex ((New-Object Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))" && SET PATH=%PATH%;%systemdrive%\chocolatey\binring('https://chocolatey.org/install.ps1'))" && SET PATH=%PATH%;%systemdrive%\chocolatey\bin
```

如果用powershell安裝時，遇到HTTP 407(proxy authentication is required)
改成用下面的指令裝

``` power shell
@powershell -NoProfile -ExecutionPolicy Unrestricted -Command "[Net.WebRequest]::DefaultWebProxy.Credentials = [Net.CredentialCache]::DefaultCredentials; iex ((New-Object Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))" && SET PATH=%PATH%;%systemdrive%\chocolatey\bin
```

接下來要說得很重要，所以要說三次！

要記得裝.Net Framework 4.6.2以上！

要記得裝.Net Framework 4.6.2以上！

要記得裝.Net Framework 4.6.2以上！

官方文件中，似乎沒有講到要搭配的.Net Version

實測後，建議直接裝.Net Framework 4.6.2以上的版本

就是有遇到Windows 7，可以跑(裝了.Net Framework 4.6)

但是Windows Server 2012(也是裝了.Net Framework 4.6)，不能動啊！！！

慢慢找原因，才發現是同樣是.Net 4.6，安裝在Server 2012上的，比Win 7還舊一些。  
(詳情請參考微軟[How to: Determine Which .NET Framework Versions Are Installed](http://0rz.tw/Dkovt)
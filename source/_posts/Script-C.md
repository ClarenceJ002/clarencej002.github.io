---
title: 'Script C#'
date: 2016-09-26 12:28:27
tags:
---

這陣子因應公司需求，所以學了ScriptC#

大致上就是把C#當作Script Language寫XD

要安裝的話

可以從[chocolate](https://chocolatey.org/)安裝
## chocolate

``` shell
C:\> choco install scriptcs
```

chocolate的預設安裝位置為：`%LOCALAPPDATA%\scriptcs\`

也可以從powershell裝

``` power shell
@powershell -NoProfile -ExecutionPolicy Unrestricted -Command "iex ((New-Object Net.WebClient).DownloadSt@powershell -NoProfile -ExecutionPolicy Unrestricted -Command "iex ((New-Object Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))" && SET PATH=%PATH%;%systemdrive%\chocolatey\binring('https://chocolatey.org/install.ps1'))" && SET PATH=%PATH%;%systemdrive%\chocolatey\bin
```

如果用powershell安裝時，遇到HTTP 407(proxy authentication is required)
改成用下面的指令裝

``` power shell
@powershell -NoProfile -ExecutionPolicy Unrestricted -Command "[Net.WebRequest]::DefaultWebProxy.Credentials = [Net.CredentialCache]::DefaultCredentials; iex ((New-Object Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))" && SET PATH=%PATH%;%systemdrive%\chocolatey\bin
```

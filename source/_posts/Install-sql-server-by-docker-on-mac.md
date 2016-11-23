---
title: 在Mac上用Docker跑Sql Server vNext
date: 2016-11-24 00:27:48
tags:

- docker
- osx
- sql server

---

Sql Server v.Next Public Preview釋出了！

這邊是記錄怎麼安裝～  

首先，先去裝[Docker](https://docs.docker.com/engine/installation/)

裝好後，記得先把Docker的RAM設定成4G(Sql Server要求的)  

然後跑以下指令

``` bash
sudo docker pull microsoft/mssql-server-linux
```

然後就會看到他在抓檔案...

{% asset_img install.PNG after install command %}

抓完了，裝好了，想開始跑了嗎？指令如下(記得把裡面的<YourStrong!Passw0rd>換成自訂密碼)

``` bash
docker run -e 'ACCEPT_EULA=Y' -e 'SA_PASSWORD=<YourStrong!Passw0rd>' -p 1433:1433 -d microsoft/mssql-server-linux
```

如果想把使用完的資料存下來，就要加上輸出資料夾的參數 `-v <host directory>:/var/opt/mssql `  
(範例中是輸出到`/var/opt/mssql`)

``` bash
sudo docker run -e 'ACCEPT_EULA=Y' -e 'SA_PASSWORD=<YourStrong!Passw0rd>' -p 1433:1433 -v <host directory>:/var/opt/mssql -d microsoft/mssql-server-linux
```

題外話，目前不允許把輸出資料夾設到一個volumn底下(mac版與linux版)

## Link

* [Run the SQL Server Docker image on Linux, Mac, or Windows](https://docs.microsoft.com/zh-tw/sql/linux/sql-server-linux-setup-docker)
---
title: 在Visual Studio Code中使用MSSQL
date: 2016-11-24 10:49:58
tags:

- Visual Studio Code
- Sql Server

---

上一篇講了在Mac上用docker安裝mssql，這篇來說怎麼用Visual Studio Code下sql cmd

首先，當然要先有[VSCode](https://code.visualstudio.com/Download)了

接下來按`ctrl+shift+p` (Mac的話就是`command+shift+p`)

{% asset_img img1.png [Command Palette] %}

然後選擇`install extension` (可以直接打install縮小搜尋範圍)

選完後，左邊就會跳出一個extensions的視窗

再輸入`mssql`，就會看到，有兩個，選owner是Microsoft的後，按install

{% asset_img img2.png [Extensions] %}

安裝後，需要重新啟動Visual Studio Code才行

裝好之後，一樣先按`ctrl+shift+p`，然後打進sql後會列出相關的指令

{% asset_img img3.png [Sql Commands] %}

當然要先從connect開始了...  
一開始會先說，會把目前的編輯語言改成sql，就改吧QQ

然後選`Create connection profile`

{% asset_img img4.png [Create Connection Profile] %}

依序輸入

* Server Name (沒意外的話輸入localhost就好)
* Database Name(可按enter跳過)
* User Name(輸入sa)
* Password(輸入啟動sql的docker時設定的那串密碼)
* 是否要存密碼(要不要yes就見仁見智了)
* 為這個profile取個名字(可按enter跳過)

都好了之後，可以在又下方檢查是不是有連線成功了

{% asset_img img5.png [Connected to Sql Server] %}

開個新檔案後，在右下方的檔案類型把他換成sql(原本是plain text)

{% asset_img img6.png [Current file type] %}

然後，直接輸入

``` sql
SELECT * FROM sys.databases;
```

按`ctrl+shift+p`後，先輸入sql後，選擇`Execute Query`

{% asset_img img7.png [Select execute sql query] %}

就可以看到輸出結果了

{% asset_img img8.png [Executed result] %}
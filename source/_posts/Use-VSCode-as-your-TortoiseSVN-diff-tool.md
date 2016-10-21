---
title: Use VSCode as your TortoiseSVN diff tool
date: 2016-10-17 16:48:36
tags: Visual Studio Code, SVN
---

不囉唆，先上圖  
{% asset_img VSCode_SVN_Diff.PNG VSCode SVN Diff Tool %}

指令如下
```
code.exe --wait --diff %base %mine
```

``--wait`` 等待這個視窗關閉，然後返回。

``--diff`` 開啟一個比對用的editor，後面要帶兩個檔案的路徑當參數  
(例如上圖的 %base 與 %mine)

目前還不能拿來當merge tool，已哭
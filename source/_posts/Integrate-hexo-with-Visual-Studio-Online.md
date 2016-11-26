---
title: 讓Visual Studio Team Services來幫忙建置hexo
tags:
  - hexo
  - Continuous Integration
  - Visual Studio Team Services
date: 2016-11-26 21:56:42
---


首先，先在[Visual Studio Team Services](https://azure.microsoft.com/zh-tw/services/visual-studio-team-services/)
上面要有帳號，而且要開一個新的專案

然後原本若hexo還沒有放到git上的話，看要不要考慮直接在他的`Code`裡面開一個新的repository

{% asset_img NewRepo.png [Create a new repository] %}

選完後，到`Build & Release`，並按右邊的`+ New`按鈕，這時應該會跳出`Create new build definition`，請選擇最下面的`Empty`

{% asset_img CreateNewBuildDefinition.png [Create new build definition] %}

如果剛剛跟筆者一樣，已經在[Visual Studio Team Services](https://azure.microsoft.com/zh-tw/services/visual-studio-team-services/)
開了Repo的話，就可以直接在這裡選`Repository`與`Default branch`  
如果要讓他每次commit後就自動build，記得要把`Continuous integration`打勾，選完後按`Create`  
若是放在`GitHub`上，請選`GitHub`  
放在`bitbucket`或是其他git repository，就選擇`Remote Git Repository`  
讓筆者比較意外的是還可以選SVN

{% asset_img SelectRepo.png [Select repository] %}

好了之後，應該會跳出下面那個畫面，請按`Add build step`

{% asset_img BuildStepsIndex.png [Build steps index] %}

這時，會跳出`Task catalog`，然後請在左邊的選單選All後，找到npm，並按`Add`

{% asset_img FindNpm.png [Find npm build] %}

按完後，`Build Steps`會加入一個`npm install`，然後請按`Close`關閉`Task catalog`

{% asset_img FirstBuildStep.png [First build step] %}

然後選了剛剛新建的build step後，右邊會跳出這個Step的詳細資訊

在`npm command`填入`install`(等於在本機上跑`npm install`)

然後再加入一個新的Build step(跟剛剛一樣選npm)

加入後，一樣在steps中選他，然後右邊的詳細資訊中填的下圖一樣

{% asset_img InstallHexoCli.png [Install hexo-cli] %}

加入一個npm的build step，`npm command`一樣放`install`，但是`arguments`放`hexo --save`

加入一個`Command Line`的`Build Step`(可以在`Task catalog`中的`Utility`中找到)填入內容如下

{% asset_img HexoGenerate.png [Hexo generate] %}

最後再加入一個`Command Line`的`Build Step`，`Tool`一樣是`C:/NPM/Modules/hexo`，`Arguments`為`deploy`

不過當然記得要先把相關hexo的相關deploy資訊寫在`_config.yml`中，不然也是沒用XD"

都完成後，記得要按左上方的`Save`，然後再按右上方的`Queue new build...`試試看了～～
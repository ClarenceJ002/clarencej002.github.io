---
title: Backup IIS site to location in IIS config by using msdeploy.exe
date: 2016-11-11 18:30:07
tags:

- IIS
- msdeploy

---

使用  
`msdeploy.exe -verb:sync -source:backupManager={siteName} -dest:backupManager={siteName}`  
就可以在IIS已經設定好的backupPath中建立一個package(zip格式)    
所有的相關參數(例如：最多留幾個備份、備份位置)  
都吃已經設定到ApplicationHost.config裡面的參數  
之後若有需要，可以直接用這個package還原回來

## Link

* [Web Deploy Automatic Backups](https://www.iis.net/learn/publish/using-web-deploy/web-deploy-automatic-backups)
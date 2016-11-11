layout: article
title: backup iis application by cmd
date: 2016-11-11 18:30:07
tags:
---

var deployCmd = "\"C:/Program Files/IIS/Microsoft Web Deploy V3/msdeploy.exe\"";
var arguments = " -verb:sync -source:backupManager={0} -dest:backupManager={0}";
---
title: Ubuntu 裝Java 8 (JDK 8 / JRE 8)
date: 2016-11-22 18:43:10
tags:

- Ubuntu
- java
---

這算是舊文了  
剛好翻到以前的blog就把他整理過來  

安裝步驟：

1. 安裝Java 8

``` bash
sudo add-apt-repository ppa:webupd8team/java
sudo apt-get update
sudo apt-get install oracle-java8-installer
```

2. 檢查安裝版本

    * 只安裝JRE

    ``` bash
    java -version
    ```

    會顯示

    ``` bash
    java version "1.8.o_xx"
    ```

* 有裝JDK

    ``` bash
    javac -version
    ```

    會顯示

    ``` bash
    javac "1.8.o_xx"
    ```

3. 把一些環境變數設定好(像是classpath, java_home之類)

``` bash
sudo apt-get install oracle-java8-set-default
```

## Link

* [http://www.webupd8.org/2012/09/install-oracle-java-8-in-ubuntu-via-ppa.html]
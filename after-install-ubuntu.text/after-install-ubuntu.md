Title: [安装配置] 装完 Ubuntu 后
Date: 2013-08-05
Tags: Ubuntu,Linux,安装
Slug: after-install-ubuntu
Author: Zoey Young
Summary: 装完 Ubuntu 后

[官网](http://www.ubuntu.org.cn/)

### 升级系统

sudo apt-get update && sudo apt-get upgrade

### 要安装的

[ubuntu-tweak](http://ubuntu-tweak.com/source/ubuntu-tweak-stable/)

    :::bat
    sudo add-apt-repository ppa:tualatrix/ppa
    sudo apt-get update
    sudo apt-get install ubuntu-tweak

新立得: synaptic

    sudo apt-get install synaptic

fcitx、fcitx-table-wubi、wps。

其中wps是wps官网下载，然后dpkg安装；ubuntu-tweak是手动添加源，再apt安装；其他则用命令来完成：sudo apt-get install synaptic fcitx fcitx-table-wubi。

没装搜狗软件法是因为我基本不用拼音。

### 要卸载的

libreoffice、thunderbird、ibus、Firefox Ubufox扩展、桌面共享、Empathy、扫描易、蓝牙、ubuntu one、各种辅助功能等。

4、彻底清除无用的软件包

在新立得中，搜索libreoffice、bluz、ubuntu one相关包，能卸载的全部卸载。

打开ubuntu tweak，清理垃圾文件。

### 开发相关

sudo apt-get install git

### 其他

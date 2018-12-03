---
layout: post
title:  "centos7安装mysql5.7"
date:   2018-11-28 16:30:45
categories: linux centos 7 mysql
---

# centos7安装mysql5.7
1. 配置YUM源
    在MySQL官网中下载YUM源rpm安装包：https://dev.mysql.com/downloads/repo/yum/

    **下载mysql源安装包**
    ```shell
    wget https://dev.mysql.com/get/mysql57-community-release-el7-8.noarch.rpm
    ```

    **安装mysql源**

    ```shell
    yum localinstall mysql57-community-release-el7-8.noarch.rpm
    ```

    **检查mysql源是否安装成功**

    ```shell
    yum repolist enabled | grep "mysql.*-community.*"
    ```
    可以修改vim /etc/yum.repos.d/mysql-community.repo源，改变默认安装的mysql版本。
	比如要安装5.6版本，将5.7源的enabled=1改成enabled=0。然后再将5.6源的enabled=0改成enabled=1即可。

2.安装mysql
    ```shell
    yum install mysql-community-server
    ```
    
3.启动mysql服务
    ```shell
    systemctl start mysqld
    ```
    
4.修改密码（首次登录均要修改）  
    **登录**    
    ```shell
    mysql -u root -p
    ```    
    **初始密码**    
    ```shell
    grep 'temporary password' /var/log/mysqld.log
    ```
    **进入mysql后，设置密码**    
    ```shell
    mysql>set password for 'root'@'localhost'=password('密码');
    ```

参考[地址](https://www.linuxidc.com/Linux/2016-09/135288.htm)

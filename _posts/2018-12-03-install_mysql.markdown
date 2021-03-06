---
layout: post
title:  "centos7安装mysql5.7"
date:   2018-12-03 17:30:45
categories: linux centos 7 mysql
---

### centos7安装mysql5.7
一、配置YUM源
   1. 在MySQL官网中下载YUM源rpm安装包：[https://dev.mysql.com/downloads/repo/yum/](https://dev.mysql.com/downloads/repo/yum/)

   2. **下载mysql源安装包**
      ```shell
      wget https://dev.mysql.com/get/mysql57-community-release-el7-8.noarch.rpm
      ```

   3. **安装mysql源**

      ```shell
      yum localinstall mysql57-community-release-el7-8.noarch.rpm
      ```

   4. **检查mysql源是否安装成功**

      ```shell
      yum repolist enabled | grep "mysql.*-community.*"
      ```
      可以修改vim /etc/yum.repos.d/mysql-community.repo源，改变默认安装的mysql版本。
	比如要安装5.6版本，将5.7源的enabled=1改成enabled=0。然后再将5.6源的enabled=0改成enabled=1即可。

二、安装mysql

   ```shell
   yum install mysql-community-server
   ```

三、启动mysql服务

   ```shell
   systemctl start mysqld
   ```

四、修改密码  
   1. **登录**

       ```shell
       mysql -u root -p
       ```
    
   2. **初始密码**

       ```shell
       grep 'temporary password' /var/log/mysqld.log
       ```
    
   3. **进入mysql后，设置密码**

       ```shell
       mysql>set password for 'root'@'localhost'=password('密码');
       ```
       
       或
       
       ```shell
       mysql>ALTER USER 'root'@'localhost' IDENTIFIED BY '密码';
       ```

参考[地址](https://www.linuxidc.com/Linux/2016-09/135288.htm)

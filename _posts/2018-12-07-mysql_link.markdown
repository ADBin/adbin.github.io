---
layout: post
title:  "mysql5.7简单实现外部访问"
date:   2018-12-07 16:42:45
categories: linux centos 7 mysql link
---

### mysql5.7简单实现外部访问

#### 需要打开防火墙的3306（mysql默认）端口

一、进入mysql

   ```shell
   mysql -uroot -p
   ```

二、进入mysql数据库

   ```shell
   mysql>use mysql;
   ```

三、修改user表

   ```shell
   update user set host='%' where user='root'
   ```

>**注意：** 有些user表里会有多个root用户，选择其中一个进行修改

四、使配置生效

   1. 方法一：重启mysql
   
      ```shell
      systemctl restart mysqld
      ```
    
   2. 方法二：刷新mysql的权限表

      ```shell
      mysql>flush privileges;
      ```

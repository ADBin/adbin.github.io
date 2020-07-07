---
layout: post
title:  "centos7 升级 openssl"
date:   "2020-07-07 16:09:10"
categories: linux centos 7 openssl
---

## Centos7 升级 openssl

- #### 环境：
  - CentOS Linux release 7.6.1810 (Core)

    ```shell
	[root@localhost ~]# cat /etc/redhat-release
	CentOS Linux release 7.6.1810 (Core)
	```

- #### 一、去 openssl 官网下载源码包并解压

  ``` shell
  wget https://www.openssl.org/source/openssl-1.1.1g.tar.gz
  tar zxf openssl-1.1.1g.tar.gz
  ```

- #### 二、进入解压目录，编译安装

  ``` shell
  ./config --prefix=/usr/local/openssl
  make&&make install
  ```

- #### 三、建立备份，创建软连接

  ``` shell
  mv /usr/bin/openssl /usr/bin/openssl.bak                  #建立备份
  ln -sf /usr/local/openssl/bin/openssl /usr/bin/openssl    #创建软连接 
  ```

- #### 四、配置环境

  ``` shell
  echo "/usr/local/openssl/lib" >> /etc/ld.so.conf
  ldconfig -v
  ```

- #### 五、检查 openssl 版本

  ``` shell
  [root@localhost ~]# openssl version
  OpenSSL 1.1.1g  21 Apr 2020
  ```

参考[地址](https://www.cnblogs.com/itbsl/p/11275728.html)
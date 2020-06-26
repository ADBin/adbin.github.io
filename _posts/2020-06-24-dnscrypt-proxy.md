---
layout: post
title:  "centos7 配置 dnscrypt-proxy"
date:   "2020-06-24 15:38:52"
categories: linux centos 7 dnscrypt-proxy dns
---

### centos7 配置 dnscrypt-proxy

- #### 环境：
  - CentOS Linux release 7.6.1810 (Core)

    ```shell
	[root@localhost system]# cat /etc/redhat-release
	CentOS Linux release 7.6.1810 (Core)
	```
- #### 一、安装依赖
    
  ``` shell
  yum install libsodium [libsodium13]??
  ```  

-  #### 二、下载 dnscrypt-proxy

  ``` shell
  wget https://github.com/DNSCrypt/dnscrypt-proxy/releases/download/2.0.44/dnscrypt-proxy-linux_x86_64-2.0.44.tar.gz
  ```

  - 备用地址

    ``` shell
    wget https://adbin.top/md/dnscrypt-proxy-linux_x86_64-2.0.44.tar.gz
    ```

-  #### 三、解压并配置
  
  ``` shell
  tar -zxf dnscrypt-proxy-linux_x86_64-2.0.44.tar.gz
  cd linux-x86_64/
  cp example-dnscrypt-proxy.toml dnscrypt-proxy.toml
  vi dnscrypt-proxy.toml
  ```

  > 基础参数：
  >
  > server_names = ['alidns-doh','adguard-dns','adguard-dns-doh']   dns服务器名（获取文件：./public-resolvers.md）
  >
  > listen_addresses = ['127.0.0.1:53']   监听地址

-  #### 四、启动
  
  ``` shell
  ./dnscrypt-proxy &
  ```

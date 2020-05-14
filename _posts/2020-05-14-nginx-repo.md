---
layout: post
title:  "centos7 配置 nginx 官方源"
date:   "2020-05-14 09:56:50"
categories: linux centos 7 nginx 
---

- 环境：
  - CentOS Linux release 7.6.1810 (Core)

    ```shell
	[root@localhost]# cat /etc/redhat-release
	CentOS Linux release 7.6.1810 (Core)
	```


- 一、配置官方源  

  ``` shell
  [root@localhost]# vim /etc/yum.repos.d/nginx.repo
  
  ------------------nginx.repo--------------------------  
  [nginx-stable]
  name=nginx stable repo
  baseurl=http://nginx.org/packages/centos/7/$basearch/
  gpgcheck=1
  enabled=1
  gpgkey=https://nginx.org/keys/nginx_signing.key
  module_hotfixes=true
  ```

- 二、建立缓存

  ``` shell
  yum makecache
  ```
   
- 三、安装

  ``` shell
  yum install nginx
  ```


- 附：[nginx官网文档](https://nginx.org/en/linux_packages.html)
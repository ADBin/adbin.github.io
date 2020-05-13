---
layout: post
title:  "centos7 配置 nginx tengine 服务及自启"
date:   "2020-05-13 16:04:54"
categories: linux centos 7 nginx tengine
---


- ### 环境：
  - CentOS Linux release 7.6.1810 (Core)

    ```shell
	[root@localhost system]# cat /etc/redhat-release
	CentOS Linux release 7.6.1810 (Core)
	```

  - nginx为yum安装，源为nginx官方源
    
    ```
    [root@localhost]# nginx -v
    nginx version: nginx/1.16.1
    ```

  - tengine是编译安装
    - 编译参数：
	  
	  ``` shell
      [root@localhost system]# /usr/local/tengine/sbin/nginx -V
      Tengine version: Tengine/2.3.2
      nginx version: nginx/1.17.3
      built by gcc 4.8.5 20150623 (Red Hat 4.8.5-39) (GCC)
      built with OpenSSL 1.0.2k-fips  26 Jan 2017
      TLS SNI support enabled
      configure arguments: --prefix=/usr/local/tengine --with-http_stub_status_module --with-http_ssl_module
	  ```	 



- ### 自启配置
  
  - #### 一、建立服务
     
	 - 服务目录： /usr/lib/systemd/system/

	   ``` shell
		cd /usr/lib/systemd/system/
		vim nginx.service

		--------------nginx.service------------------
		[Unit]
		Description=nginx - high performance web server
		Documentation=http://nginx.org/en/docs/
		After=network-online.target remote-fs.target nss-lookup.target
		Wants=network-online.target

		[Service]
		Type=forking
		PIDFile=/var/run/nginx.pid
		ExecStart=/usr/sbin/nginx -c /etc/nginx/nginx.conf
		ExecReload=/bin/kill -s HUP $MAINPID
		ExecStop=/bin/kill -s TERM $MAINPID

		[Install]
		WantedBy=multi-user.target
       ```

   - #### 二、测试能不能起来
     
	 ``` shell
	 systemctl start nginx
     ```

   - #### 三、开启自启（前提是第二部能通过）

     ``` shell
	 systemctl stop nginx
	 systemctl enable nginx
	 systemctl start nginx
     ```
	 

- **附 tengine 服务配置文件**

  - 服务目录： /usr/lib/systemd/system/

	``` shell
	cd /usr/lib/systemd/system/
	vim tengine.service

	--------------tengine.service------------------
	[Unit]
	Description=tengine(nginx) - high performance web server
	Documentation=https://tengine.taobao.org/documentation.html
	After=network-online.target remote-fs.target nss-lookup.target
	Wants=network-online.target

	[Service]
	Type=forking
	PIDFile=/usr/local/tengine/logs/nginx.pid
	ExecStart=/usr/local/tengine/sbin/nginx -c /usr/local/tengine/conf/nginx.conf
	ExecReload=/usr/local/tengine/sbin/nginx -s reload
	ExecStop=/usr/local/tengine/sbin/nginx -s quit
	PrivateTmp=true

	[Install]
	WantedBy=multi-user.target
	```

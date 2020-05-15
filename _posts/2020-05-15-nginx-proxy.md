---
layout: post
title:  "Nginx 代理"
date:   "2020-05-15 10:58:54"
categories: linux centos 7 nginx proxy
---

## Nginx 代理

- ### 四层代理
 
  - #### 写在配置文件的http外面

    ``` shell
    stream{
        upstream rdp_proxy{
                hash $remote_addr consistent;
                server 192.168.1.140:3389;
        }
        server {
                listen 6666;
                proxy_connect_timeout 1s;
                proxy_timeout 300s;
                proxy_pass rdp_proxy;
        }
    }
    ```
    
- ### 七层代理（负载均衡）


- ### 接口代理

  - #### 一、路径代理

    > 在server里面添加
    > 实际访问为 http(s)://域名/path/（后端接口必须由path这个接口路径）
    > 后端实际路径 http://ip:port/path

    ``` shell
    location /path/ {
        proxy_pass http://ip:port;
    }
    ```  

    

  - #### 二、添加路径

    > 实际后端路径 http://ip:port
    > 需添加虚拟主机

    ``` shell
    upstream apiName{
        http://ip:port;
    }
    ```
  
    ``` shell
    location ^~/path/ {
        #proxy_pass http://127.0.0.1:8000;
        #root   html;
        #index  index.html index.htm;
        proxy_set_header Host $host;

        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-NginX-Proxy true;

        proxy_pass http://apiName/;
    }
    ```

  - #### 区别

    > 第一种是要求后端服务器的接口中必须含有该路径（后端会接收到改path）
    > 第二种是单纯的增加路径，对后端没有要求（后端不会接收到改path）


- ### 路径代理

  - #### 一、
    
    ``` shell
    location /path/{
        root path1;
        html index.html;        
    }
    ```

    > 服务器文件实际路径 path1/path/

  - #### 二、别名代理
 
    ``` shell
    location /path/{
        alias path2;
        html index.html;        
    }
    ```
   
    > 服务器文件实际路径 path2/

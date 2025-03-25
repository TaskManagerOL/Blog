---
title: Nginx
date: 2024-01-30 20:53:18
tags: [笔记,前端,服务器]
excerpt: 常用的用于设置代理的工具，同类的有使用Golang写的更轻量一点的Caddy。
categories: 技术栈
---

下载路径：[nginx下载](https://nginx.org/en/download.html)

Nginx是目前最流行的web服务器，同类型的还有Apache、Cloudflare、OpenResty。最开始是由⼀个叫做igor的俄罗斯的程序员开发的，2019年3⽉11⽇被美国的F5公司以6.7亿美元的价格收购，现在Nginx是F5公司旗下的⼀款产品了。

# Nginx进程模型

+ Master进程是Nginx的主进程，负责读取和验证配置文件。
+ worker进程就是nginx的工作进程，负责处理实际的请求。
+ master进程只可以有一个，但是worker进程可以有很多个。

# Nginx部署静态资源

nginx静态资源部署运行时需要开任务管理器检查是否存在。

子文件夹：

+ html：用于放你需要部署的、打包好的静态资源。tips：直接放有html的那一堆不要再多包一个文件夹了。
+ logs：用于放每次运行的情况。
+ conf：是配置，可以在nginx.conf中修改端口号，默认80，如果占用就会报错，可修改。
  + 端口号：需要修改时打开nginx.conf文件，找到server->listen 修改后面端口号即可

# Nginx配置文件

### 配置文件的结构

Nginx的配置⽂件是由⼀系列的指令组成的，每个指令都是由⼀个指令名和⼀个或者多个参数组成的。

指令和参数之间使⽤空格来分隔，指令以分号 ; 结尾，参数可以使⽤单引号或者双引号来包裹。

配置⽂件分为以下⼏个部分：

```nginx
# 全局块

worker_processes 1;

events {
	# events块
}
http {
    # http块
    server {
		# server块
         location / {
            # location块
        }
    }
}
```



##### 全局块

+ worker_processes是用于控制worker进程数量的，也可以设置auto，worker进程数量保持同服务器CPU内核数量相同比较合适
+ 其他一些能配置的东西包括运行Nginx服务器的用户组、进程PID存放路径、日志存放路径和类型以及配置文件引入等。

##### events块

> 用于配置客户端和服务器网络连接的一些配置。比如指定每个worker进程可以接收多少个网络连接、网络IO模型等。

+ use：指定使用哪种网络IO模型，只能在events块中进行配置。
+ worker_connections：每个worker process允许链接的最大连接数。

##### http块

> 虚拟主机、反向代理、负载均衡等都在这里配置，http块可以包含很多server块又叫虚拟主机。

+ include：nginx可以使用include指令引入其他配置文件。
+ default_type：默认类型，如果请求的URL没有包含文件类型，会使用默认类型。
+ sendflie：开启高效文件传输模式。
+ keepalive_timeout：连接超时时间。
+ access_log：日志的存放路径和类型。
+ log_format：自定义日志格式。
+  sendfile_max_chunk：设置sendfile最⼤传输⽚段⼤⼩，默认为0，表示不限制。
+  keepalive_requests：每个连接的请求次数。
+ keepalive_timeout： keepalive超时时间。
+ gzip：开启gzip压缩。
+ gzip_min_length： 开启gzip压缩的最⼩⽂件⼤⼩。
+ gzip_comp_level：gzip压缩级别，1-9，级别越⾼压缩率越⾼，但是消耗CPU资源也越多。
+ gzip_types：gzip压缩⽂件类型。
+  upstream： upstream指令⽤于定义⼀组服务器，⼀般⽤来配置反向代理和负载均衡。
  + ip_hash指令⽤于设置负载均衡的⽅式，ip_hash表示使⽤客户端的IP进⾏hash，这样可以保证同⼀个客户端的请求每次都会分配到同⼀个服务器，解决了session共享的问题。
  + weight ⽤于设置权重，权重越⾼被分配到的⼏率越⼤

##### server块

+ listen：监听IP和端⼝。

  +  listen指令⾮常灵活，可以指定多个IP和端⼝，也可以使⽤通配符

    ```
    下⾯是⼏个实际的例⼦：
    # listen 127.0.0.1:80; # 监听来⾃127.0.0.1的80端⼝的请求
    # listen 80; # 监听来⾃所有IP的80端⼝的请求
    # listen *:80; # 监听来⾃所有IP的80端⼝的请求，同上
    # listen 127.0.0.1; # 监听来⾃来⾃127.0.0.1的80端⼝，默认端⼝为80
    ```

+  server_name：⽤来指定虚拟主机的域名，可以使⽤精确匹配、通配符匹配和正则匹配等⽅式

+ location：location块⽤来配置请求的路由，⼀个server块可以包含多个location块，每个location块就是⼀个请求路由。

  + root：root指令⽤于指定请求的根⽬录，可以是绝对路径，也可以是相对路径
  + index：index指令⽤于指定默认⽂件，如果请求的是⽬录，则会在⽬录下查找默认⽂件

+ error_page：⽤于指定错误⻚⾯，可以指定多个，按照优先级从⾼到低依次查找

# Nginx的常用模块

+ http_access_module ：接受或者拒绝特定的客户端请求

+ http_auth_basic_module ：HTTP基本认证，使用用户名和密码来限制对资源的访问

+ http_autoindex_module ：⾃动索引，⽤于显示⽬录列表

+ http_browser_module ：从 User-Agent 请求头中获取和识别客户端浏览器

+ http_charset_module ：添加特定的字符集到 Content-Type 响应头中

+ http_empty_gif_module ：返回⼀个1像素的透明GIF图⽚

+ http_fastcgi_module ：FastCGI⽀持

+ http_geo_module ：从IP地址中获取地理位置信息

+ http_gzip_module ：Gzip压缩⽀持

+ http_limit_conn_module ：限制并发连接数

+ http_limit_req_module ：限制请求速率

+ http_map_module ：从变量中获取值

+ http_memcached_module ：Memcached⽀持

+ http_proxy_module ：反向代理⽀持

+ http_referer_module ：防盗链

+ http_rewrite_module ：URL重写

+ http_scgi_module ：转发请求到SCGI服务器

+ http_ssi_module ：处理和⽀持SSI（Server Side Includes）

+ http_split_clients_module ：根据客户端IP地址或者其他变量将客户端分配到组中，⼀般⽤于A/B测试

+ http_upstream_hash_module ：启⽤⼀致性哈希负载均衡

+ http_upstream_ip_hash_module ：启⽤IP哈希负载均衡

+ http_upstream_keepalive_module ：启⽤⻓连接负载均衡

+ http_upstream_least_conn_module ：启⽤最少连接负载均衡

+ http_upstream_zone_module ：启⽤共享内存负载均衡

+ http_userid_module ：为客户端设置⼀个唯⼀的ID（UID、cookie）

+ http_uwsgi_module ：转发请求到uWSGI服务器，⼀般⽤于Python应⽤

# Nginx反向代理

> 正向代理：正向代理就是代理客户端，比如想访问某些国外网站的时候访问不了，这个时候就需要VPN代理服务器进行正向代理，帮你代理客户端

> 反向代理：反向代理就是代理服务端，比如访问一个网站的时候，比如访问咕噜咕噜（Google），他有很多很多服务器，但是对外暴露的只有一个域名，那我们访问的请求会被转发到后面的服务器上，真实的端口IP服务器信息被隐藏。

### 第一步：在upstream里面放服务器配置：

在upstream后面是一个名字类似Vue路由配置中的name，可以随便取。

```nginx
upstream name {
	server 127.0.0.1:8000;
    server 127.0.0.1:8001;
    server 127.0.0.1:8002;
    ...(启动的服务)
}
```

有时候后台服务器的性能可能不同，以下为两种策略：

+ ip_hash指令⽤于设置负载均衡的⽅式，ip_hash表示使⽤客户端的IP进⾏hash，这样可以保证同⼀个客户端的请求每次都会分配到同⼀个服务器，解决了session共享的问题。
+ weight：⽤于设置权重，权重越⾼被分配到的⼏率越⼤，用于分流。

### 第二步：在localtion中配置：

localtion后面的/...是自己取的名字，意思是将所有访问http://app的请求发送到前面取的name里，

```nginx
localtion /route {
    proxy_pass http://name;
}
```

这样请求都被代理到我们所有服务器中，默认是以轮询的方式来代理。

# HTTPS配置

### 证书

HTTP默认端口是80，HTTPS默认端口是443。

HTTPS协议需要使用到SSL证书，主流云平台上都可以申请到SSL证书，也可以通过openssl生成一个自签名的证书。

```
生成私钥文件：
	openssl genrsa -out private.key 2048
根据私钥生成证书签名请求文件：
	openssl req -new -key private.key -out cert.csr
使用私钥对证书申请进行签名从而生成证书文件：
	openssl x509 -req -in cert.csr -out cacert.pem -signkey private.key
```

### 配置

在server中修改listen监听端口，改为 `443 ssl`

+ ssl_certificate：用于放证书文件路径（填入完整证书链可以不报红）
+ ssl_certificate_key：用于放证书私钥文件路径（填入完整证书链可以不报红）
+ ssl_session_timeout：缓存有效期
+ ssl_protocols：安全链接可选的加密协议
+ ssl_ciphers：配置加密套件/加密算法
+ ssl_prefer_server_ciphers：使用服务器端的首选算法

### 重定向

在http的server上加如下代码：

```
return 301 https://$server_name$request_url
```

# 虚拟主机

虚拟主机可以在一台服务器上部署多个站点，nginx的虚拟主机是通过server块来实现的，每个server块就是一个虚拟主机，通过server_name来指定这个虚拟主机的域名。

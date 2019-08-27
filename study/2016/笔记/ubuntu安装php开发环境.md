##首先安装nginx
```
vim /etc/apt/sources.list
```

增加如下内容

```
## Replace $release with your corresponding Ubuntu release.
deb http://nginx.org/packages/ubuntu/ $release nginx
deb-src http://nginx.org/packages/ubuntu/ $release nginx
```

将$release替换成自己ubuntu版本，如Ubuntu 16.04 (Xenial)：

```
	deb http://nginx.org/packages/ubuntu/ xenial nginx
	deb-src http://nginx.org/packages/ubuntu/ xenial nginx
```

安装这些包

```
sudo apt-get update
sudo apt-get install nginx
```

如果出现GPG错误：http://nginx.org/packages/ubuntu xenial Release: The following signatures couldn't be verified because the public key is not available: NO_PUBKEY $key

执行如下命令

```
## 将$key用GPG错误中的key替换
sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys $key
sudo apt-get update
sudo apt-get install nginx
```

安装完成

测试：
```
nginx -v
```

参考地址：<https://www.nginx.com/resources/wiki/start/topics/tutorials/install/>

##安装php

1.

下载php安装包，比如php-5.5.38.tar.gz 

解压

```
tar zxf php-x.x.x
```

2.

配置，编译PHP。

```
cd ../php-x.x.x
./configure --enable-fpm --with-mysql
make
sudo make install
```

此时有可能报错：error: xml2-config not found. Please check your libxml2 installation.

只需

```
sudo apt install libxml2-dev
```


4.

移动配置文件到正确的目录下

```
sudo cp php.ini-development /usr/local/php/php.ini
sudo cp /usr/local/etc/php-fpm.conf.default /usr/local/etc/php-fpm.conf
sudo cp sapi/fpm/php-fpm /usr/local/bin
```


5.阻止没有可访问文件的时候nginx传递请求到PHP-FPM后端

```
sudo vim /usr/local/php/php.ini
```

添加如下内容

```
cgi.fix_pathinfo=0
```

6.在启动服务之前，还要指定php=fpm以用户 www-data 和 www-data组来运行

```
sudo vim /usr/local/etc/php-fpm.conf
```


找到并修改如下内容

```
; Unix user/group of processes
; Note: The user is mandatory. If the group is not set, the default user's group
;       will be used.
user = www-data
group = www-data
```

启动php-fpm服务

```
sudo /usr/local/bin/php-fpm
```

7.配置nginx

```
sudo vim /etc/nginx/conf.d/default.conf
```

修改默认location，index要首先尝试serve.php文件

```
 location / {
        root   /usr/share/nginx/html;
        index  index.php index.html index.htm;
    }
```

下一步，确保.php文件能转到PHP-FPM后端。在php location配置的下面，增加内容：

```
location ~* \.php$ {
    root            /usr/share/nginx/html;
    fastcgi_index   index.php;
    fastcgi_pass    127.0.0.1:9000;
    include         fastcgi_params;
    fastcgi_param   SCRIPT_FILENAME    $document_root$fastcgi_script_name;
    fastcgi_param   SCRIPT_NAME        $fastcgi_script_name;
}
```

启动Nginx

```
sudo /usr/sbin/nginx -s stop
sudo /usr/local/nginx/sbin/nginx
```

8.移除默认html文件，新建测试php文件

```
sudo rm /usr/share/nginx/html/index.html
sudo touch index.php
sudo chmod 777 index.php 
sudo echo "<?php phpinfo(); ?>" >> /usr/share/nginx/html/index.php
```


最后，访问<http://localhost>,就能看到phpinfo()页面了。

参考<http://php.net/manual/en/install.unix.nginx.php>


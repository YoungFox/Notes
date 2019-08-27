##1
下载软件包http://pecl.php.net/package/yaf，解压

```
cd yaf-xx.xx
phpize
```

如果报错Cannot find autoconf

```
sudo apt-get install autoconf
```

之后再执行一遍phpize

```
./configure
make
sudo make install
```

注意 php5.6如果安装yaf2.3.3以下版本会报错，囧

##在PHP中添加yaf扩展

将php.ini移动到正确目录下，php默认使用的配置是/usr/local/lib/php.ini，被这个坑爹的问题卡了很久。
```
sudo cp /usr/local/php/php.ini /usr/local/lib/
```

在php.ini添加

```
[yaf]
extension="/home/yang/php/yaf-2.3.3/modules/yaf.so"
yaf.environ = product
yaf.library = NULL
yaf.cache_config = 0
yaf.name_suffix = 1
yaf.name_separator = ""
yaf.forward_limit = 5
yaf.use_namespace = 0
yaf.use_spl_autoload = 0
```

重启php-fpm

```
sudo pkill php-fpm
php-fpm
```

在localhost中查询yaf，如果存在则证明安装完成。


##hello yaf

按如下约定目录新建一份。

<pre>
+ public
  |- index.php //入口文件
  |- .htaccess //重写规则    
  |+ css
  |+ img
  |+ js
+ conf
  |- application.ini //配置文件   
+ application
  |+ controllers
     |- Index.php //默认控制器
  |+ views    
     |+ index   //控制器
        |- index.phtml //默认视图
  |+ modules //其他模块
  |+ library //本地类库
  |+ models  //model目录
  |+ plugins //插件目录
</pre>


入口文件，public/index.php

```
<?php  
define("APP_PATH",  realpath(dirname(__FILE__) . '/../')); /* 指向public的上一级 */  
$app  = new Yaf_Application(APP_PATH . "/conf/application.ini");  
$app->run();  
?>
```

将所有请求rewrite到入口文件，nginx中配置

```
  server_name  helloyaf.com;
  root   /usr/share/nginx/test/helloyaf;
  index  index.php index.html index.htm;

  location  / {
        index public/index.php;
        if (!-f $request_filename) {
            rewrite ^/(.*) /public/index.php?$1 last;
        }
   }

  location ~* \.php$ {
         root            /usr/share/nginx/test/helloyaf;
        fastcgi_index   index.php;
        fastcgi_pass    127.0.0.1:9000;
        include         fastcgi_params;
        fastcgi_param   SCRIPT_FILENAME    $document_root$fastcgi_script_name;
        fastcgi_param   SCRIPT_NAME        $fastcgi_script_name;
        }
}

```

重启nginx

```
sudo /usr/sbin/nginx -s stop
sudo /usr/sbin/nginx
```

修改yaf配置，application/conf/application.ini

```
[product]
;支持直接写PHP中的已定义常量
application.directory=APP_PATH "/application/"
```

修改控制器，application/controllers/Index.php ，注意大写Index

```
<?php
class IndexController extends Yaf_Controller_Abstract {
   public function indexAction() {//默认Action
       $this->getView()->assign("content", "Hello Yaf");
   }
}
?>
```

视图，application/views/index/index.phtml 

```
<html>
<head>
   <title>Hello Yaf</title>
</head>
<body>
  <?php echo $content;?>
</body>
</html>
```

配置host，浏览效果：http://helloyaf.com:8000



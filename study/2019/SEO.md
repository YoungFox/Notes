SPA 对SEO不友好

301跳转的SEO可以借助serverMiddleware来做

一定要用hid属性，google引擎会惩罚多重定义meta的站点

```
module.exports = {
  serverMiddleware: [
    '~/servermiddleware/seo.js'
  ]
};

[
  { "from": "/old", "to": "/new" },
  { "from": "/veryold", "to": "/verynew" },
  { "from": "/too-old", "to": "/new" }
]
```

　我们称sitemap.xml,sitemap.html为网站地图，但是两者却有不同的使用方法，具体如下：

       sitemap.xml

　　sitemap.xml的创建是为了更有利于搜索引擎的的抓取策略，从而提高工作效率。生成sitemap.xml后将其链接放入robort.txt内 ：（Disallow:http://网站域名/sitemap.xml）

　　提示：

　　1.良好的robort.txt协议可以指导搜索引擎抓取方向，节省“蜘蛛”抓取时间，所以无 形中提升了“蜘蛛”的工作效率，也就提高了页面被抓取的可能性了。

　　2.将sitemap.xml和robort.txt放在网站的根目录下。


       Sitemap.htm

　　Sitemap.html格式的网站地图主要用来方便用户的浏览使用，并不能起到 XML Sitemap 所起的作用。所以最好是两者都要有。
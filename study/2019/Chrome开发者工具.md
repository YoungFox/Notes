##CSS

审查元素
```
command + option + c ！！！
```

Styles | Computed 可以用 filter

Command Menu
```
shift + command + p
```

CSS覆盖率

红色代表未用到，绿色代表已用。可以点击具体文件查看每一行的使用情况

```
命令行
coverage
```

改变CSS值，配合箭头，原来有多种步伐可选。。。

```
Option+Up (Mac) or Alt+Up (Windows, Linux) to increment by 0.1.

Up to change the value by 1, or by 0.1 if the current value is between -1 and 1.

Shift+Up to increment by 10.

Shift+Command+Up (Mac) or Shift+Page Up (Windows, Linux) to increment the value by 100.
```

More actions:
悬停在某个样式上，会出现快捷添加阴影、背景等操作

Inspect Animations??


##Network


Long-press Reload Reload and then select Empty Cache And Hard Reload.

必须是DevTools打开的情况，才能这么操作

清缓存强刷！！！学到了

除了正则，还支持domain过滤

Type domain:raw.githubusercontent.com into the Filter text box. DevTools filters out any resource with a URL that does not match this domain.

还可以多选，多种response类型

To also see scripts, hold Control or Command (Mac) and then click JS.


Waiting (TTFB). The browser is waiting for the first byte of a response. TTFB stands for Time To First Byte. This timing includes 1 round trip of latency and the time the server took to prepare the response.

###TTFB过长的两种可能原因

The connection between the client and server is slow.

The server is slow to respond. Host the server locally to determine if it's the connection or server that is slow. If you still get a slow TTFB when service locally, then the server is slow.

###Fixes

If the connection is slow, consider hosting your content on a CDN or changing hosting providers.

If the server is slow, consider optimizing database queries, implementing a cache, or modifying your server configuration.


还可以拦截请求，chrome命令行输入block，填入规则、刷新就ok


##Security


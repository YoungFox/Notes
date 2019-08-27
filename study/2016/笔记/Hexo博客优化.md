# Hexo博客优化

##将默认评论插件替换为“多说”
新建comment.ejs

```
<% if ( page.comments){ %>
	<section id="comment">
		<!-- 多说JS代码  -->
	</section>
<% } %>
```

其中page.comments默认值为true


将article.ejs中原来的评论代码删除

```
<% if (!index && post.comments && config.disqus_shortname){ %>
	<section id="comments">
 		<div id="disqus_thread">
    		<noscript>Please enable JavaScript to view the <a href="//disqus.com/?ref_noscript">comments powered by Disqus.</a></noscript>
  		</div>
	</section>
<% } %>
```

引入新的评论

```
<%- partial('comment') %>
```

##JS、CSS压缩
分别安装:hexo-renderer-stylus、hexo-uglify模块

```
$ npm install hexo-renderer-stylus --save
```

```
$ npm install hexo-uglify --save
```

在_config.yml中添加：

```
stylus:
  compress: true
  sourcemaps:
    comment: true
    inline: true
    sourceRoot: ''
    basePath: .

uglify:
  mangle: true
  output:
  compress:
  exclude: '*.min.js'
```

##为不同模板更换不同的layout(视图)
比如有这样的需求：首页使用酷炫的header，而其他页比如文章页等使用普通的header，可以这样做：
在index.ejs中添加如下代码

```
<% page.layout="home" %>
```

在_partial文件夹中新建header-common.ejs，内容自己编写。

在layout.ejs中将header引入代码改为

```
<% if (page.layout=="home"){ %>
    <%- partial('_partial/header', null, {cache: !config.relative_link}) %>
<% }else{%>
    <%- partial('_partial/header-common', null, {cache: !config.relative_link}) %>
<%}%>
```

目前能想到的最好办法就是这样，如果还有更好的方案请不吝赐教。

##本地化（i18n）

在languages文件夹中新建zh-cn.yml，将需要翻译的e文写入文件如下：

```
Home: 首页
Archives: 归档
```

在_config.yml中配置i18n_dir:

```
i18n_dir: zh-cn
```

在模板中通过`__()`或`_p()`,即可得到翻译后的字符串。


##添加“阅读全文”功能

只需在文章中插入<!--more-->即可，此注释之前的内容可以显示在首页，之后会插入"阅读全文"按钮，按钮文字在相应主题文件夹下的_config.yml文件中：

```
excerpt_link: 阅读全文
```





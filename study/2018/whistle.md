（http://wproxy.org/whistle/）

使用流程
w2 start -> 配置浏览器代理至127.0.0.1:8899 -> 访问http://local.whistlejs.com 配置rules和values ->如果要抓https请求则需要安装whistle的根证书

配置代理时，需要选中switchysharp的“对所有协议均使用相同的代理服务器”，否则抓不到https

需要打开HTTPS选项，选中 Capture TUNNEL CONNECTs

可以改ua、refferer


拦截请求，mock jsonp数据


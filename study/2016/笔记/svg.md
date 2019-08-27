Scalable Vector Graphics

使用xml格式定义图像

HTML5中，可以直接在HTML页面中嵌入SVG

```
<!DOCTYPE html>
<html>
<body>

<h1>My first SVG</h1>

<svg width="100" height="100">
  <circle cx="50" cy="50" r="40" stroke="green" stroke-width="4" fill="yellow" />
</svg>

</body>
</html>
```

和img标签一样，但是属于行内元素
\<svg\>标签的width、height定义了SVG图像的宽高

标签要正确关闭

SVG预定义的形状

*	Rectangle <rect> 长方形
*	Circle <circle> 圆
*	Ellipse <ellipse> 椭圆
*	Line <line> 线
*	Polyline <polyline> 折线
*	Polygon <polygon> 多边形
*	Path <path> 路径

属性：
x,y：定位信息
rx,ry：圆角

style
fill：填充颜色
stroke：边框颜色
stroke-width：边框宽度
fill-opacity：填充色的不透明度
stroke-opacity：边框颜色的不透明度






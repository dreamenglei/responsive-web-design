# 主流浏览器的CSS hack
css hack是一种技术手段，**目的是解决不同浏览器对css解析不一致的问题**，最终产生的效果就是可以跨终端，在不同浏览器中显示一致的界面效果。

针对不同器写相应的CSS代码的过程，就叫做CSS HACK.
## CSS hack 书写顺序
一般将适用范围广、被识别能力强的CSS定义在前面。
## 分类
 - CSS属性前缀

在CSS样式属性名前加上一些只有特定浏览器才能识别的前缀。
**浏览器内核与前缀**

| 内核  | 内核前缀  | 浏览器  |
| :------------: | :------------: | :------------: |
| Webkit  | -webkit-  |    Safari、Chrome27以下|
|  Blink | -webkit-  |  Chrome28以上、Opera15以上 |
|  Gecko | -moz-  | Firefox  |
|  Trident | -ms  |  IE系列、360安全浏览器 |
|  Presto | -o-  |  Opera12以下 |
- 选择器前缀

在CSS选择器前加上一些只有某些特定浏览器才能识别的前缀

- IE条件注释（HTML头部引用if IE）

该方式是IE浏览器专有的方式。
```css
<!--[if IE]>
这段文字只在IE浏览器显示
<![endif]-->
——————————————
<!--[if gte IE 6]>
这段文字只在IE6以上(包括)版本IE浏览器显示
<![endif]-->
——————————————
<!--[if ! IE]>
这段文字只在非IE浏览器显示
<![endif]-->
```

------------
判断某属性是否被浏览器们支持，可用到这个网站。[Can I use](https://caniuse.com/#home "Can I use")
下面这个算啥，不知道呃，应该是属性前缀。
这是CSS3里的animation动画，做了兼容性设置。
```css
@keyframes myfirst
{
from {background: red;}
to {background: yellow;}
}

@-moz-keyframes myfirst /* Firefox */
{
from {background: red;}
to {background: yellow;}
}

@-webkit-keyframes myfirst /* Safari 和 Chrome */
{
from {background: red;}
to {background: yellow;}
}

@-o-keyframes myfirst /* Opera */
{
from {background: red;}
to {background: yellow;}
}
```
下面这个是CSS3里的transition属性。
```css
div
{
width:100px;
transition: width 2s;
-moz-transition: width 2s; /* Firefox 4 */
-webkit-transition: width 2s; /* Safari 和 Chrome */
-o-transition: width 2s; /* Opera */
}
```

------------

下面来自知乎：[跨浏览器问题的五种解决方案](https://zhuanlan.zhihu.com/p/25975404 "跨浏览器问题的五种解决方案")
- 前缀，跟前面说的一样
- 使用reset，不同浏览器的默认配置不一样，先reset，包括border,margin什么的
作者推荐了一个[normalize.css](http://necolas.github.io/normalize.css/ "normalize.css")
```css
html,body,div,span,applet,object,iframe,h1,h2,
h3,h4,h5,h6,p,blockquote,a,abbr,acronym,address,
big,cite,del,dfn,em,img,ins,kbd,q,s,samp,small,
strike,strong,sub,sup,tt,var,b,u,i,center,dl,dt,
dd,ol,ul,li,fieldset,form,label,legend,table,caption,
tbody,tfoot,thead,tr,th,td,article,aside,canvas,details,
embed,figure,figcaption,footer,header,hgroup,input,menu,
nav,output,ruby,section,summary,time,mark,audio,video {
border: 0;
margin: 0;
padding: 0;
vertical-align: baseline;
}
```
用这个样式就行
- 避免填充宽度，是说默认的盒子模型元素width和height只包括内容区域，当有border和padding时，绘制出的元素宽度还得加上那两个值，这不利于实现响应式布局。所以可以利用box-sizing属性来设置，默认是content-box，我们可以设置成border-box，即此时width是包含了border和padding的。
详情可查看[MDN box-sizing](https://developer.mozilla.org/zh-CN/docs/Web/CSS/box-sizing "MDN box-sizing")
```css
 * { -webkit-box-sizing: border-box; /* Safari/Chrome, other WebKit */
-moz-box-sizing: border-box; /* Firefox, other Gecko */
box-sizing: border-box; }
```
作者推荐我们用上面的样式。
- 清除float，可以用伪元素after来做，比较帅。
代码如下：
```css
.parent-selector:after {
content: "";
display: table;
clear: both;
}
```
- 测试的话，作者推荐了一个[endtest](https://endtest.io/ "endtest"),或者就往电脑上装五个浏览器吧！一边测试一边开发，但兼容性会好！
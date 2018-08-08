# 主流浏览器的CSS 适配
css hack是一种技术手段，**目的是解决不同浏览器对css解析不一致的问题**，最终产生的效果就是可以跨终端，在不同浏览器中显示一致的界面效果。

当浏览器无法解析其中一段CSS样式或属性时，就会自动忽略这一段的样式，进而解析下一段样式。所谓的CSS Hack技巧，讲的就是找出不同浏览器版本之间不同的CSS解析规则，好让网页设计师所定义的CSS样式可以让该样式在特定浏览器版本下无法辨识，但另一个版本的浏览器可以辨识的技巧，也是因为这类「小技巧」十分神奇，所以才被称为“ Hack ”。     
[跨浏览器网页设计密技2](https://blog.miniasp.com/post/2012/05/02/Building-Website-is-not-that-easy-CSS-Hacks-and-IE-Conditional-Comments.aspx "跨浏览器网页设计密技")
```css
.page {
   color : black;    /*所有浏览器*/    
   color /**/ : green ;  /* IE7, IE8, IE9 */ 
  * color : blue;        /* IE6, IE7 */ 
  _ color : red;         /* IE6 */ 
 }
```
**注意：**样式的顺序性非常重要，因为比较晚定义的样式会取代较早定义的样式，所以你必须把最多浏览器版本看的懂的样式写在比较上面，这样才能达到CSS Hack的效果。
例如：对于IE6,会先套用正常的color: black;属性，套用值为black 
第2行的color /**/: green;它看不懂，所以跳过 
第3行的*color: blue;它也看的懂，所以套用值会变成blue 
第4行的_color: blue;它也看的懂，所以套用值会变成red

由于CSS hack 技巧用了很多非标准的写法，而且这类语法是通过浏览器解析CSS规则的瑕疵来达到目的的，万一哪天哪个浏览器改了规则，整个套路还得变，这是一个不确定的风险，所以应该尽量减少CSS hack的语法。

------------


再来看一看[跨浏览器见面设计密技1](https://blog.miniasp.com/post/2012/03/14/Building-Website-is-not-that-easy-DOCTYPE-and-CSS-Reset-Normalize.aspx "跨浏览器见面设计密技1")
- 使用DOCTYPE
HTML4.01里，定义了三种标准模式，网页设计师想要利用CSS 设计出具有编排弹性又能够跨浏览器显示的网页，必须要求浏览器使用「标准模式」来显示网页，否则网页怎样排版都不可能编排到一致的。
- 使用CSS Reset
由于使用CSS Reset 的主要目的是为了替你的「跨浏览器网页设计」打下一个稳固的根基，那么这个根基就必须十分牢固，不可任意变动，否则影响到的将会是你整个网站的样式。但是，网路上有些特定的CSS Reset 版本会与特定CSS Framework 或JavaScript Framework 紧密的绑在一起，如果不小心混用的话，就会导致网页上出现一些不必要的版面问题。尤其是你在一个网页里用了两套以上不同的CSS Framework 会更容易遇到这个问题。
这些CSS reset样式也许会和第三方UI框架不太兼容，会出现一些奇怪的样式，
还好，目前市面上那些能说得出名称的UI 框架，都对这类CSS Reset 互相影响的情况做出了处理，也都有解决方法，各位详读这些UI 框架的注意事项即可了解如何避免此类问题发生。
- CSS normalize
CSS reset的缺点在于把大部分的标签的预设样式都规0了，这样有些标签，尤其是ol ul li等标签，必须要再定义过样式才能正常运作，故开发出了normalize版本，其特点是保留了原本预设的HTML标签的样式，仅针对不同浏览器不相容的标签进行调整。
normalize和reset二选一即可，一起用就消了啊大兄弟。

------------

看看[跨浏览器见面设计密技3](https://blog.miniasp.com/post/2012/05/14/Building-Website-is-not-that-easy-Cross-browser-testing-tools.aspx "跨浏览器见面设计密技3")    
建站过程中要不断打开不同的浏览器来测试，很麻烦，所以作者推荐了测试工具。
- IETester 免费的，内建IE5.5~10.9核心引擎，测试见面在各IE版本中的相容性。
- Browsershots 免费线上服务，各种浏览器，但不太稳定。
还有两个，懒的写了……

------------


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

------------

一篇CSDN上的，翻译的杂志上的文章，给跨浏览器的CSS编码提出一些建议。
[跨浏览器CSS编码的准则](https://blog.csdn.net/echody/article/details/55214227 "跨浏览器CSS编码的准则")
- 理解盒子模型
盒子模型的一些基本准则：
	- 如果没有指定高度，块元素将与其包含的内容一样高，加上内边距（除非有浮动）
	- 如果未指定宽度，则非浮动框将展开以适合其父级的宽度减去内边距
	- 如果一个框的宽度设置为“100％”，它不应该有任何外边距，内边距或边界，否则会从其父辈元素溢出
- 内联元素与块级元素
	- 默认情况下，块元素将自然水平扩展以填充其父容器，因此不需要设置宽度为“100％”
	- 默认情况下，块元素将从父容器的最左边缘开始，位于任何之前的块元素下面（除非使用浮动或定位元素） 内联元素将忽略宽度或高度设置
	- 内联元素随文本一起流动，并且受空白，字体大小和字母间距等打印属性的制约
	- 内联元素可以使用vertical-align属性进行对齐，但块元素不能
- CSS重置
当实现CSS重置时，在不同浏览器中发生的和内边距及外边距相关的差异变得更加规范化（即使在麻烦的HTML表单中）。 因为重置会导致所有元素从零开始，所以你可以更好地控制元素的间距和对齐方式，因为所有浏览器都将从相同的基本设置开始。
	- 
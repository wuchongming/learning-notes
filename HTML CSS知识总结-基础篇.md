#### 块级元素、行内元素和inline-block元素之间的区别

- 行内元素：display:inline。和其它行内元素都在一行上排列，不可以设置宽高，宽高随文本内容的变化而变化，但是可以设置行高（line-height）和左右内外边距；

```
行内元素一般不包括块级元素，但是a标签例外。比如页面有banner广告，并且可以点击跳转，这个时候a标签可以包含块级元素，浏览器会将a标签的透明度设置为0）；
```

- 块级元素：display:block。独自占一行，高度、行高、内外边距都可改变，可以容纳行内元素；

```
块级元素可以包含块级元素和行内元素，但是P元素不可以包含块级元素。
```
- inline-block元素。既可以其它元素排在一行，又可以改变元素的高度、行高和内外边距。

```
比如input、select元素，可以设置宽高
```

#### 解释下inline-block盒子之间间隙的问题
> 水平排列的inline-block盒子之间会出现间隙，这种情况类似于文本字体之间也会有间隙
- 解决办法：将父级元素字体大小设为0

#### 如何理解html结构的语义化
1. 结构清晰，易于开发者阅读；
2. 有助于搜索引擎机器人的搜索；
3. 有助于SEO,利于网站的推广；
4. semantic、microdata

#### HTML、XHTML和HTML5的区别
- html属于SGML(标准通用标记语言)
- XHTML属于XML,是HTML进行XML严格化的结果
- HTML5不属于SGML或XML,比XHTML宽松

#### HTML和XHTML有什么区别？
1. XHTML元素必须被正确地嵌套
2. XHTML元素必须严格区分大小写
3. XHTML标签必须被关闭
4. XHTML空标签也必须被关闭
5. XHTML元素必须拥有根元素

#### 哪些元素可以自闭合
所谓闭合元素即在该元素中不可能再嵌入别的元素
- meta link
- input
- img
- hr br

#### HTML和DOM的区别
- HTML本质是字符串
- DOM是浏览器对HTML解析后生成的JS对象，提供了访问HTML文档的接口和方法。

#### attribute和property的区别
- attribute是HTML标签的属性
- property是DOM对象的属性

#### form的作用有哪些
- 直接提交表单
- 使用submit/reset按钮
- 可以对表单进行校验
- 便于第三方库提取整体值
- 便于浏览器保存表单

#### 伪类选择器和伪元素的区别
> 伪类用单冒号表示，伪元素用双引号表示；
- 伪类种类

```
:active
:focus
:hover
:link
:visited
:first-child :last-child :nth-child 
:nth-of-type
:root
:not
:empty
```
- 伪元素种类

```
::first-letter 将特殊样式添加到文本首字母
::first-line 将特殊样式添加到文本首行
::before 在某元素之前插入某些内容
::after 在某元素之后插入某些内容
```
- 区别
- 伪类作用对象是整个元素，是元素的某种状态

```
a:hover {
    color: #222;
}
div:nth-child(3) {
    color: #444;
}
```

- 伪元素是真实的元素，作用于元素的一部分：比如一个段落的第一行或者首字母

```
p::first-letter {
    color: #555;
}
p:first-line {
    color: #777
}
```

#### H5的新特性
- 语义化更好的标签元素：header、nav、section、article、aside、fildset、footer
- 新的表单控件：calender、data、time、email、url、search
- 拖拽释放API（drag、drop）
- 音频、视频API（audio、video）
- 画布API（canvas）
- 本地离线缓存（localstorage、sessionstorage）
- 地理位置API(getlocation)
- 新的技术（webWorker、webSocker）

#### em和i的区别
- 都是表示斜体
- em是语义化的标签，表示强调
- i是纯样式标签，表示斜体
- HTML5中i不推荐使用，一般用作图标

#### viewport所有属性
1. width:设置layout-viewport的宽度，为正整数或者设置为device-width;
1. initial-scale:设置页面的初始缩放值;
1. minimum-scale:允许用户的最小缩放值;
1. maximum-scale:允许用户的最大缩放值;
1. user-scalable:是否允许用户进行缩放;
1. target-densitydpi:安卓中使用，表示设备的密度等级，决定css中1px代表多少物理像素;
1. height:设置layout-viewport的高度，很少用到。

#### display:none和visibility:hidden的区别
- display:none 隐藏对应的元素，但是在文档布局中不再给它分配空间；
- visibility:hidden 将对应的元素的透明度设置为0，但是在文档布局中仍保留原来的空间。

#### href和src之间的区别、title和alt之间的区别

- href：指定网络资源的位置（超文本链接），从而在当前元素、当前文档定义的锚点与网络资源之间建立链接；应用元素：link、a。
- src：指将资源嵌入到当前元素定义的位置；应用元素：img、script、iframe。
- title：既是html标签，也是html属性，作为属性时，用来为元素提供额外的说明信息。
- alt：html属性，主要在网页图片无法正常显示时向用户提供图片的文字说明。

#### iframe的优缺点
- 优点

```
1.解决第三方内容如图标和广告等加载缓慢的问题
2.Security sandbox
3.并行加载脚本
```
- 缺点

```
1.需要等到父子页面内容一起加载完才显示
2.加载缓慢，影响页面性能
```

#### documnet.write和innerHtml的区别
- documnet.write会重绘整个页面
- innerHtml只是重绘页面的一部分

#### Doctype的作用
- DOCTYPE：<!DOCTYPE>声明位于html文档的最前面，此标签告知浏览器文使用哪种html或者xhtml规范。
> 个人理解：DOCTYPE告知浏览器使用哪种DTD规范。
- DTD(Document Type Definition):是一套关于标记符的语法规则，是html的验证机制。
> 个人理解：DTD用来告诉浏览器使用哪种引擎来解析html文档。
- 严格模式和混杂模式如何区分

```
1.严格模式中，页面以浏览器的最高标准运行；
2.混杂模式中，页面模拟老浏览器的行为使得站点正常工作，DOCTYPE不存在或者格式不正确会导致文档以混杂模式呈现。
```

- HTML5的DOCTYPE声明：<!DOCTYPE html>
- HTML 4.01 Strict 
```
DOCTYPE声明：使用展示性和已废弃的标签，浏览器解析会出现错误
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01//EN" "http://www.w3.org/TR/html4/strict.dtd">
```

- HTML 4.01 Transitional 
```
DOCTYPE声明：使用展示性和已废弃的标签，浏览器解析不会报错
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
```

#### 标准盒模型和怪异盒模型
- 标准盒模型：box-sizing:content-box;
- 怪异盒模型：box-sizing:border-box;
- 区别：

```
在标准模式的盒模型下：设置的宽/高=内容content的width/height;
在怪异模式的盒模型下：设置的宽/高=内容content的width/height+padding+border
```
- JS如何设置获取盒模型对应的宽高

```
dom.style.width/height // 仅在dom有行内样式下
dom.currentStyle.width/height // 仅仅IE支持
window.getComputedStyle(dom).width/height // 兼容ff，chrome浏览器
dom.getBoundingClientRect().width/height // 获取dom的绝对位置
```

#### css3增加了哪些新特性
> 圆角（border-radius）、阴影（border-shadow）、文字特效（text-shadow）、渐变（gradient）、图形边框（border-image）、透明度（rgba）、transform、弹性盒模型（flex）、媒体查询、伪类选择器、唯一的伪元素（::selection）。
- 注：阴影（border-shadow）、渐变（gradient）等新特效比较耗性能，尽量减少使用。

#### link、import两者之间的区别

1. 老祖宗的差别，link是HTML标签，@import只支持加载css;
1. 加载顺序的差别，link引用的文件会被浏览器同时加载，而@import引用的css会等到页面加载完后再加载；
1. link是标签元素，不存在兼容性问题，而@import是在css2中引进的，老版本浏览器不兼容；
1. link引用的样式权重高于@import引用的样式权重。

#### transform、transition和animation
- transform:作用于元素本身，通过偏移（translate）、旋转（rotate）、变形（screw）、缩放（scale）、透视（perspective）等功能实现炫酷的静态效果。
- transtion和animation都是在一段时间内css元素随着时间改变而改变；
- transtion和animation的区别

```
1.transition需要事件去触发，比如hover、click等事件，而animation不需要事件触发，会自动执行；
2.animation可以通过keyframe(关键帧)显示的控制某一帧下具体的CSS属性值，例如：
@keyframes myfirst
{
    0% {background: red; left:0px; top:0px;}
    50% {background: blue; left:200px; top:200px;}
    100% {background: red; left:0px; top:0px;}
}
而transition只能隐式来执行，不能控制某一帧下的CSS属性值；
3.animation是通过模拟CSS属性值来改变动画的，动画结束后CSS属性值没有改变，而transition在动画结束后改变了CSS属性值。
```
-animation属性

```
animation-name
animation-duration
animation-timing-function
animation-delay
animation-iteration-count
animation-direaction
```
-transtion属性

```
transtion-property
transtion-duration
transtion-timing-function
transtion-delay
```


#### nth-of-type && nth-child的区别
- 举例说明：
```
<ul>
    <p>111<p/>
    <span>222</span>
    <li>1</li>
    <li>2</li>
    <li>3</li>
</ul>
```
- li:nth-of-type(2) 表示ul下得到第二个li元素
- li:nth-child(2) 表示既是li元素又是ul下的第二个元素

#### 如何让一个div上下左右居中
- 方法一：

```
.div1 {
    width:400px;
    height:400px;
    position:absolute;
    top:50%;
    left:50%;
    transform:translate(-50%,-50%)
}
```
- 方法二：

```
.div2 {
    width:400px;
    height:400px;
    position:absolute;
    top:50%;
    left:50%;
    margin-top:-200px;
    margin-left:-200px;
    }
```
- 方法三：

```
.div3 {
    width:400px;
    height:400px;
    position:absolute;
    top:0;
    left:0;
    bottom:0;
    right:0;
    margin:auto;
}
```

#### 清除浮动有几种方式
1. 给父元素设置高度
1. 在浮动元素后面添加新的元素（百度做法，兼容性更好）：
```
{
    content: '';
    height: 0;
    display: block;
    clear:both; // 清除两边浮动
}
```

1. 给父元素格式化上下文（BFC）;
1. 在父元素内部插入伪元素::before、::after（腾讯、淘宝、网易做法）

```
{
    content: '';
    height: 0;
    display: table;
    clear:both; // 清除两边浮动
}
```

#### BFC、IFC、FFC
- BFC：块级格式化上下文（使元素内外相互不受影响）；IFC：行内盒子格式化上下文;FFC：弹性盒子格式化上下文。
- BFC的几种方式：

```
1.float不为none;
2.position为absolute和fixed;
3.display为inline-block、table-caption、table-cell、flex、inline-flex
2.overflow不为visible
```
- BFC的作用：

```
1.解决浮动引起父级元素高度塌陷的问题；
2.解决浮动侵占的问题；
3.解决元素margin上下重叠的问题；
```

#### 对flex的理解
1. 弹性盒模型
2. 默认水平排列
3. 用于响应式开发

#### 为什么要初始化css样式
> 因为浏览器兼容性问题，不同的浏览器对有些标签的默认样式值是不同的，如果没对css初始化往往会出现浏览器之间的页面显示差异。

#### 解释下css sprites,以及页面中如何使用它
- css sptites其实就是将多张背景图整合到一张大的图片当中，再利用css的‘background-image’、‘background-repeat’、‘background-position’等组合进行背景定位。
- 作用:减少http的请求、节省网络开销。

#### 什么是FOUC?如何来避免FOUC
> FOUC:无样式内容闪烁
- IE、firefox浏览器先对html进行展示，然后等css文件加载完成的时候再对html进行渲染，特别是用@import引用css文件的时候（最后被加载），就会出现FOUC问题。
- 如何避免FOUC：将@import要引用的css文件用link引用。

#### CSS选择器和CSS样式的优先级
- css选择器：
> id选择器 class选择器 属性选择器 伪类选择器 标签选择器 伪元素选择器 相邻选择器（+）子选择器（>）后代选择器（div p）通配符选择器
- 优先级
> !important > 行内样式 > id选择器(权重100) >类选择器 = 属性选择器 = 伪类选择器(权重10) > 元素选择器 = 伪元素选择器(权重1) > 通配符选择器（权重0） > 浏览器默认样式(权重0)

```
权重计算示例（不进位-权重等级不可逾越）：
#id .link a[href]
#id 100
.link 10
a 1
href 0
结果100+10+1+0=111

#id .link.active
#id 100
.link 10
.active(属性选择器) 10
结果 100+10+10=120
```

#### 浏览器是如何解析CSS选择器的
从右到左解析

#### base64的使用
1. 用于减少http的请求,避免跨域
2. 适用于小图片
3. base64文本的大小约为原图的4/3，浏览器不会缓存

#### 如何用CSS绘制出一个三角形
设置盒子三边border-width，再将三边围起来的盒子宽或高设置为0

#### 如何美化checkbox
隐藏input,美化label样式

#### 什么是预处理器语言
> css预处理器是一种语言用来为css增加一些编程的特性（变量、逻辑、函数和模块化-按需加载），可以使得css编写更加简洁。

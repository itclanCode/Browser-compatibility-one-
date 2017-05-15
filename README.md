# Browser-compatibility-one-
# 活解浏览器兼容性(一)
![](http://i.imgur.com/eXefGF9.jpg)
前言:

自从你进入前端队伍时，任你天马行空的写html css javascript代码写得多么happy，百分百的还原UI M M给出的psd文档，编织成静态页面，原本是一完美的页面，可是当不同user一打开时，纵使完美的外表下也略有瑕疵，不尽相同，同一段代码，放在不同的浏览器下，表现得不一致，这就是浏览器的兼容性问题，无可奈何，我们注定终身要与浏览器兼容性作斗争，无论是在面试时，还是自己平时写代码时，兼容性问题：一直是我们天敌，今天我就对我自己的学习及平时遇到的一些兼容问题，进行了一下总结，无法归纳关乎所有的兼容性问题，但是我们是可以减少和避免兼容性的问题的发生，认清本质，平时遇到了，留意一手，总结归纳一下，便是，希望对你有用

正文从这里开始~

> 如何看待兼容性问题

产生的原因：同一段html css,js代码在不同的浏览器中，展现出的效果不尽相同，各个浏览器版本之间的内核的差异，对代码的解析也不完全一致，这样就产生了hack

> 如何解决这种问题

1. 合理规范的html结构代码，使用标准规范的标签，认清css的属性，css代码尽量简单有效，属性写全，低版本浏览器的交互效果，css解决不了的，用javascript编写（例如IE8下的hover是不起作用的），针对比较特殊的用css hack处理（IE6标签属性前加*  +  Ie7标签属性前加_下划线等）
2. 确定什么浏览器，什么版本，先分析代码结构--》css，js代码-放在不同的版本的浏览器下测，缩小范围，是不是该标签在该浏览器不支持，css样式前缀等
3. 确定是不是原生js的一些方法。属性等问题，比如：某个浏览器下不支持该事件触发等，使用更加稳当兼容性更好的的框架，例如jquery框架，用某些框架是不是可以规避这些问题
4. 使用其他的方法，能否快速的绕过去，用某种方法代替，只要不在影响效果的情况下，能用即可
5. 抛弃IE6 7 8万恶的三个祖宗等低版本浏览器，时代在进步，体验差烂的技术终将会被淘汰，纵使要做兼容，如果在功能不影响的情况下，扁平化处理即可，也可提示用户浏览器进行升级处理
6. 渐进增强(向上兼容)与优雅降级(向下兼容)处理,前者一开始就针对低版本浏览器进行构建页面,完成基本的功能,然后针对高版本浏览器进行效果，交互，追加功能达到更好的体验,后者一开始就构建站点的完整功能,然后针对浏览器测试和修复,比如一开始使用css3就构建应用页面,然后逐步针对各大浏览器进行hack使其可以在低版本浏览器上正常浏览,大部分情况下,如果只优先考虑用户体验，那么选择优雅降级,如果考虑低版本，那么选择渐进增强,因为很多公司是以业务为导向的,在满足该情况下,在谈用户体验

> 浏览器的内核

`常见的四种:`

1. Trident(IE内核):IE浏览器 The world世界之窗，360,2345浏览器等(-ms)
2. Gecko:Firefox,MozillaSuite(-moz)
3. presto:opera浏览器(-o)
4. webkit内核浏览器: chrome(谷歌)，safari(-webkit)

其实列出来很无语，是有些面试时，总喜欢问的，记得有次面试时，就问了我浏览器内核，让我说出浏览器内核之间有什么区别，怎么渲染的，哎，说真的，能深入浏览器内核，深入引擎的，不是我说，逼格太高了，当时简直是想喷那人的，我觉得记得后面的前缀即可，在使用css3的某些属性时，记得在属性前加上不同版本的浏览器前缀即可，填写的规则是：从低版本往高版本写，属性最通用的写在最后面，至于更深入的研究的，自己花时间兴趣慢慢即可了，逼格高暂时我还真够不着
> 兼容1：低版本浏览器下，计算一定要精确，不要让子元素内容的宽高超出父元素设置的宽高，在IE6下，内容会撑开设置好的宽高

现象：IE6下，子元素设置为左右浮动时，会存在不对齐的情况

解决办法：精确的计算子元素的宽高度，不要让子元素内容的宽高超出父元素
![](http://i.imgur.com/U0cRMMM.png)
> 兼容2：在IE6元素浮动，如果宽度需要内容撑开，就给子元素加上浮动
现象：在IE67低版本下：设置左右浮动时，不起作用，独占一行显示

解决办法：子元素也设置浮动，可解决
![](http://i.imgur.com/H017g6Y.png)
> 兼容3：注意标签嵌套

现象：当p标签嵌套块级元素时，会出现诡异多出一个块级元素的情况

解决办法：合理的利用标签的嵌套，块级元素可嵌套行内元素，反之，则不行

p标签不能嵌套块级元素，这个问题很诡异，p标签是块级元素，div,h1~h6是块级元素，按理来说，块级元素是能嵌套块级元素的，但是此元素例外：块级元素是相当于是一个盒子，是用来承载装内容的，支持宽高，是用来布局的，行内元素：由自身内容撑大，不支持宽高（当然除了转化之外，升级标签）
![](http://i.imgur.com/jNK7W6w.png)
> 兼容4：IE6低版本下最小高度的问题

现象：IE6下设置最小高度时，默认会显示19px

解决办法：overflow:hidden
![](http://i.imgur.com/5Cw3dAP.png)
> 兼容5:margin传值，外边的合并问题，子元素添加margin会触发父元素

现象：子元素设置margin的情况下，会触发父元素

解决办法(如下5种方法可解决)

1. 父元素添加一边框border
2. 父元素添加一overflow:hidden(但是会隐藏子元素的溢出的内容)
3. 父元素添加一绝对定位position:absolute
4. 父元素添加一固定定位posiiton:fixed(除相对定位)
5. 父元素添加一浮动:float
关于浮动和相对定位的特性可参考前文的《从小小标签到绚目多彩的网页》《恰用position定位进行布局》就知道了
![](http://i.imgur.com/cjeHkuw.png)
> 兼容6：IE67下低版本浏览器双外边距问题

现象：在IE67低版本浏览器下，块级元素设置浮动时，并有横向的margin值时，横向的margin值会被放大两倍

解决办法：将其设置成display:inline;行内元素
![](http://i.imgur.com/yimge75.png)
> 兼容7：块级元素本身没有浮动，子元素设置了浮动，在低版本浏览器下有间隙问题

现象：在IE67低版本浏览器下，块级元素没有设置浮动，但子元素设置了浮动，在低版本浏览器下有一间隙

解决办法：父元素同样添加浮动(加上vertical-align:top也可解决)
![](http://i.imgur.com/93ts1P6.png)
> 兼容8：当一行子元素占有的宽度之和和父级的宽度相差超过3px,或者有不满行状态的时候,最后一行子元素的下margin在IE6下就会失效

现象：最后一行元素的margin值会在IE6低版本下失效

解决办法：方法1：父元素加高度，精确的计算固定的高度

方法2：子排元素填满，凑成偶数列
![](http://i.imgur.com/vquYi2f.png)
> 兼容9:IE6下文字溢出的问题，子元素的宽度和父级元素的宽度相差小于3px的时候，两个浮动元素之间有注释或者若然内嵌元素
现象：明明是一行文字，却出现两行文字

解决办法：用块级元素div，p等把注释和内嵌元素给包裹起来，便可解决
![](http://i.imgur.com/LUz1AdL.png)
> 兼容10:IE67下，子元素有相对定位的话，父级的overflow包不住子元素，父级也用相对定位

现象：子元素使用了相对定位，父元素包不住子元素问题

解决办法：给父元素加一相对定位或者绝对定位即可
![](http://i.imgur.com/Qrf43aS.png)
> 兼容11：在IE67下绝对定位元素宽高是奇数的时候，元素的right和bottom值会有1px的偏差》
显现：有一像素的偏差

解决办法：父元素的宽高尽量使用偶数
![](http://i.imgur.com/2g8Rsyg.png)
> 兼容12：在ie6下设置table的背景色会覆盖tbody设置的背景色

现象：低版本下设置table的背景色会覆盖tbody的背景色

解决办法：准确的给所要的元素添加背景色
![](http://i.imgur.com/FnYLKkp.png)
> 兼容13：IE67下低版本浏览器下input下表单上下有一像素的偏差问题

现象：低版本下浏览器下input下表单上下一像素偏差

解决办法：给input加上一浮动，本身如想去掉自身的边框,加上border:none即可
![](http://i.imgur.com/vzQ9wUD.png)
> 兼容14：低版本浏览器下输入框若背景图，当输入文字过多时，背景图会跟随着移动

现象：不断的输入文字，背景图跟着动

解决办法：将背景图设置给父元素
![](http://i.imgur.com/SDIOnHj.png)
> 兼容15：png图片在IE6浏览器的显示问题
现象：png在低版本浏览器下显示，出现背景透明不显示情况
解决办法:引入外部的一个js，做浏览器的判断，IE67低版本浏览器便加载这段js
DD_belatePNG.fix("添加背景的元素");至于这个处理png图片的js，度娘就可以找到 了
![](http://i.imgur.com/MJUBOXg.png)
> 兼容16：条件注释语句

现象：往往针对不同版本的浏览器，针对不同浏览器加载不同的css和js
写法：
![](http://i.imgur.com/9097noO.png)
> 兼容17：关于css hack问题

显现：同一段css在不同的版本显示不一样

解决办法：针对不同浏览器版本，属性前添加不同的前缀
IE67属性前加：+ - *

书写规则：从低版本到高版本依次书写，最为通用的写在最后面
![](http://i.imgur.com/2bHs14v.png)
> 兼容18：png滤镜 IE低版本浏览器下png图片不显示问题
现象：png图片在低版本浏览器不显示

解决办法：IE下滤镜处理
_filter:progid:DXImageTransform.Microsoft.AlphaImageLoader(src="png.png", sizingMethod="crop");
![](http://i.imgur.com/6O5IA6a.png)
> 兼容19：!important权重问题

现象：在IE6下，在important 后面在加一条同样的样式，会破坏掉important的作用，会按照默认的优先级顺序来走
![](http://i.imgur.com/H2MQRmf.png)
> 兼容20：给图片加a链接在IE8低版本浏览器，会出现蓝色的边框

现象：图片被嵌套a链接后，在低版本浏览器下出现蓝色的边框

解决办法：img:去除边框：border:none(border:0;)
> 兼容21：重置css样式

现象：不同浏览器对html标签默认的样式不同，外边距和内边距

解决办法：我们应该摒弃这种*{padding:0;,margin:0}方式，而是具体的在用到某些标签时，进行特定的处理，审查元素，看标签自身是否有默认的样式需要重置，确保在各个浏览器显示一致
![](http://i.imgur.com/LdfN7jh.png)
更多的重置样式，我觉得，用到什么就设置什么，就好了的，平时用得比较多的也就常用那几个标签，真正用到时，利用外部样式，保存在reset.css，引入到你所要用的页面即可。
好了，关于浏览器的兼容性的东西还是挺多的，不仅仅是有css的兼容，还有更多的是javascript的兼容，BOM，DOM相关的兼容性处理，比较繁琐，其实平时接触处理更多的还是相关浮动和定位的一些兼容性处理，兼容性的处理一直是我们必不可少的一门槛，移动端的适配，各个设备之间兼容性处理，都需要自己去不断的去积累和学习。不过对于兼容性的处理：我列如下自己的处理顺序:
1. 规范书写结构性html,认识标签的属性，不写css hsck的代码
2.  是css兼容性还是js的兼容性问题，缩小问题范围
3. 用比较成熟的一些框架：jquery,避免了兼容性
最后，还是总结下，本节图片比较多，更多的兼容是在处理IE67低版本浏览器，其实我觉得万恶的IE678三个祖宗终将是要被淘汰的，我们应顺应潮流,至于兼容性的处理，平时遇到了还是多总结下就好

`以下是本篇提点概要`

* 如何看待浏览器兼容性问题
* 如何的解决这种浏览器兼容性问题
* 浏览器的内核》
* 兼容1：低版本浏览器下，计算一定要精确，不要让子元素内容的宽高超出父元素设置的宽高，在IE6下，内容会撑开设置好的宽高
* 兼容2：在IE6元素浮动，如果宽度需要内容撑开，就给子元素加上浮动
* 兼容3：注意标签嵌套
* 兼容4：IE6低版本下最小高度的问题
* 兼容5:margin传值，外边的合并问题，子元素添加margin会触发父元素
* 兼容6：IE67下低版本浏览器双外边距问题
* 兼容7：块级元素本身没有浮动，子元素设置了浮动，在低版本浏览器下有间隙问题
* 兼容8：当一行子元素占有的宽度之和和父级的宽度相差超过3px,或者有不满行状态的时候,最后一行子元素的下margin在IE6下就会失效
* 兼容9:IE6下文字溢出的问题，子元素的宽度和父级元素的宽度相差小于3px的时候，两个浮动元素之间有注释或者若然内嵌元素》
* 兼容10:IE67下，子元素有相对定位的话，父级的overflow包不住子元素，父级也用相对定位
* 兼容11：在IE67下绝对定位元素宽高是奇数的时候，元素的right和bottom值会有1px的偏差
* 兼容12：在ie6下设置table的背景色会覆盖tbody设置的背景色
* 兼容13：IE67下低版本浏览器下input下表单上下有一像素的偏差问题
* 兼容14：低版本浏览器下输入框若背景图，当输入文字过多时，背景图会跟随着移动
* 兼容15：png图片在IE6浏览器的显示问题
* 兼容16：条件注释语句
* 兼容17：关于css hack问题
* 兼容18：png滤镜 IE低版本浏览器下png图片不显示问题
* 兼容19：!important权重问题
* 兼容20：给图片加a链接在IE8低版本浏览器，会出现蓝色的边框
* 兼容21：重置css样式

![](http://i.imgur.com/TPUpeKA.jpg)

`更多精彩内容,敬请关注微信itclan公众号`






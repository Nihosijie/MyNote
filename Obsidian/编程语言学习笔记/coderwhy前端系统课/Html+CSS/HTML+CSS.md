# HTML
## 文档声明
html文件的最上方的的一段文本称之为文档类型声明，用于声明文档类型
```html
<!DOCTYPE html>
```

声明文档是html5类型的，确保浏览器以html5语法来解析html文件。
必须放在文档最上方，不可省略，否则会出现兼容性问题。

## html元素
`<html>`元素表示一个html文件的根(顶级元素)，所以称之为**根元素**，所有其他元素是此元素的后代。

`<html lang="en">`，w3c标准建议为html元素加上一个lang属性，以方便语音合成工具确定要使用的发音，和帮助翻译软件选择规则。

`lang="en"`表示html文档的语言是英文。
`lang="zh-CN"`表示html文档的语言是中文。

## head元素
head元素规定了文档相关的配置信息(也称为元数据)，包括文档的标题，字符设置，引用的文档样式和脚本等

一般head元素至少会包含两个元素title和meta元素
```html

<title>网页的标题</title>
<meta charset="utf-8">

```

## body元素
body元素是网页的具体内容和结构

## Html元素

### h(heading)元素
标题元素，包含h1-h6，通常和seo优化有关

### p(paragraph)元素
p是段落，分段的意思，表示文本的一个段落
多个段落之间通常会有一定的间隔

### img(image)元素
img元素用来向网页中插入图片，是一个可替换元素。
常用属性有src(source)和alt(alternative)属性
src属性的值是需要插入图片的路径，是**必须**存在的
alt属性表示加载失败后显示的文字，或者当残障人士使用屏幕阅读器时会读取alt中的文字，**非必须**。

### img元素的路径
设置img元素的src时可以给图片设置两种路径：
1. 网络路径，一个URL地址
2. 本地路径：本电脑上图片的相对路径或绝对路径

本地图片的路径有两种表示方法：相对路径和绝对路径，相对路径是图片相对于html文件所处的位置，比较常用，绝对路径是从电脑根路径开始找到资源的路径，几乎不用。

### a(anchor)元素
html中的a(可称之为锚元素)，可以定义一个超链接，用于打开新的URL

a元素有两个常用的属性：
href(hypertext reference)属性，可以指定一个URL，也可以指定一个本地地址。
target可以选择在何处打开的资源，有四种值
```html
_blank 在新标签页打开
_self 在本页面打开
下面两种通常和iframe元素搭配使用
_parent 在父元素页面打开
_top 在嵌套的元素的最外层打开
```

### a元素 锚点链接
锚点链接可以实现跳转到网页的具体位置。
首先指定网页中元素的id属性
然后设置a的href值为要跳转元素的id值
```html

<p id=top>要跳转到的地方</p>


<a href="#top">点击跳转到p元素的位置</a>
```

### a元素 图片链接
可以用img元素配合a元素来实现点击图片跳转
```html
<a href="https://www.baidu.com"><img src="百度图片资源地址" alt="百度一下"></a>
```

### a元素 其他URL地址
a元素定义的URL不一定是打开网页的
```html
文件下载地址
https://github.com/coderwhy/HYMiniMall/archive/master.zip
调用邮件应用发送邮件
mailto:12345@qq.com

```

### iframe元素
iframe可以实现在一个网页中嵌套其他html文档
frameborder属性用于设置是否显示边框，1表示显示，0表示不显示。

```html
以下显示的代码片段为body中内容
inner.html
<a href="https://www.taobao.com" target="_top">打开淘宝</a>
outer.html
<iframe src="inner.html" class="inner" frameborder="1">
</iframe>
index.html
<iframe src="outer.html" class="outer" frameborder="1">
</iframe>
```
当a元素的target值设置为_parent时会在outer的iframe中打开淘宝
当a元素的target值设置为_top时会在最外层的index网页中打开淘宝


### div元素和span元素
div是division，分开分配的意思
span元素表示跨域、涵盖

div和span元素都是纯粹的盒子，都是被用来包裹内容的
div元素: 多个div元素包裹的内容会在不同的行显示
	通常用于作为其他元素的父元素，把其他元素包住，表示一个整体
	用于把网页分为多个独立的部分
span元素：多个span元素包裹的内容会在同一行显示
	默认情况下和普通文本没什么区别
	用于区分特殊文本和普通文本，比如用来显示一些关键字
	
	
### 不常用元素
- b元素：文本加粗
- strong元素：文本加粗
- i元素：文本倾斜
- em元素：斜体，但不应仅被用于斜体，通常用于标记需要用户着重标记的内容
- u：下划线
- br：换行，现在开发一般不用


### 全局属性
所有html元素都具有的属性
### 常用全局属性
- id：定义唯一标识符(ID)，该标识符在整个文档中必须是唯一的，其目的是在链接（使用片段标识符）、脚本或样式表(使用css)时标识元素。
- class：一个以空格分隔的元素类名(classes)列表，允许CSS和javascript以类选择器和DOM方法来选择和访问特定的元素。
- style：给元素添加内联样式
- title：包含表示与其所属元素相关的文本，这些信息通常可以作为提示展现给用户，但不是必须的。

# CSS
CSS表示层叠样式表(Cascading Style Sheet，简称CSS)是为网页添加样式的代码
CSS不算编程语言，不算标记语言，是一门样式表语言。
CSS是一门计算机语言，但是不是编程语言。
CSS语法
![[resources/CSS语法.png]]
- 声明(declaration)是一个单独的CSS规则，用于给指定的元素添加样式

## CSS链接方法
### 内联样式
内联样式直接处于元素开始标记的style属性中
```html
	<p style="color: red; font-size:30px;">内联样式</p>
```

###  内部样式表
```html
	在head中添加style元素，在其中设置元素样式
```

### 外部样式表
```html
	创建一个css文件，然后在head中添加
	<link rel="stylesheet" href="css路径">
```
在一个css文件中引用其他css文件可使用@import url(其他css文件的路径)

## CSS属性
### color 前景颜色
color用于设置元素的前景色，前景表示包括文字、装饰线、边框和外轮廓都会被该属性影响。

### background-color 背景色
设置元素的背景色

## 文本属性

### (常用)text-decoration 文字装饰
decoration是装饰/装饰品的意思

text-decoration常用取值：
- none 无装饰线，可用来去除a元素的下划线
- underline 下划线
- overline上划线
- line-through 中划线(删除线)

a元素具有下滑线的本质就是被添加了text-decoration属性

### (不常用)text-transform 大小写转换
用于设置文字的大小写及其转换

转换大小写更常用js实现
常用值
- caplitalize  使....首字母大写，资本化的意思，可将每个单词的首字符变为大写
- uppercase (大写字母)将每个单词的所有字符都变为大写
- lowercase (小写字母)将每个单词的所有字符都变为小写
- none 无影响

### (不常用)text-indent 首行缩进
用于设置第一行内容的缩进
**text-indent: 2em 刚好是缩进两个文字**

### (重要)text-align 文本对齐方式

text-align: 直译是设置文本的对齐方式
但其对所有行内元素都生效

常用值：
- left 左对齐
- right: 右对齐
- center 居中对齐
- justify 两端对齐

### (不常用)letter-space、word-space 间距
可设置字母、单词之间的间距，默认为0，可以设置为负数

## 字体属性
### (重要)font-size 字体大小
font-size决定字体的大小
可用`数值+单位`或者`百分比`
可用px或者em
em表示相对于父元素的倍数，1em就是100%，2em就是200%

### (重要)font-family 设置字体
font-family用于设置文字的字体名称
可以设置一个或者多个字体名称，浏览器会自动选择设置的第一个字体，如果计算机没有安装对应字体则向后寻找，直到字体可用。
也可以设置@font-face指定的可以下载的字体

### (重要)ont-weight 字体粗细
font-weight 用于设置字体粗细
可取100-900之间的整百值
normal为400
bold为700

加粗的标签默认就是bold

### (不常用)font-style 斜体
font-style 通常用于设置文字的常规、斜体显示
总共有三种值
normal:  常规显示
italic:  斜体
oblique: 倾斜 压斜的

### (不常用) font-varinant 小写字母显示形式
可以改变小写字母的显示形式，varinant是变形的意思
可以设置的值有
normal 正常
small-caps 将小写字母替换为缩小过的大写字母


### (常用)line-height  行高
line-height可以设置文本的行高
line-height是元素中每一行文本所占据的高度
height是元素的整体高度
当line-height和height相等时，文本垂直居中

### font缩写属性
font是一个缩写属性
可用来作为font-style  font-size  font-weight  font-variant line-height font-family属性的缩写
顺序为
font-style font-variant font-weight font-size/lineheight font-family

font-style font-variant font-weight可以随意调换顺序，也可以省略
/line-height可以省略，如果不省略需要跟在font-size后面
font-size font-family不可以调换顺序，不可以省略


## CSS选择器

### 通用选择器
`*` 所有元素都会被选中
一般用来给所有元素作一些通用的设置
比如内外边距或者重置内容

`效率较低，不建议使用`

### 简单选择器
包括`元素选择器`、`类选择器`、`id选择器`

### 属性选择器
拥有一个属性`[att]`
属性值等于某个值`[att=val]`

了解内容
- [attr*=val]：属性值包含某个val
- [attr^=val]：属性值以val开头
- [attr$=val]：属性值以val结尾
- [attr|=val]：属性值等于val或以val开头后面跟着-(就是val-开头)
- [attr~=val]：属性值包含val，如果有其他值必须以空格和val分割

### 后代选择器
所有后代以`空格`分隔
直系后代以`>` 分割

### 兄弟选择器
相邻兄弟使用 `+`
普遍兄弟使用`~`

### 选择器组
交集选择器需要紧密连接
```html
<div class="one">  交集选择器为div.one
<p id="pra"> 交集选择器 p#pra
```


并集选择器以 `,` 分隔
```html
<div class="one">
<p id="pra"> 
	
并集选择器为 .one, .pra
```


## 伪类
Psedo-classes
伪类是选择器的一种，通常用于选择处于某种状态的元素

### 动态伪类
a:link 未访问的链接
a:visited 已访问的链接
a:hover 鼠标挪动到链接上(最常用)
a:active 激活的连接，鼠标长按在上面未松开

遵循 `lvha` 原则，必须按照顺序才可以生效
除了a元素，:hover :active也能用在其他元素上

:focus
:focus指当前具有输入焦点的元素(能接受键盘输入)，例如文本框

因为链接a元素也可以使用tab键被聚焦，所以focus也可以用在a元素上

所以总体原则就是 LVFHA

 可以直接给a元素设置样式(比如color)，相当于给a的所有伪类设置了样式
 
 
 ## 伪元素
 - ::first-line
 - ::first-letter
 - ::before
 - ::after

上述伪元素也可以直接用单冒号，为了和伪类区分，建议使用双冒号。



### (不常用)::first-line ::first-letter
::first-line 可以为首行文本设置属性
::first-letter 可以为首字母设置属性

### (常用) ::before ::after
::before 可以在元素之前插入内容
::after 可以在元素之后插入内容
常通过 content属性来为一个元素添加修饰性的内容

## CSS属性继承
如果一个属性具备传递性，那么在某元素设置该属性后，其后代的该属性默认是父元素设置的属性，如果子元素自己设置了该属性，则覆盖掉父元素的设置，使用自己设置的值。

### (不用记忆)常用的可继承属性
![[resources/Pasted image 20230206114400.png]]

## CSS属性的重叠
对于一个元素来说，同一个属性可以通过不同的选择器给它重复设置，但是最终只会有一个属性生效

当多个样式被设置在同一个元素时，首先需要判断选择器的权重，权重大的生效，当选择器权重相同时，后设置的样式生效

## 选择器的权重
- !important 10000
- 内联样式 1000
- id选择器 100
- 类选择器、属性选择器、伪类 10
- 元素选择器、伪元素 1
- 通配选择器 0

![[resources/Pasted image 20230206114755.png]]

## HTML元素类型(块元素、行内元素)

当设置标题和段落时，我们会希望它们独占一行
而img/span/a等元素是对内容的细节性描述，不需要它们独占一行

为了区分，html通过css将元素分为了两类
`块级元素` 独占父元素的一行
`行内级元素` 多个行内级元素可以在父元素的同一行显示

## 通过CSS设置元素的类型(display)
可通过设置display属性来改变元素的类型
display有四个常用值：
- block 块级元素
- inline 行内级元素
- inline-block 对外表现为块元素，对内表现为行内元素
- none 隐藏元素

### display值的特性
- block元素
	- 独占一行
	- 可设置宽高
	- 高度默认由内容决定
- inline元素
	- 跟其他行内元素在同一行显示
	- 宽高由内容决定
	- 不可设置宽高
- inline-block
	- 可以和其他行内元素在同一行显示
	- 可设置宽高
	- 可理解为，对外是行内元素，对内是块级元素

一般来说
**块级元素可以包裹其他的块级元素**
但有一特殊情况
**p元素不可包裹其他块级元素**

**行内级元素不可包裹块级元素，只能包裹行内元素**


## 元素隐藏方法
1. display设置为none
	元素不显示并且不占位置
2. visibility设置为hidden
	设置为hidden时，元素不可见，但`会占据空间`
	设置为visible时，元素是可见的
3. rgba设置颜色，将a值设置为0
	元素不可见，但会占据空间，不会影响子元素的显示
4. opacity设置透明度为0
	设置整个元素的透明度，子元素也会受到影响

## CSS属性 overflow
overflow属性用于控制内容溢出时的行为，包含以下值
- visible 溢出内容可见
- hidden 溢出内容直接裁剪
- scroll 溢出内容被裁剪，但是可以通过滚动条查看，该值显示的滚动条占用的空间属于width和height，会始终显示gpdstc
- auto 自动根据内容大小来判断是否使用滚动条

## CSS样式不生效可能原因
- 选择器优先级太低
- 选择器没有选中对应元素
- CSS属性使用形式不对
	- 元素不支持此css属性，如span的宽高
	- 浏览器不支持css属性，旧版本浏览器可能不支持一些css3的属性
	- 被同类型的css属性覆盖，如font覆盖font-size

当出现css样式不生效时，可通过浏览器的开发者调试工具来调试和查错

## (重要)css盒子模型
html的每一个元素都可以看作为一个盒子，都包含以下四个属性
- 内容(content) 元素的width/height
- 内边距(padding) 元素和内容之间的间距
- 边框(border) 元素的边框
- 外边距(margin) 元素和元素之间的间距

### 内容(content)的宽高
设置内容是通过宽度和高度设置的
宽度设置: width
高度设置: height
对于`行内非替换元素`来说设置宽高时`无效`的
我们还可以设置如下属性
min-width 最小宽度，无论内容多少，宽度都大于等于min-width
max-width 最大宽度，无论内容多少，宽度都小于等于min-width
移动端适配时可以设置最大宽度和最小宽度
height两个属性同理，但不常用

### 内边距padding
padding属性用于设置盒子的内边距，通常用于设置盒子和内容之间的间距
padding包括四个方向
padding-top
padding-right
padding-bottom
padding-left
也可以缩写，直接设置padding
- 四个值，分别表示上右下左
- 三个值，表示上左右下
- 两个值，上下 左右
- 一个值 四个方向都是该值

### 边框border
边框用于设置盒子的边框
border具备width style 和color属性
border-width可设置四个方向上的边框宽度
border-style 可以设置边框的样式
![[resources/Pasted image 20230208113437.png]]
color设置边框的颜色

#### border-radius
可以用来设置边框的圆角
值可以为 `数值`和`百分比`

border-radius 包括四个角
- border-top-left-radius
- border-top-right-radius
- border-bottom-right-radius
- border-bottom-left-radius

如果元素是一个正方形，当所有角设置的值大于等于50%时会将正方形变成一个圆形

### 外边距 margin
margin属性用来设置盒子的外边距，通常用于元素和元素之间的间距
同样的，margin也可以在四个方向上分别设置
缩写属性也为顺时针方向

#### margin的传递
- margin-top传递：如果块级元素的顶线和其父元素的顶线重合，那么该元素的margin-top值会传递给父元素
- matrgin-bottom：如果子元素的底线和父元素的底部重合，并且父元素的高度为auto，那么这个块级元素的margin-bottom值会传递给父元素
- 如何防止出现传递问题？
	- 给父元素设置padding-top或者padding-bottom属性
	- 给父元素设置border
	- 触发BFC 设置overflow为auto

`建议`：margin一般用于设置兄弟之间的间距，padding一般用来设置父子元素之间的间距

#### 上下margin的折叠
垂直方向上两个margin有可能被合并为1个margin，这种现象叫做collapse(折叠)
- 水平方向上的margin永远不会折叠
- 折叠后margin取两者中较大的值
- 可以通过只设置1个元素的margin值来防止margin collapse

上下margin的折叠可以分为两种情况：
- 两个兄弟块级元素上下之间的折叠
	- ![[resources/Pasted image 20230208152133.png]]
- 父子块级元素之间的折叠
	- ![[resources/Pasted image 20230208152156.png]]

### 外轮廓outline
outline表示元素的外轮廓，不占用空间并且默认显示在border的外面
outline的相关属性有width、style和color，也可以简写，用法和border类似

可用来去除a，input元素的focus效果

### 盒子阴影 box-shadow
box-shadow属性可以设置一个或者多个阴影
每个阴影可用 < shadow > 表示，多个阴影之间用 `,` 隔开，从前到后叠加

shadow常见格式如下：
![[resources/Pasted image 20230208160053.png]]
用正则解读
- 第1个length：offset-x 水平方向上的偏移，正数往右偏移
-  第2个length：offset-y 垂直方向上的偏移，正数往下偏移
-  第3个length：  blur-radius，模糊半径
-  第4个length：  spred-radius，延伸半径
-  color：阴影的颜色，如果没有设置就使用color的颜色
-  inset 外框阴影变成内框阴影

### 文字阴影 text-shadow
text-shadow的用法类似box-shadow，用于给文字添加阴影效果
text-shadow常见格式如下：
![[resources/Pasted image 20230208161058.png]]
相当于box-shadow，不过它没有spread-radius的值


## 行内非替换元素的注意事项
以下元素对行内非替换元素不管用
width、height、margin-top、margin-bottom

以下元素对行内非替换元素的效果比较特殊
padding-top、padding-bottom、上下方向上的border

## CSS属性 box-sizing
box-sizing用来设置盒子模型中宽高的行为
- content-box
	- padding、border都布置在width、height外面
- border-box
	- padding、border都布置在width、height里面


### box-sizing: content-box

![[resources/Pasted image 20230208163212.png]]
元素的实际占用宽度 = border + padding + width
元素的实际占用高度 = border + padding + height


### box-sizing: border-box
![[resources/Pasted image 20230208164723.png]]
元素的实际占用宽度 = width
元素的实际占用高度 = height

## 元素的水平居中方案
在一些需求中，需要元素在父元素中水平居中显示(父元素一般是块级元素，inline-block)

- 行内级元素(包括inline-block)
 水平居中：在父元素中设置text-align: center;
 
 - 块级元素 (block)
 水平居中：margin: 0 auto
 
 

## CSS背景

### background-imt 背景图片
background-image 用于设置元素的背景图片，被设置的元素必须有宽和高

img会‘盖在(不是覆盖)’ 在color的上面
如果设置了多张背景图片，会将设置的第一张图片显示在最上面，其他图片按照顺序叠在下面

### background-repeat 背景平铺
background-repeat 用于设置图片是否需要平铺
常见设置：
- repeat：平铺
- no-repeat 不平铺
- repeat-x 只在水平方向上平铺
- repeat-y 只在垂直方向上平铺

### background-size 背景大小
该属性用于设置背景图片的大小
- auto 默认值，以背景图片本身的大小显示
- cover 缩放背景图，以完全覆盖铺满元素，可能背景图片的部分看不见
- contain：缩放背景图，直到宽度或者高度到达元素边缘，图片会保持宽高比进行缩放
- \<percentage\> 百分比，相对于背景区(background positioning area)
- length 具体大小，比如100px
![[resources/Pasted image 20230219211637.png]]

### background-position 背景位置
用于设置背景图片在水平、垂直方向上的具体位置
- 可以设置具体的数值，比如10px，20px
- 水平方向上可以设值：left、center、right
- 垂直方向上可以设置：top、center、bottom
- 如果只设置了一个方向上的值，则另一个方向上的值默认为center

### background-attachment 背景固定
决定背景图像的位置是在视口内固定，或者随着包含它的区块滚动，可以设置为：
- scroll 表示背景相对于元素本身固定，而不是随着它的内容滚动
- local 表示背景相对于元素的内容固定，如果一个元素拥有滚动机制，则背景也将会随着元素的内容滚动
- fixed：此关键属性表示背景相对于视口固定，即使一个元素拥有滚动机制，背景也不会随着元素的内容滚动。

### background 简写属性
![[resources/Pasted image 20230219212143.png]]

background-size 可以省略，如果不省略，/background-size必须紧跟在background-position的后面
其他属性也都可以省略，而且顺序任意
### background-image和img对比
 利用background-image和img都能够实现显示图片的需求，在开发中该如何选择？
 
 ![[resources/Pasted image 20230219214827.png]]
 
 总结：
 img，可以作为网页内容的重要组成部分，比如广告图片、LOGO图片、文章配图、产品图片
 background-image，可有可无，有的话能让网页更加美观，没有的话也不影响用户获取完整的网页内容。
 
 
 ## 列表
 Html提供了3组常用的用来展示列表的元素
 - 有序列表：ol li
 - 无序列表：ul li
 - 定义列表：dl dt dd

### 有序列表 Ordered list
ol ordered list 
有序列表，直接子元素只能是li

li list item
列表中的每一项


### 无序列表 Unordered list
ul unordered list 
无序列表，直接子元素只能是li
li list item
列表中的每一项

### 定义列表
dl definition list
定义列表，直接子元素只能是dt、dd

dt definition term
列表中的每一项的项目名

dd definition description
列表中的每一项的具体描述，是对dt的描述、解释和补充
一个dt后面一般会紧跟着1个或者多个dd

## 表格
表格中最常见的元素有
table 表格
tr table row 表格中的行
td table data 表格中的单元格
表格中有许多标签属性，但是现在一般都使用css属性设置

其他元素
thead 表格的表头
tbody 表格的主题
tfoot 表格的页脚
caption 表格的标题
th表格的表头单元格

### 单元格的合并
跨行合并 rowspan 在上面的单元格设置rowspan属性，并且删除后面tr中td

跨列合并 colspan 在左边的单元格设置colspan属性，并且删除当前tr右边的td


## 表单
HTML表单元素是和用户交互最重要的方式之一，在很多网站都需要使用表单

### 常见的表单元素
- form 表单，一般情况下，其他表单相关元素都是它的后代元素
- input 单行文本输入框、单选框、复选框、按钮等元素
- textarea 多行文本框
- select、option 下拉选择框
- button 按钮
- label 表单元素的标题


### input元素
input是表单中使用最多的元素
input元素有如下常见属性：
type：input的类型
- text 文本输入框
- password 密文输入框
- radio 单选框
- checkbox 复选框
- button 按钮
- reset 重置按钮
- submit 提交表单数据给服务器
- file 文件上传
- readonly 只读
- disabled 禁用
- checked 默认被选中
	当type是radio或者checkbox才可以使用
- autofocus 当页面加载时，自动聚焦
- name 名字
	在提交数据给服务器时，用于区分数据类型
- value 取值

### 布尔属性 (boolean attributes)
常见的布尔属性有disabled、checked、readonly、multiple、autofocus、selected

布尔属性可以没有属性值，写上属性名就代表了使用了这个属性


### 表单按钮
表单中的按钮可以实现以下的效果
- 普通按钮(button) 使用value属性设置按钮文字
- 重置按钮(reset) 重置它所属form的所有表单元素(包括input，textarea，select)
- 提交按钮(submit) 提交它所属form的表单数据给服务器


### label 标签
label元素一般和input配合使用，用以表示input的标题
label可以和某个input绑定，点击label就可以激活对应的input

### 选择类型的使用
对于类型为radio的单选按钮，需要设置相同的name属性才可以使其实现单选效果

对于类型为checkbox的复选按钮，对于同一类型的checkbox需要设置相同的name

### textarea的使用
- cols 列数
- rows 行数
- resize 缩放属性
	- none 禁止缩放
	- horizontal 水平缩放
	- vertical 垂直缩放
	- both 水平垂直缩放

### select和option的使用
option是select 的子元素，一个opeion代表一个选项

selecy常用属性
	multiple 可以多选
	size 显示多少项
option常用属性
	selected默认被选中
	
### form常见的属性
form元素是整个表单元素的父元素
	form可以将整个表单当作一个整体来进行操作
	比如对整个表单进行重置或者提交
	
	
form常用属性
- action 表单提交的地址
- method 表单提交的方式
- target 提交表单时的页面打开方式


## 结构伪类
- :nth-child() 父元素中的第几个元素
- p:nth-child() 父元素中的第几个元素，且这个元素是p元素
- nth-last-child() 从后往前数第几个元素
- p:nth-of-type() 第几个p元素
- first-child 第一个子元素
- last-child 最后一个子元素
- first-of-type 第一个该类型的子元素
- last-of-type 最后一个该类型的子元素
- only-child 是父元素中唯一的子元素
- only-of-child 是父元素中唯一的这种类型的子元素
- :root 根元素，也就是html元素
- :empty 代表里面是完全空白的元素

否定伪类 (negation pesudo-class)

:not() 的格式就是 :not(x)
x是一个简单选择器
可以是元素\通用\属性\类\id\伪类(除否定伪类)

:not(x) 表示除了x以外的元素
### 1.1 less-初见

​	less是一种动态样式语言，属于css预处理器的范畴，它扩展了 CSS 语言，增加了变量、Mixin、函数等

特性，使 CSS 更易维护和扩展LESS 既可以在 客户端 上运行 ，也可以借助Node.js在服务端运行。

```
less的中文官网：http://lesscss.cn/
bootstrap中less教程：http://www.bootcss.com/p/lesscss/
```

#### 1.1.1 Less编译工具

​	koala 官网:www.koala-app.com 

```css
//css
#wrap{
    position: relative;
    width: 300px;
    height: 300px;
    border: 1px solid;
    margin: 0 auto;
}
#inner{
    width: 100px;
    height: 100px;
    background: pink;
    position: absolute;
    margin: 0 auto;
}
```

```less
//less
#wrap{
    position: relative;
    width: 300px;
    height: 300px;
    border: 1px solid;
    margin: 0 auto;
	#inner{
        width: 100px;
        height: 100px;
        background: pink;
        position: absolute;
        margin: 0 auto;
	}
}
```

### 1.2 less-基础

#### 1.2.1 less中的注释

​	以//开头的注释，不会被编译到css文件中

​	以/**/包裹的注释会被编译到css文件中 

#### 1.2.2  less中的变量

​	使用@来申明一个变量：@pink：pink;

​	1.作为普通属性值只来使用：直接使用@pink

​	2.作为选择器和属性名：#@{selector的值}的形式

​	3.作为URL：@{url}

```less
/*这是想暴露出去的注释*/
//这是见不得人的注释
@color:deeppink;	//属性值变量
@m:margin;			//属性名变量
@selector:#wrap;	//选择器变量  
*{
    @{m}: 0;
    padding: 0;
}
@{selector}{
    position: relative;
    width: 300px;
    height: 400px;
    border: 1px solid;
    margin: 0 auto;
    .inner{
        position: absolute;
        left: 0;
        right: 0;
        top: 0;
        bottom: 0;
        margin: auto;
        background: @color;
        height: 100px;
        width: 100px;
    }
}
```

​	4.变量的延迟加载

```less
@var: 0;
.class {	
@var: 1;
    .brass {
      @var: 2;
      three: @var;	//{}块级作用域，等{}内所有代码解析完成，再来看@var等于多少
      @var: 3;
    }
  one: @var;  
}
```

```css
//编译后
.class {
  one: 1;
}
.class .brass {
  three: 3;
}
```

#### 1.2.3 less中的嵌套规则

​	1.基本嵌套规则

​	2.&的使用

```less
/*这是想暴露出去的注释*/
//这是见不得人的注释
@color:deeppink;
*{
    margin: 0;
    padding: 0;
}
#wrap{
    position: relative;
    width: 300px;
    height: 400px;
    border: 1px solid;
    margin: 0 auto;
    .inner{
        position: absolute;
        left: 0;
        right: 0;
        top: 0;
        bottom: 0;
        margin: auto;
        background: @color;
        height: 100px;
        width: 100px;
        &:hover{	//&少掉会多个空格，代表跟.inner平级
            background: pink;
        }
    }
}
```

```css
/*这是想暴露出去的注释*/
* {
  margin: 0;
  padding: 0;
}
#wrap {
  position: relative;
  width: 300px;
  height: 400px;
  border: 1px solid;
  margin: 0 auto;
}
#wrap .inner {
  position: absolute;
  left: 0;
  right: 0;
  top: 0;
  bottom: 0;
  margin: auto;
  background: #ff1493;
  height: 100px;
  width: 100px;
}
#wrap .inner:hover {
  background: pink;
}
```

#### 1.2.4 less中@规则嵌套和冒泡

​	@ 规则（例如 `@media` 或 `@supports`）可以与选择器以相同的方式进行嵌套。@ 规则会被放在前面，同一规则集中的其它元素的相对顺序保持不变。这叫做冒泡（bubbling）。

```less
.component {
  width: 300px;
  @media (min-width: 768px) {
    width: 600px;
    @media  (min-resolution: 192dpi) {
      background-image: url(/img/retina2x.png);
    }
  }
  @media (min-width: 1280px) {
    width: 800px;
  }
}
```

编译为：

```css
.component {
  width: 300px;
}
@media (min-width: 768px) {
  .component {
    width: 600px;
  }
}
@media (min-width: 768px) and (min-resolution: 192dpi) {
  .component {
    background-image: url(/img/retina2x.png);
  }
}
@media (min-width: 1280px) {
  .component {
    width: 800px;
  }
}
```

### 1.3 less-混合1

​	混合就是将一系列属性从一个规则集引入到另一个规则集的方式

​	1.普通混合  

​	2.不带输出的混合

​	3.带参数的混合

​	4.带参数并且有默认值的混合

​	5.带多个参数的混合

​	6.命名参数

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title></title>
		<link rel="stylesheet" type="text/css" href="css/01.css"/>
	</head>
	<body>
		<div id="wrap">
			<div class="inner"></div>
			<div class="inner2"></div>
		</div>
	</body>
	<script src="less/less.min.js"></script>
</html>
```

```less
//方式一：.juzhong 普通混合 --->输出到css文件中
//方式二：.juzhong() 不带输出的混合和 --->带上()后不输出到css文件中
//方式三：.juzhong(@w,@h,@c) 形参实参个数要对应
//方式四：.juzhong(@w:10px,@h:10px,@c:pink) 带参数的混合，添加默认初始值
.juzhong(@w:10px,@h:10px,@c:pink){  
    position: absolute;
    left: 0;
    right: 0;
    top: 0;
    bottom: 0;
    margin: auto;
    background: @c;
    height: @h;
    width: @w;
}
#wrap{
    position: relative;
    width: 300px;
    height: 400px;
    border: 1px solid;
    margin: 0 auto;
    .inner{
       //方式一、二：.juzhong;
       .juzhong(100px ,100px,pink);	 //方式五：带多个参数的混合，可以覆盖最开始设置的默认值
    }
    .inner2{
       //方式一、二：.juzhong;
       .juzhong();	//方式四：有默认值后不传实参就不会报错
       //方式六：.juzhong(@c:black); 命名参数，可以指定只改变颜色，当形参与实参不匹配时，可以指定传给谁
    }
}
```

### 1.4 less-混合2

​	7.匹配模式

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title></title>
		<link rel="stylesheet" type="text/css" href="css/03.css"/>
	</head>
	<body>
		<div id="wrap">
			<div class="sjx"></div>
		</div>
	</body>
</html>
```

```less
//03.less
@import "./triangle.less"; //导入一个 .less 文件,如果导入的文件是 .less 扩展名，则可以将扩展名省略掉。
#wrap .sjx{
   .triangle(R,40px,yellow)
}
```

```less
//triangle.less 混合库
.triangle(@_,@wwww,@ccccc){  //后面两个形参要对应个数，命名可以不一样
    width: 0px;
    height: 0px;
    overflow: hidden; 
}

.triangle(L,@w,@c){
    border-width: @w;
    border-style:dashed solid dashed dashed;
    border-color:transparent @c transparent transparent ;
}

.triangle(R,@w,@c){
    border-width: @w;
    border-style:dashed  dashed dashed solid;
    border-color:transparent  transparent transparent @c;
}

.triangle(T,@w,@c){
    border-width: @w;
    border-style:dashed  dashed  solid dashed;
    border-color:transparent  transparent @c transparent ;
}

.triangle(B,@w,@c){
    border-width: @w;
    border-style:solid dashed  dashed dashed;
    border-color:@c transparent  transparent transparent ;
}
```

​	8.arguments变量

```html
<link rel="stylesheet" type="text/css" href="css/04.css"/>
```

```less
//04.less
.border(@w,@style,@c){
    border: @arguments;
}
#wrap .sjx{
   .border(1px,solid,black)
}
```

### 1.5 less-运算

​	算术运算符 `+`、`-`、`*`、`/` 可以对任何数字、颜色或变量进行运算。如果可能的话，算术运算符在加、减或比较之前会进行单位换算。计算的结果以最左侧操作数的单位类型为准。如果单位换算无效或失去意义，则忽略单位。无效的单位换算例如：px 到 cm 或 rad 到 % 的转换。

#### 1.5.1 加减

```less
@rem:100rem;
#wrap .sjx{
   width:(100 + @rem)
}
// 所有操作数被转换成相同的单位
@conversion-1: 5cm + 10mm; // 结果是 6cm
@conversion-2: 2 - 3cm - 5mm; // 结果是 -1.5cm

// conversion is impossible
@incompatible-units: 2 + 5px - 3cm; // 结果是 4px

// example with variables
@base: 5%;
@filler: @base * 2; // 结果是 10%
@other: @base + @filler; // 结果是 15%
```

#### 1.5.2 乘除

​	乘法和除法不作转换。因为这两种运算在大多数情况下都没有意义，一个长度乘以一个长度就得到一个区域，而 CSS 是不支持指定区域的。Less 将按数字的原样进行操作，并将为计算结果指定明确的单位类型。

```less
@base: 2cm * 3mm; // 结果是 6cm
```

#### 1.5.3 颜色进行算术运算

```less
@color: (#224488 / 2); // 结果是 #112244
background-color: #112244 + #111; // 结果是 #223355
//不过，你会发现 Less 提供的 色彩函数 更有用。
```

### 1.6 less-复习

   变量

​        @

​        变量的延迟加载

​        变量是块级作用域

​    嵌套

​        &:平级

​    混合

​        什么是混合？

​        	将一系列的规则集引入另一个规则集中（ctrl c + ctrl v）

​        	混合的定义在less规则有明确的指定，使用.的形式来定义

​        普通混合（编译到原生css中的）

​        不带输出的混合（加双括号）

​        带参数的混合

​        带默认值的混合

​        匹配模式

​        arguments

​    计算

​        加减乘除   计算的一方带单位就可以

​    继承	

### 1.7 less-继承

​	性能比混合高

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title></title>
		<link rel="stylesheet" type="text/css" href="css/mixin.css"/>
	</head>
	<body>
		<div id="wrap">
			<div class="inner">
				inner1
			</div>
			<div class="inner">
				inner2
			</div>
		</div>
	</body>
</html>
```

```less
//juzhong-mixin.less
.juzhong(@w,@h,@c){
    position: absolute;
    left: 0;
    right: 0;
    bottom: 0;
    top: 0;
    margin: auto;
    width: @w;
    height: @h;
    background: @c;
}
```

```less
//mixin.less
*{
    margin: 0;
    padding: 0;
}

@import "mixin/juzhong-mixin.less";
#wrap{
    position: relative;
    width: 300px;
    height: 300px;
    border: 1px solid;
    margin: 0 auto;
    .inner{
        &:nth-child(1){
           .juzhong(100px,100px,deeppink);
        }
        &:nth-child(2){
           .juzhong(50px,50px,yellow);
        }
    }
}
```

```css
//mixin.css
* {
  margin: 0;
  padding: 0;
}
#wrap {
  position: relative;
  width: 300px;
  height: 300px;
  border: 1px solid;
  margin: 0 auto;
}
#wrap .inner:nth-child(1) {
  position: absolute;
  left: 0;
  right: 0;
  bottom: 0;
  top: 0;
  margin: auto;
  width: 100px;
  height: 100px;
  background: #ff1493;
}
#wrap .inner:nth-child(2) {
  position: absolute;
  left: 0;
  right: 0;
  bottom: 0;
  top: 0;
  margin: auto;
  width: 50px;
  height: 50px;
  background: #ffff00;
}
```

​	灵活度比混合低

```html
<link rel="stylesheet" type="text/css" href="css/extend.css"/>
```

```less
//juzhong-extend.less
.juzhong{
    position: absolute;
    left: 0;
    right: 0;
    bottom: 0;
    top: 0;
    margin: auto;
}

.juzhong:hover{
    background: red!important;
}
```

```less
//extend.less
*{
    margin: 0;
    padding: 0;
}

@import "mixin/juzhong-extend.less";
#wrap{
    position: relative;
    width: 300px;
    height: 300px;
    border: 1px solid;
    margin: 0 auto;
    .inner{
        &:extend(.juzhong all);
        &:nth-child(1){
           width: 100px;
           height: 100px;
           background: pink;
        }
        &:nth-child(2){
           width: 50px;
           height: 50px;
           background: yellow;
        }
    }
}
```

```css
//extend.css
* {
  margin: 0;
  padding: 0;
}
.juzhong,
#wrap .inner {
  position: absolute;
  left: 0;
  right: 0;
  bottom: 0;
  top: 0;
  margin: auto;
}
.juzhong:hover,
#wrap .inner:hover {
  background: red!important;
}
#wrap {
  position: relative;
  width: 300px;
  height: 300px;
  border: 1px solid;
  margin: 0 auto;
}
#wrap .inner:nth-child(1) {
  width: 100px;
  height: 100px;
  background: pink;
}
#wrap .inner:nth-child(2) {
  width: 50px;
  height: 50px;
  background: yellow;
}
```

### 1.8 less-避免编译

```less
//在 Less 3.5+ 版本中，许多以前需要“引号转义”的情况就不再需要了。
*{
    margin: 100 *  10px;
    padding: ~"calc(10px + 100)";
}
```

```css
*{
  margin: 1000px;
  padding: calc(10px + 100);
}
```

### 2.1 less-函数（Functions）

​	Less 内置了多种函数用于转换颜色、处理字符串、算术运算等。这些函数在[Less 函数手册](https://less.bootcss.com/functions/)中有详细介绍。

​	函数的用法非常简单。下面这个例子将介绍如何利用 percentage 函数将 0.5 转换为 50%，将颜色饱和度增加 5%，以及颜色亮度降低 25% 并且色相值增加 8 等用法：

```less
@base: #f04615;
@width: 0.5;

.class {
  width: percentage(@width); // returns `50%`
  color: saturate(@base, 5%);
  background-color: spin(lighten(@base, 25%), 8);
}
```

#### 2.1.1 逻辑函数

**如果 **

根据条件返回两个值之一

```less
@some: foo;

div {
    margin: if((2 > 1), 0, 3px);
    color:  if((iscolor(@some)), @some, black);
}
```

编译为：

```css
div {
    margin: 0;
    color:  black;
}
```

**布尔值**

评估为真或假

#### 2.1.2 字符串函数

**％ 格式**

该函数`%(string, arguments ...)`格式化一个字符串

**代替**

替换字符串中的文本。

#### **2.1.3 列出函数**

**长度**

返回值列表中的元素数。

例子：

```less
@list: "banana", "tomato", "potato", "peach";
n: length(@list);
```

输出：

```css
n: 4;
```

**提炼**

返回列表中指定位置的值。

例子：

```less
@list: apple, pear, coconut, orange;
value: extract(@list, 3);
```

输出：

```css
value: coconut;
```

**范围**

生成跨越一系列值的列表

例子：

```less
value: range(4);
```

输出：

```css
value: 1 2 3 4;
```

**每个**

例子：

```less
@selectors: blue, green, red;

each(@selectors, {
  .sel-@{value} {
    a: b;
  }
});
```

输出：

```css
.sel-blue {
  a: b;
}
.sel-green {
  a: b;
}
.sel-red {
  a: b;
}
```

**设置变量名each()**

例子：

```less
.set-2() {
  one: blue;
  two: green;
  three: red;
}
.set-2 {
  // Call mixin and iterate each rule
  each(.set-2(), .(@v, @k, @i) {
    @{k}-@{i}: @v;
  });
}
```

输出：

```css
.set-2 {
  one-1: blue;
  two-2: green;
  three-3: red;
}
```

### 2.2 less-命名空间和访问符

​	有时，出于组织结构或仅仅是为了提供一些封装的目的，你希望对混合（mixins）进行分组。你可以用 Less 更直观地实现这一需求。假设你希望将一些混合（mixins）和变量置于 `#bundle` 之下，为了以后方便重用或分发：

```less
#bundle() {
  .button {
    display: block;
    border: 1px solid black;
    background-color: grey;
    &:hover {
      background-color: white;
    }
  }
  .tab { ... }
  .citation { ... }
}
//现在，如果我们希望把 .button 类混合到 #header a 中，我们可以这样做：
#header a {
  color: orange;
  #bundle.button();  // 还可以书写为 #bundle > .button 形式
}
//注意：如果不希望它们出现在输出的 CSS 中，例如 #bundle .tab，请将 () 附加到命名空间（例如 #bundle()）后面。
```

编译为：

```css
#header a {
  color: orange;
  display: none;
  border: 1px solid black;
  background-color: grey;
  height: 1px;
}
#header a:hover {
  background-color: white;
}
```

### 2.3 less-映射（Maps）

​	从 Less 3.5 版本开始，你还可以将混合（mixins）和规则集（rulesets）作为一组值的映射（map）使用。

```less
#colors() {
  primary: blue;
  secondary: green;
}

.button {
  color: #colors[primary];
  border: 1px solid #colors[secondary];
}
```

编译为：

```less
.button {
  color: blue;
  border: 1px solid green;
}
```

### 2.4 作用域（Scope）

​	Less 中的作用域与 CSS 中的作用域非常类似。首先在本地查找变量和混合（mixins），如果找不到，则从“父”级作用域继承。

```less
@var: red;

#page {
  @var: white;
  #header {
    color: @var; // white
  }
}
```

​	与 CSS 自定义属性一样，混合（mixin）和变量的定义不必在引用之前事先定义。因此，下面的 Less 代码示例和上面的代码示例是相同的：

```less
@var: red;

#page {
  #header {
    color: @var; // white
  }
  @var: white;
}
```

参见：懒加载
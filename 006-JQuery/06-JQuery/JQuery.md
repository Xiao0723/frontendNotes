### jQuery学习笔记

#### 1.jQuery

##### 1.1 初识jQuery

```javascript
//本地引入
<script type="text/javascript" src="js/jquery-1.12.3.js"></script>
//远程引入
<script src="https://cdn.bootcss.com/jquery/1.12.4/jquery.js"></script>

<script type="text/javascript">    
//HTML结构
$('body').append('<input type="submit" value="btn1" id="btn1">')
$('body').append('<input type="submit" value="btn2" id="btn2">')
$('body').append('<input type="text" id="username" value="username值">')

//需求: 点击"确定"按钮, 提示输入的值
//使用原生DOM
window.onload = function () {
	var btn1 = document.getElementById('btn1')
    btn1.onclick = function () {
    var username = document.getElementById('username').value
        alert(username)
    }
}

//使用jQuery实现
jQuery(function () {//绑定文档加载完成的监听
	var $btn2 = $('#btn2')
	$btn2.click(function () {// 给btn2绑定点击监听
		var username = $('#username').val()
        alert(username)
    })
})
</script>
```

#### 2.jQuery的2把利器

##### 2.1 jQuery核心函数

\* 简称: jQuery函数($/jQuery)

\* jQuery库向外直接暴露的就是$/jQuery

\* 引入jQuery库后, 直接使用$即可

\* 当函数用: $(xxx)

\* 当对象用: $.xxx()

##### 2.2 jQuery核心对象

\* 简称: jQuery对象

\* 得到jQuery对象: 执行jQuery函数返回的就是jQuery对象

\* 使用jQuery对象: $obj.xxx()

```javascript
//1. jQuery函数: 直接可用
console.log($, typeof $)   	//$是一个function
console.log($ === jQuery) 	//（true）$与jQuery等同
console.log($ === window.$) //（true）$是一个全局函数

//2. jQuery对象: 执行jQuery函数得到它
console.log($() instanceof Object) //（true）"object"这个对象就是jQuery对象
/*
  (function (window) {
    var jQuery = function () {
      return new xxx()
    }
    window.$ = window.jQuery = jQuery
  })(window)
*/
```

#### 3.jQuery核心函数

##### 3.1 作为一般函数调用: $(param)

\* 参数为函数 : 当DOM加载完成后，执行此回调函数

\* 参数为选择器字符串: 查找所有匹配的标签, 并将它们封装成jQuery对象

\* 参数为DOM对象: 将dom对象封装成jQuery对象

\* 参数为html标签字符串 (用得少): 创建标签对象并封装成jQuery对象

##### 3.2 作为对象使用: $.xxx()

\* $.each() : 隐式遍历数组

\* $.trim() : 去除两端的空格

```javascript
<script type="text/javascript">
//html结构
$('body').append('<div></div>')
$('<button id="btn">测试</button><br/>').appendTo('div')
$('<input type="text" name="msg1"/><br/>').appendTo('div')
$('<input type="text" name="msg2"/><br/>').appendTo('div')

/*需求1. 点击按钮:显示按钮的文本,显示一个新的输入框*/
//1.1参数为函数:当DOM加载完成后，执行此回调函数
$(function () { //绑定文档加载完成的监听
    //1.2参数为选择器字符串: 查找所有匹配的标签, 并将它们封装成jQuery对象
	$('#btn').click(function () { //绑定点击事件监听
    	//this是什么? 发生事件的dom元素(<button>)
    	//1.3参数为DOM对象: 将dom对象封装成jQuery对象
    	alert($(this).html())	//alert(this.innerHTML) 原生js
      	//1.4参数为html标签字符串 (用得少): 创建标签对象并封装成jQuery对象
      	$('<input type="text" name="msg3"/><br/>').appendTo('div')
    })
})

/*需求2. 遍历输出数组中所有元素值*/
var arr = [123, 'demo', true]
//1.$.each()隐式遍历数组
$.each(arr, function (index, item) {
	console.log('第' + (index + 1) + '个元素的值为' + item)
})

/*需求3. 去掉"  my deom  "两端的空格*/
var str = "  my deom  "
//2.$.trim()去除两端的空格
console.log(str.trim() === 'my deom') //原生js
console.log($.trim(str) === 'my deom') //true
</script>
```

#### 4.jQuery对象

##### 4.1 jQuery对象是一个包含所有匹配的任意多个dom元素的伪数组对象

```javascript
/*伪数组可以理解为类似数组的一个集合,常见的有俩个,一个是arguments还有一个是DOM的children属性，获取回来的子节点集合。他们与数组一样，具有索引(下标)和length属性。可以通过for循环写循环语句去循环遍历。*/
//自定义一个伪数组
var weiArr = {}
weiArr.length = 0
weiArr[0] = 'yrk'
weiArr.length = 1
weiArr[1] = 0723
weiArr.length = 2
for (var i = 0; i < weiArr.length; i++) {
	var obj = weiArr[i]
    console.log(i, obj)
}
//普通数组有很多数组的方法,而伪数组却没有
console.log(weiArr.forEach) //undefined
```

##### 4.2 基本行为

\* size()/length: 包含的DOM元素个数

\* [index]/get(index): 得到对应位置的DOM元素

\* each(): 遍历包含的所有DOM元素

\* index(): 得到在所在兄弟元素中的下标

```javascript
<script type="text/javascript">
//html结构
$('body').append('<div></div>') //添加div，避免遇到index()得到的不是准确下标
$('div').append('<button>测试一</button>')
$('div').append('<button>测试二</button>')
$('div').append('<button id="btn3">测试三</button>')
$('div').append('<button>测试四</button>')

//需求1. 统计一共有多少个按钮
$(function () {
var $buttons = $('div > button')
/*size()/length: 包含的DOM元素个数*/
console.log($buttons.size(), $buttons.length)

//需求2. 取出第2个button的文本
/*[index]/get(index): 得到对应位置的DOM元素*/
console.log($buttons[1].innerHTML, $buttons.get(1).innerHTML)

//需求3. 输出所有button标签的文本
/*each(): 遍历包含的所有DOM元素*/
$buttons.each(function () {
	console.log(this.innerHTML)
})
/*回调函数可以传入形参
$buttons.each(function (index, domEle) {
  	console.log(index, domEle.innerHTML, this)
})
*/

//需求4. 输出'测试三'按钮是所有按钮中的第几个
/*index(): 得到在所在兄弟元素中的下标*/
console.log($('#btn3').index())    
})
</script>
```

#### 5.基本选择器

##### 5.1 是什么?

  \- 有特定格式的字符串

##### 5.2 作用

  \- 用来查找特定页面元素

##### 5.3 基本选择器

  \- #id : id选择器

  \- element : 元素选择器

  \- .class : 属性选择器

  \- * : 任意标签

  \- selector1,selector2,selectorN : 取多个选择器的并集(组合选择器)

  \- selector1selector2selectorN : 取多个选择器的交集(相交选择器)

```javascript
<script type="text/javascript">
//html结构
$('body').append('<div id="div1" class="box">div1(class="box")</div>')
$('body').append('<div id="div2" class="box">div2(class="box")</div>')
$('body').append('<div id="div3">div3</div>')
$('body').append('<span class="box">span(class="box")</span><br>')
$('body').append('<ul></ul>')
$('ul').append('<li>AAAAA</li>')
$('ul').append('<li title="hello">BBBBB(title="hello")</li>')
$('ul').append('<li class="box">CCCCC(class="box")</li>')
$('ul').append('<li title="hello">DDDDDD(title="hello")</li>')

//1. 选择id为div1的元素
$('#div1').css('background', 'red')

//2. 选择所有的div元素
$('div').css('background', 'red')

//3. 选择所有class属性为box的元素
$('.box').css('background', 'red')

//4. 选择所有的div和span元素
$('div,span').css('background', 'red')

//5. 选择所有class属性为box的div元素
$('div.box').css('background', 'red')

//6. 选择HTML所有标签元素
$('*').css('background', 'red')
</script>
```

#### 6.层次选择器

##### 6.1 层次选择器: 查找子元素, 后代元素, 兄弟元素的选择器

1. ancestor descendant

  在给定的祖先元素下匹配所有的后代元素

2. parent>child

  在给定的父元素下匹配所有的子元素

3. prev+nexts

  匹配所有紧接在 prev 元素后的 next 元素

4. prev~siblings

  匹配 prev 元素之后的所有 siblings 元素

```javascript 
<script type="text/javascript">
//html结构
$('body').append('<ul></ul>')
$('ul').append('<li>AAAAA</li>')
$('ul').append('<li class="box">CCCCC</li>')
$('ul').append('<li title="hello"><span>BBBBB</span></li>')
$('ul').append('<li title="hello"><span class="box">DDDD</span></li>')
$('ul').append('<span>EEEEE</span>')

//1. 选中ul下所有的的span
$('ul span').css('background', 'yellow')

//2. 选中ul下所有的子元素span
$('ul>span').css('background', 'yellow')

//3. 选中class为box的下一个li
$('.box+li').css('background', 'yellow')

//4. 选中ul下的class为box的元素后面的所有兄弟元素
$('ul .box~*').css('background', 'yellow')
</script>
```

#### 7.过滤选择器

##### 7.1 在原有选择器匹配的元素中进一步进行过滤的选择器

\* 基本\* 内容\* 可见性\* 属性

```html
<div id="div1" class="box">class为box的div1</div>
<div id="div2" class="box">class为box的div2</div>
<div id="div3">div3</div>
<span class="box">class为box的span</span>
<br/>
<ul>
  <li>AAAAA</li>
  <li title="hello">BBBBB</li>
  <li class="box">CCCCC</li>
  <li title="hello">DDDDDD</li>
  <li title="two">BBBBB</li>
  <li style="display:none">我本来是隐藏的</li>
</ul>
```

```javascript
//1. 选择第一个div
$('div:first').css('background', 'red')

//2. 选择最后一个class为box的元素
$('.box:last').css('background', 'red')

//3. 选择所有class属性不为box的div
$('div:not(.box)').css('background', 'red')  //没有class属性也可以

//4. 选择第二个和第三个li元素
$('li:gt(0):lt(2)').css('background', 'red') 
// 多个过滤选择器不是同时执行, 而是依次
$('li:lt(3):gt(0)').css('background', 'red')

//5. 选择内容为BBBBB的li
$('li:contains("BBBBB")').css('background', 'red')

//6. 选择隐藏的li
console.log($('li:hidden').length, $('li:hidden')[0])

//7. 选择有title属性的li元素
$('li[title]').css('background', 'red')

//8. 选择所有属性title为hello的li元素
$('li[title="hello"]').css('background', 'red')
```

#### 8.表单选择器

##### 8.1 表单、表单对象属性

```javascript
$('body').append('<form></form>')
$('form').append('用户名: <input type="text" disabled="disabled"/><br>')
$('form').append('爱好：<input type="checkbox"/>篮球')
$('form').append('<input type="checkbox" checked="checked"/>足球')
$('form').append('<input type="checkbox" checked="checked"/>羽毛球')
$('form').append('<select></select>')
$('select').append('<option value="1">北京</option>')
$('select').append('<option value="2" selected="selected">天津</option>')
$('select').append('<option value="3">河北</option>')

//1. 选择不可用的文本输入框
$(':text:disabled').css('background', 'red')

//2. 显示选择爱好 的个数
console.log($(':checkbox:checked').length)

//3. 显示选择的城市名称
$(':submit').click(function () {
	var city = $('select>option:selected').html() // 选择的option的标签体文本
    city = $('select').val()  // 选择的option的value属性值
    alert(city)
  })
```

#### 9.$工具方法

##### 9.1常用工具方法

\* $.each(): 遍历数组或对象中的数据

\* $.trim(): 去除字符串两边的空格

\* $.type(obj): 得到数据的类型

\* $.isArray(obj): 判断是否是数组

\* $.isFunction(obj): 判断是否是函数

\* $.parseJSON(json) : 解析json字符串转换为js对象/数组

```javascript
//1. $.each(): 遍历数组或对象中的数据
var obj = {
	name: 'Tom',	
   	setName: function (name) {
      	this.name = name
    }
}
$.each(obj, function (key, value) {
    console.log(key, value)
})
  
//2. $.trim(): 去除字符串两边的空格
var str = '   text    '
console.log('---'+$.trim(str)+'---')

//3. $.type(obj): 得到数据的类型
console.log($.type($)) //'function'

//4. $.isArray(obj): 判断是否是数组
console.log($.isArray($('body')), $.isArray([])) //false true

//5. $.isFunction(obj): 判断是否是函数
console.log($.isFunction($)) //true

//6. $.parseJSON(json): 解析json字符串转换为js对象/数组
var json = '{"name":"Tom", "age":12}' //json对象: {}
// json对象===>JS对象
console.log($.parseJSON(json))
json = '[{"name":"Tom", "age":12}, {"name":"JACK", "age":13}]' //json数组: []
// json数组===>JS数组
console.log($.parseJSON(json))
/*
JSON.parse(jsonString)   json字符串--->js对象/数组
JSON.stringify(jsObj/jsArr)  js对象/数组--->json字符串
*/
```

#### 10.属性

##### 10.1 操作任意属性

\* attr()

\* removeAttr()	

\* prop()

##### 10.2 操作class属性

\* addClass()	

\* removeClass()

##### 10.3 操作HTML代码/文本/值

\* html()	

\* val()

```javascript
<script type="text/javascript">
//html结构
$('body').append('<div id="div1" class="box" title="one">class为box的div1</div>')
$('body').append('<div id="div2" class="box" title="two">class为box的div2</div>')
$('body').append('<div id="div3">div3</div>')
$('body').append('<span class="box">class为box的span</span><br/>')
$('body').append('<ul></ul>')
$('ul').append('<li>AAAAA</li>')
$('ul').append('<li title="hello" class="box2">BBBBB</li>')
$('ul').append('<li class="box">CCCCC</li>')
$('ul').append('<li title="hello">DDDDDD</li>')
$('ul').append('<li title="two"><span>BBBBB</span></li>')
$('body').append('<input type="text" name="username" value="guiguClass"/><br>')
$('body').append('<input type="checkbox"><input type="checkbox"><br>')
$('body').append('<button>选中</button> <button>不选中</button>')
    
//1. 读取第一个div的title属性
console.log($('div:first').attr('title')) //one

//2. 给所有的div设置name属性(value为atguigu)
$('div').attr('name', 'atguigu')

//3. 移除所有div的title属性
$('div').removeAttr('title')

//4. 给所有的div设置class='guiguClass'
$('div').attr('class', 'guiguClass')

//5. 给所有的div添加class='abc'
$('div').addClass('abc')

//6. 移除所有div的guiguClass的class
$('div').removeClass('guiguClass')

//7. 得到最后一个li的标签体文本
console.log($('li:last').html())

//8. 设置第一个li的标签体为"<h1>mmmmmmmmm</h1>"
$('li:first').html('<h1>mmmmmmmmm</h1>')

//9. 得到输入框中的value值
console.log($(':text').val()) //读取

//10. 将输入框的值设置为atguigu
$(':text').val('atguigu') //设置(读写合一)

//11. 点击按钮实现全选
var $checkboxs = $(':checkbox')
  	$('button:first').click(function () {
    $checkboxs.prop('checked', true)
})

//12. 点击按钮实现全不选
$('button:last').click(function () {
    $checkboxs.prop('checked', false)
})
// attr(): 操作属性值为非布尔值的属性
// prop(): 专门操作属性值为布尔值的属性
</script>
```

#### 总结：

##### 1.了解jQuery

###### 1.1 是什么: What?

- 一个JS函数库: write less, do more
- 封装简化DOM操作(CRUD) / Ajax

###### 1.2 为什么用它: why?

- 强大选择器: 方便快速查找DOM元素
- 隐式遍历(迭代): 一次操作多个元素
- 读写合一: 读数据/写数据用的是一个函数
- 链式调用: 可以通过.不断调用jQuery对象的方法
- 事件处理
- DOM操作(CUD)
- 样式操作
- 动画
- 浏览器兼容

###### 1.3 如何使用: How?

- 引入jQuery库
  - 本地引入与CDN远程引入
  - 测试版与生产版(压缩版)
- 使用jQuery
  - 使用jQuery函数: $/jQuery
  - 使用jQuery对象: $xxx(执行$()得到的)

##### 2.jQuery的2把利器

###### 2.1 jQuery函数: $/jQuery

- jQuery向外暴露的就是jQuery函数, 可以直接使用
- 当成一般函数使用人: $(param)
  - param是function: 相当于window.onload = function(文档加载完成的监听)
  - param是选择器字符串: 查找所有匹配的DOM元素, 返回包含所有DOM元素的jQuery对象
  - param是DOM元素: 将DOM元素对象包装为jQuery对象返回  $(this)
  - param是标签字符串: 创建标签DOM元素对象并包装为jQuery对象返回
- 当成对象使用: $.xxx
  - each(obj/arr, function(key, value){})
  - trim(str)

###### 2.2 jQuery对象

- 包含所有匹配的n个DOM元素的伪数组对象

- 执行$()返回的就是jQuery对象

- 基本行为:

  - length/size(): 得到dom元素的个数

  - [index]: 得到指定下标对应的dom元素

  - each(function(index, domEle){}): 遍历所有dom元素

  - index(): 得到当前dom元素在所有兄弟中的下标

##### 3.选择器

###### 3.1 是什么?

- 有特定语法规则(css选择器)的字符串
- 用来查找某个/些DOM元素: $(selector)

- 分类
  - 基本
    - #id
    - tagName/*
    - .class
    - selector1,selector2,selector3: 并集
    - selector1selector2selector3: 交集
  - 层次
    - 找子孙后代, 兄弟元素
    - selector1>selector2: 子元素
    - selector1 selector2: 后代元素
  - 过滤
    - 在原有匹配元素中筛选出其中一些
    - :first
    - :last
    - :eq(index)
    - :lt
    - :gt
    - :odd
    - :even
    - :not(selector)
    - :hidden
    - :visible
    - [attrName]
    - [attrName=value]
  - 表单
    - :input
    - :text
    - :checkbox
    - :radio
    - :checked: 选中的

##### 4.属性/文本

###### 4.1 是什么？

  - 操作标签的属性, 标签体文本

    - :attr(name) / attr(name, value): 读写非布尔值的标签属性

    - :prop(name) / prop(name, value): 读写布尔值的标签属性

    - :removeAttr(name)/removeProp(name): 删除属性

    - :addClass(classValue): 添加class

    - :removeClass(classValue): 移除指定class

    - :val() / val(value): 读写标签的value

    - :html() / html(htmlString): 读写标签体文本

#### 11.设置/读取css样式

##### 11.1 案例

```javascript
<script type="text/javascript">
//html结构
$('body').append('<p style="color: blue;">blue蓝色</p>')
$('body').append('<p style="color: green;">green绿色</p>')

//1. 得到第一个p标签的颜色
console.log($('p:first').css('color'))

//2. 设置所有p标签的文本颜色为red
$('p').css('color', 'red')

//3. 设置第2个p的字体颜色(#ff0011),背景(blue),宽(300px), 高(30px)
$('p:eq(1)').css({
    color: '#ff0011',
    background: 'blue',
    width: 300,
    height: 30
})
</script>
```

#### 12.offset和position

##### 12.1 案例

```javascript
<script type="text/javascript">
//html结构
$('body').append('<div class="div1"></div>')
$('.div1').append('<div class="div2">测试offset</div>')
$('body').append('<div class="div3"></div>')
$('.div3').append('<button id="btn1">读取offset和position</button> ')
$('.div3').append('<button id="btn2">设置offset</button>')

//css样式
$('body').css('margin', 0)
$('.div1').css({
    position: 'absolute',
    width: 200,
    height: 200,
    top: 20,
    left: 10,
    background: 'blue'
})
$('.div2').css({
  position: 'absolute',
  width: 100,
  height: 100,
  top: 50,
  background: 'red'
})
$('.div3').css({
  position: 'absolute',
  top: 250
})

//点击 btn1
$('#btn1').click(function () {
//打印 div1 相对于页面左上角的位置
var offset = $('.div1').offset()
console.log(offset.left, offset.top) // 10 20
    
//打印 div2 位置相对于页面左上角的
offset = $('.div2').offset()
console.log(offset.left, offset.top) // 10 70
    
//打印 div1 相对于父元素左上角的位置
var position = $('.div1').position()
console.log(position.left, position.top) // 10 20
    
//打印 div2 相对于父元素左上角的位置
position = $('.div2').position()
console.log(position.left, position.top) // 0 50
})

//点击 btn2
$('#btn2').click(function () {
    //设置 div2 相对于页面的左上角的位置
	$('.div2').offset({
      	left: 50,
      	top: 100
    })
})
</script>
```

#### 13.元素滚动

##### 13.1 案例

```javascript
<script type="text/javascript">
//html结构
$('body').append('<div></div>')
$('body').append('<br><br><br>')
$('body').append('<button id="btn1">得到scrollTop</button> ')
$('body').append('<button id="btn2">设置scrollTop</button>')

//css样式
$('div').css({
    border: '1px solid black',
    width: 100,
    height: 150,
    overflow: 'auto'
})

//1. 得到div或页面滚动条的坐标
$('#btn1').click(function () {
    console.log($('div').scrollTop())
	console.log($(document.documentElement).scrollTop()+$(document.body).scrollTop()) // 兼容IE/Chrome
})

//2. 让div或页面的滚动条滚动到指定位置
$('#btn2').click(function () {
    $('div').scrollTop(200)
    $('html,body').scrollTop(300)
})
</script>
```

#### 14.元素的尺寸

##### 14.1 内容尺寸

\* height(): height
\* width(): width

##### 14.2 内部尺寸

\* innerHeight(): height+padding
\* innerWidth(): width+padding

##### 14.3 外部尺寸

\* outerHeight(false/true): height+padding+border  如果是true, 加上margin
\* outerWidth(false/true): width+padding+border 如果是true, 加上margin

##### 14.4 案例

```javascript
<script type="text/javascript">
//html结构
$('body').append('<div>DIV</div>')

//css样式
$('div').css({
    width: 100,
    height: 150,
    background: 'red',
    padding: 10,
    border: '10px #fbd850 solid',
    margin: 10
})

// 1. 获取内容尺寸
var $div = $('div')
console.log($div.width(), $div.height())  // 100 150

// 2. 获取内部尺寸
console.log($div.innerWidth(), $div.innerHeight()) //120 170

// 3. 获取外部尺寸
console.log($div.outerWidth(), $div.outerHeight()) //140 190
console.log($div.outerWidth(true), $div.outerHeight(true)) //160 210
</script>
```

#### 15.筛选&过滤

##### 15.1 在jQuery对象中的元素对象数组中过滤出一部分元素来

\* first()

\* last()

\* eq(index|-index)

\* filter(selector)

\* not(selector)

\* has(selector)

##### 15.2 案例

```javascript
<script type="text/javascript">
//html结构
$('body').append('<ul></ul>')
$('ul').append('<li>AAA</li>')
$('ul').append('<li title="hello" class="box2">BBB</li>')
$('ul').append('<li class="box">CCC</li>')
$('ul').append('<li title="hello">DDD</li>')
$('ul').append('<li title="two"><span>BBB</span></li>')
$('body').append('<li>eee</li>')
$('body').append('<li>EEE</li>')

var $lis = $('ul>li')
//1. ul下li标签第一个
$lis.first().css('background', 'red')
$lis[0].style.background = 'red' //原生js

//2. ul下li标签的最后一个
$lis.last().css('background', 'red')

//3. ul下li标签的第二个
$lis.eq(1).css('background', 'red')

//4. ul下li标签中title属性为hello的
$lis.filter('[title=hello]').css('background', 'red')

//5. ul下li标签中title属性不为hello的
$lis.not('[title=hello]').css('background', 'red')
$lis.filter('[title!=hello]').filter('[title]').css('background', 'red')

//6. ul下li标签中有span子标签的
$lis.has('span').css('background', 'red')
</script>
```

#### 16.筛选&查找(孩子-父母-兄弟标签)

##### 16.1 在已经匹配出的元素集合中根据选择器查找孩子/父母/兄弟标签

\* children(): 子标签中找

\* find() : 后代标签中找

\* parent() : 父标签

\* prevAll() : 前面所有的兄弟标签

\* nextAll() : 后面所有的兄弟标签

\* siblings() : 前后所有的兄弟标签 

##### 16.2 案例

```javascript
<script type="text/javascript">
//html结构
$('body').append('<span>span文本5</span>')
$('body').append('<div></div>')
$('div').append('<ul></ul>')
$('ul').append('<span>span文本1</span>')
$('ul').append('<li>AAA</li>')
$('ul').append('<li title="hello" class="box2">BBB</li>')
$('ul').append('<li class="box" id="cc">CCC</li>')
$('ul').append('<li title="hello">DDD</li>')
$('ul').append('<li title="two"><span>span文本2</span></li>')
$('ul').append('<span>span文本3</span>')
$('div').append('<span>span文本4</span>')

var $ul = $('ul')
//1. ul标签的第2个span子标签
$ul.children('span:eq(1)').css('background', 'red')

//2. ul标签的第2个span后代标签
$ul.find('span:eq(1)').css('background', 'red')

//3. ul标签的父标签
$ul.parent().css('background', 'red')

//4. id为cc的li标签的前面的所有li标签
$ul.children('#cc').prevAll('li').css('background', 'red')

//5. id为cc的li标签的所有兄弟li标签
$ul.children('#cc').siblings('li').css('background', 'red')
</script>
```

#### 17.文档增删改

##### 17.1 添加/替换元素

\* append(content)

​	向当前匹配的所有元素内部的最后插入指定内容

\* prepend(content)

​	向当前匹配的所有元素内部的最前面插入指定内容

\* before(content)

​	将指定内容插入到当前所有匹配元素的前面

\* after(content)

​	将指定内容插入到当前所有匹配元素的后面替换节点

\* replaceWith(content)

​	用指定内容替换所有匹配的标签删除节点

##### 17.2 删除元素

\* empty()

​	删除所有匹配元素的子元素

\* remove()

​	删除所有匹配的元素

##### 17.3 案例

```javascript
<script type="text/javascript">
//html结构
$('body').append('<ul id="ul1"></ul>')
$('#ul1').append('<li>AAAAA</li>')
$('#ul1').append('<li title="hello">BBBBB</li>')
$('#ul1').append('<li class="box">CCCCC</li>')
$('#ul1').append('<li title="hello">DDDDDD</li>')
$('#ul1').append('<li title="two">EEEEE</li>')
$('#ul1').append('<li>FFFFF</li>')
$('body').append('<ul id="ul2"></ul>')
$('#ul2').append('<li>aaa</li>')
$('#ul2').append('<li title="hello">bbb</li>')
$('#ul2').append('<li class="box">ccc</li>')
$('#ul2').append('<li title="hello">ddd</li>')
$('#ul2').append('<li title="two">eee</li>')

//1. 向id为ul1的ul下添加一个span(最后)
var $ul1 = $('#ul1')
$ul1.append('<span>append()添加的span</span>')
$('<span>appendTo()添加的span</span>').appendTo($ul1)

//2. 向id为ul1的ul下添加一个span(最前)
$ul1.prepend('<span>prepend()添加的span</span>')
$('<span>prependTo()添加的span</span>').prependTo($ul1)

//3. 在id为ul1的ul下的li(title为hello)的前面添加span
$ul1.children('li[title=hello]').before('<span>before()添加的span</span>')

//4. 在id为ul1的ul下的li(title为hello)的后面添加span
$ul1.children('li[title=hello]').after('<span>after()添加的span</span>')

//5. 将在id为ul2的ul下的li(title为hello)全部替换为p
$('#ul2>li[title=hello]').replaceWith('<p>replaceAll()替换的p</p>')

//6. 移除id为ul2的ul下的所有li
$('#ul2').empty() //<p>也会删除
$('#ul2>li').remove()
</script>
```

#### 18.事件绑定与解绑

##### 18.1 事件绑定(2种)：

\* eventName(function(){})

​	绑定对应事件名的监听, 例如：$('#div').click(function(){});

\* on(eventName, funcion(){})

​	通用的绑定事件监听, 例如：$('#div').on('click', function(){})

\* 优缺点:

​	eventName: 编码方便, 但只能加一个监听, 且有的事件监听不支持

​	on: 编码不方便, 可以添加多个监听, 且更通用

##### 18.2 事件解绑：

\* off(eventName)

##### 18.3 事件的坐标

\* event.clientX, event.clientY  相对于视口的左上角

\* event.pageX, event.pageY  相对于页面的左上角

\* event.offsetX, event.offsetY 相对于事件元素左上角

##### 18.4 事件相关处理

\* 停止事件冒泡 : event.stopPropagation()

\* 阻止事件默认行为 : event.preventDefault()

##### 18.5 案例

```javascript
<script type="text/javascript">
//html结构
$('body').append('<div class="out">外部DIV</div>')
$('.out').append('<div class="inner">内部div</div>')
$('body').append('<div class="divBtn"></div>')
$('.divBtn').append('<button id="btn1">取消绑定所有事件</button>')
$('.divBtn').append('<button id="btn2">取消绑定mouseover事件</button>')
$('.divBtn').append('<button id="btn3">测试事件坐标</button>')
$('.divBtn').append('<a href="http://www.baidu.com" id="test4">百度一下</a>')

//css样式
$('*').css('argin', '0')
$('.out').css({
    position: 'absolute',
    width: 200,
    height: 200,
    top: 20,
    left: 10,
    background: 'blue'
})
$('.inner').css({
    position: 'absolute',
    width: 100,
    height: 100,
    top: 50,
    background: 'red'
})
$('.divBtn').css({
    position: 'absolute',
    top: 250
})

//1. 给.out绑定点击监听(用两种方法绑定)
$('.out').click(function () {
   console.log('click out')
})

$('.out').on('click', function () {
    console.log('on click out')
})

//2. 给.inner绑定鼠标移入和移出的事件监听(用3种方法绑定)
$('.inner')
	.mouseenter(function () { // 进入
	console.log('进入')
})
.mouseleave(function () { // 离开
	console.log('离开')
})
  
$('.inner')
	.on('mouseenter', function () {
	console.log('进入2')
})
	.on('mouseleave', function () {
	console.log('离开2')
})
  
$('.inner').hover(function () {
	console.log('进入3')
}, function () {
    console.log('离开3')
})

//3. 点击btn1解除.inner上的所有事件监听
$('#btn1').click(function () {
    $('.inner').off()
})

//4. 点击btn2解除.inner上的mouseenter事件
$('#btn2').click(function () {
    $('.inner').off('mouseenter')
})

//5. 点击btn3得到事件坐标
$('#btn3').click(function (event) { // event事件对象
    console.log(event.offsetX, event.offsetY) // 原点为事件元素的左上角
    console.log(event.clientX, event.clientY) // 原点为窗口的左上角
    console.log(event.pageX, event.pageY) // 原点为页面的左上角
})

//6. 点击.inner区域, 外部点击监听不响应
$('.inner').click(function (event) {
    console.log('click inner')
    //停止事件冒泡
    event.stopPropagation()
})
  
//7. 点击链接, 如果当前时间是偶数不跳转
$('#test4').click(function (event) {
    if(Date.now()%2===0) {
      event.preventDefault()
    }
})
</script>
```

#### 19.事件mouseover与mouseenter

##### 19.1 区别mouseover与mouseenter?

\* mouseover(): 在移入子元素时也会触发, 对应mouseout

\* mouseenter(): 只在移入当前元素时才触发, 对应mouseleave

\* hover(): 使用的就是mouseenter()和mouseleave()

##### 19.2 区别on('eventName', fun)与eventName(fun)

\* on('eventName', fun): 通用, 但编码麻烦

\* eventName(fun): 编码简单, 但有的事件没有对应的方法

##### 19.3 案例

```javascript
<script type="text/javascript">
//html结构
$('body').append('<div class="divText">区分鼠标的事件</div>')
$('body').append('<div class="div1">div1......</div>')
$('.div1').append('<div class="div2">div2......</div>')
$('body').append('<div class="div3">div3.....</div>')
$('.div3').append('<div class="div4">div4.....</div>')

//css样式
$('*').css('margin', '0')
$('.div1').css({
    position: 'absolute',
    width: 200,
    height: 200,
    top: 50,
    left: 10,
    background: 'olive'
})
$('.div2').css({
    position: 'absolute',
    width: 100,
    height: 100,
    top: 50,
    background: 'red'
})
$('.div3').css({
    position: 'absolute',
    width: 200,
    height: 200,
    top: 50,
    left: 230,
    background: 'olive'
})
$('.div4').css({
    position: 'absolute',
    width: 100,
    height: 100,
    top: 50,
    background: 'yellow'
})
$('.divText').css({
    position: 'absolute',
    top: 330,
    left: 10
})
//区别测试
$('.div1')
	.mouseover(function () {
		console.log('mouseover 进入')
	})
	.mouseout(function () {
		console.log('mouseout 离开')
	})

$('.div3')
	.mouseenter(function () {
		console.log('mouseenter 进入')
	})
	.mouseleave(function () {
		console.log('mouseleave 离开')
	})
</script>
```

#### 20.事件委托

##### 20.1 绑定事件监听的问题: 新加的元素没有监听

```javascript
<script type="text/javascript">
//html结构
$('body').append('<ul></ul>')
$('ul').append('<li>1111</li>')
$('ul').append('<li>2222</li>')
$('ul').append('<li>3333</li>')
$('body').append('<button id="btn1">添加新的li</button>')

//1.点击 li 背景就会变为红色
$('ul>li').click(function () {
	this.style.background = 'red'
})
//2.点击 btn 就添加一个 li
$('#btn').click(function () {
    $('ul').append('<li>新增的li....</li>')
})
</script>
```

##### 20.2 事件委托(委派/代理):

\* 将多个子元素(li)的事件监听委托给父辈元素(ul)处理

\*监听回调是加在了父辈元素上

\*当操作任何一个子元素(li)时, 事件会冒泡到父辈元素(ul)

\*父辈元素不会直接处理事件, 而是根据event.target得到发生事件的子元素(li), 通过这个子元素调用事件回调函数

##### 20.3 事件委托的2方:

\*委托方: 业主  li

\*被委托方: 中介  ul

##### 20.4 使用事件委托的好处

\*添加新的子元素, 自动有事件响应处理

\*减少事件监听的数量: n==>1

##### 20.5 jQuery的事件委托API

\*设置事件委托: $(parentSelector).delegate(childrenSelector, eventName, callback)

\*移除事件委托: $(parentSelector).undelegate(eventName)

##### 20.6 案例

```javascript
<script type="text/javascript">
//html结构
$('body').append('<ul></ul>')
$('ul').append('<li>1111</li>')
$('ul').append('<li>2222</li>')
$('ul').append('<li>3333</li>')
$('body').append('<button id="btn1">添加新的li</button>')
$('body').append('<button id="btn2">删除ul上的事件委托的监听器</button>')

$(function () {
    //事件委托
    $('ul').delegate('li', 'click', function () {
      this.style.background = 'red'
    })

    $('#btn1').click(function () {
      $('ul').append('<li>xxxxxxxxx</li>')
    })

    $('#btn2').click(function () {
      // 移除事件委托
      $('ul').undelegate()
    })
  })
</scrpit>
```

#### 总结：

##### 1.CSS模块

- ###### style样式

  - css(styleName): 根据样式名得到对应的值
  - css(styleName, value): 设置一个样式
  - css({多个样式对}): 设置多个样式

- ###### 位置坐标

  - offset(): 读/写当前元素坐标(原点是页面左上角)
  - position(): 读当前元素坐标(原点是父元素左上角)
  - scrollTop()/scrollLeft(): 读/写元素/页面的滚动条坐标

- ###### 尺寸

  - width()/height(): width/height
  - innerWidth()/innerHeight(): width + padding
  - outerWidth()/outerHeight(): width + padding + border

##### 2.筛选模块

- ###### 过滤

  - 在jQuery对象内部的元素中找出部分匹配的元素, 并封装成新的jQuery对象返回
  - first()
  - last()
  - eq(index)
  - filter(selector): 对当前元素提要求
  - not(selector): 对当前元素提要求, 并取反
  - has(selector): 对子孙元素提要求

- ###### 查找

  - 查找jQuery对象内部的元素的子孙/兄弟/父母元素, 并封装成新的jQuery对象返回
  - children(selector): 子元素
  - find(selector): 后代元素
  - preAll(selector): 前的所有兄弟
  - siblings(selector): 所有兄弟
  - parent(): 父元素

##### 3.文档处理(CUD)模块

- ###### 增加

  - append() / appendTo(): 插入后部
  - preppend() / preppendTo(): 插入前部
  - before(): 插到前面
  - after(): 插到后面

- ###### 删除

  - remove(): 将自己及内部的孩子都删除
  - empty(): 掏空(自己还在)

- ###### 更新

  - replaceWith()

##### 4.事件模块

- ###### 绑定事件

  - eventName(function(){})
  - on('eventName', function(){})
  - 常用: click, mouseenter/mouseleave mouseover/mouseout focus/blur
  - hover(function(){}, function(){})

- ###### 解绑事件

  - off('eventName')

- ###### 事件委托

  - 理解: 将子元素的事件委托给父辈元素处理
    - 事件监听绑定在父元素上, 但事件发生在子元素上
    - 事件会冒泡到父元素
    - 但最终调用的事件回调函数的是子元素: event.target
  - 好处
    - 新增的元素没有事件监听
    - 减少监听的数量(n==>1)
  - 编码
    - delegate(selector, 'eventName', function(event){}) // 回调函数中的this是子元素
    - undelegate('eventName')

- ###### 事件坐标

  - event.offsetX: 原点是当前元素左上角
  - event.clientX: 原点是窗口左上角
  - event.pageX: 原点是页面左上角

- ###### 事件相关

  - 停止事件冒泡: event.stopPropagation()
  - 阻止事件的默认行为: event.preventDefault()

#### 21.动画淡入淡出

##### 21.1 淡入淡出: 不断改变元素的透明度来实现的

\* fadeIn(): 带动画的显示

\* fadeOut(): 带动画隐藏

\* fadeToggle(): 带动画切换显示/隐藏

##### 21.2 案例

```javascript
//html结构
$('body').append('<button id="btn1">慢慢淡出</button>')
$('body').append('<button id="btn2">慢慢淡入</button>')
$('body').append('<button id="btn3">淡出/淡入切换</button>')
$('body').append('<div class="div1"></div>')

//css样式
$('*').css('margin', 0)
$('.div1').css({
    position: 'absolute',
    width: 200,
    height: 200,
    top: 50,
    left: 10,
    background: 'red'
})

var $div1 = $('.div1')
/*1. 点击btn1, 慢慢淡出
* 无参 $('.div1').fadeOut()
* 有参 $('.div1').fadeOut(1000)
	* 字符串参数
	* 数字参数
*/
$('#btn1').click(function () {
    $div1.fadeOut(1000, function () {
    })
})
//2. 点击btn3, 慢慢淡入
$('#btn2').click(function () {
    $div1.fadeIn()
})
//3. 点击btn3, 淡出/淡入切换
$('#btn3').click(function () {
    $div1.fadeToggle()
})
```

#### 22.动画滑动

##### 22.1 滑动动画: 不断改变元素的高度实现

\* slideDown(): 带动画的展开

\* slideUp(): 带动画的收缩

\* slideToggle(): 带动画的切换展开/收缩

##### 22.2 案例

```javascript
<script type="text/javascript">
//html结构
$('body').append('<button id="btn1">慢慢收缩</button>')
$('body').append('<button id="btn2">慢慢展开</button>')
$('body').append('<button id="btn3">收缩/展开切换</button>')
$('body').append('<div class="div1"></div>')

//css样式
$('*').css('margin', 0)
$('.div1').css({
    position: 'absolute',
    width: 200,
    height: 200,
    top: 50,
    left: 10,
    background: 'red'
})

var $div1 = $('.div1')
// 1. 点击btn1, 向上滑动
$('#btn1').click(function () {
    $div1.slideUp(3000)
})
// 2. 点击btn2, 向下滑动
$('#btn2').click(function () {
    $div1.slideDown()
})
// 3. 点击btn3, 向上/向下切换
$('#btn3').click(function () {
    $div1.slideToggle()
})
</script>
```

#### 23.动画显示与隐藏

##### 23.1 显示隐藏，默认没有动画, 动画(opacity/height/width)

\* show(): (不)带动画的显示

\* hide(): (不)带动画的隐藏

\* toggle(): (不)带动画的切换显示/隐藏

##### 23.2 案例

```javascript
<script type="text/javascript">
//html结构
$('body').append('<button id="btn1">瞬间显示</button>')
$('body').append('<button id="btn2">慢慢显示</button>')
$('body').append('<button id="btn3">慢慢隐藏</button>')
$('body').append('<button id="btn4">显示隐藏切换</button>')
$('body').append('<div class="div1"></div>')

//css样式
$('*').css('margin', 0)
$('.div1').css({
    position: 'absolute',
    width: 200,
    height: 200,
    top: 50,
    left: 10,
    background: 'red',
    display: 'none'
})
var $div1 = $('.div1')
//1. 点击btn1, 立即显示
$('#btn1').click(function () {
    $div1.show()
})
//2. 点击btn2, 慢慢显示
$('#btn2').click(function () {
    $div1.show(1000)
})
//3. 点击btn3, 慢慢隐藏
$('#btn3').click(function () {
    $div1.hide(1000)
})
//4. 点击btn4, 切换显示/隐藏
$('#btn4').click(function () {
    $div1.toggle(1000)
})
</script>
```

#### 24.自定义动画

##### 24.1 jQuery动画本质 : 在指定时间内不断改变元素样式值来实现的

\* animate(): 自定义动画效果的动画

\* stop(): 停止动画

##### 24.2 案例

```javascript
<script type="text/javascript">
//html结构
$('body').append('<button id="btn1">逐渐扩大</button>')
$('body').append('<button id="btn2">移动到指定位置</button>')
$('body').append('<button id="btn3">移动指定距离</button>')
$('body').append('<button id="btn4">停止动画</button>')
$('body').append('<div class="div1">测试自定义动画</div>')

//css样式
$('*').css('margin', 0)
$('.div1').css({
    position: 'absolute',
    width: 100,
    height: 100,
    top: 50,
    left: 300,
    background: 'red'
})
//1. 逐渐扩大
$('#btn1').click(function () {
	//1). 宽/高都扩为200px
    $div1.animate({
		width: 200,
    	height: 200
	}, 1000)
    //2). 宽先扩为200px, 高后扩为200px
	$div1
		.animate({
        	width: 200
    	}, 1000)
    	.animate({
    		height: 200
    	}, 1000)
})
//2. 移动到指定位置
$('#btn2').click(function () {
    // 1).移动到(500, 100)处
    $div1.animate({ // 向右下移动
    	left: 500,
        top: 100
    }, 1000)
    // 2).移动到(100, 20)处
    $div1.animate({ // 向左上移动
        left: 100,  // 300
        top: 20  // 50
    }, 1000)
  })
//3.移动指定的距离
$('#btn3').click(function () {
    // 1). 移动距离为(100, 50)
    $div1.animate({
    	left: '+=100',
        top: '+=50'
    }, 1000)
    // 2). 移动距离为(-100, -20)
    $div1.animate({
      left: '-=100',
      top: '-=20'
    }, 3000)
})
//4. 停止动画(如果多个动画，需要点n次才可以停止动画)
$('#btn4').click(function () {
	$div1.stop()
})
</script>
```

#### 25.扩展插件

##### 25.1 扩展jQuery的工具方法

 	\* $.extend(object)

##### 25.2 扩展jQuery对象的方法

 	\* $.fn.extend(object)

##### 25.3 案例

```javascript
<script src="js/jquery-1.10.1.js"></script>
<script src="js/my_jQuery-plugin.js" type="text/javascript"></script>

<script type="text/javascript">
//html结构
$('body').append('<input type="checkbox" name="items" value="足球"/>足球')
$('body').append('<input type="checkbox" name="items" value="篮球"/>篮球')
$('body').append('<input type="checkbox" name="items" value="羽毛球"/>羽毛球')
$('body').append('<input type="checkbox" name="items" value="乒乓球"/>乒乓球<br/>')
$('body').append('<input type="button" id="checkedAllBtn" value="全　选"/>')
$('body').append('<input type="button" id="checkedNoBtn" value="全不选"/>')
$('body').append('<input type="button" id="reverseCheckedBtn" value="反选"/>')

/* 扩展$的方法
	1. 给 $ 添加4个工具方法:
	* min(a, b) : 返回较小的值
   	* max(c, d) : 返回较大的值
   	* leftTrim() : 去掉字符串左边的空格
   	* rightTrim() : 去掉字符串右边的空格
*/
(function () {
	$.extend({
        min: function (a, b) {
          return a < b ? a : b
        },
        max: function (a, b) {
          return a > b ? a : b
        },
        leftTrim: function (str) {
          return str.replace(/^\s+/, '')
        },
        rightTrim: function (str) {
          return str.replace(/\s+$/, '')
        }
  	})
/* 扩展jQuery对象的方法
	2.给jQuery对象 添加3个功能方法:
 	* checkAll() : 全选
 	* unCheckAll() : 全不选
 	* reverseCheck() : 全反选
*/
  	$.fn.extend({
        checkAll: function () {
          this.prop('checked', true) // this是jQuery对象
        },
        unCheckAll: function () {
          this.prop('checked', false)
        },
        reverseCheck: function () {
          // this是jQuery对象
          this.each(function () {
            // this是dom元素
            this.checked = !this.checked
          })
    	}
  	})

})()
```

```javascript
console.log($.min(3, 5), $.max(3, 5))
var string = '   my atguigu    '
console.log('-----' + $.leftTrim(string) + '-----')
console.log('-----' + $.rightTrim(string) + '-----')

var $items = $(':checkbox[name=items]')
$('#checkedAllBtn').click(function () {
    $items.checkAll()
})
$('#checkedNoBtn').click(function () {
    $items.unCheckAll()
})
$('#reverseCheckedBtn').click(function () {
    $items.reverseCheck()
})
```

#### 26.多库共存

##### 26.1 问题 : 如果有2个库都有$, 就存在冲突

​	解决 : jQuery库可以释放$的使用权, 让另一个库可以正常使用, 此时jQuery库只能使用jQuery了

​	API : jQuery.noConflict()

```javascript
<script type="text/javascript" src="js/myLib.js"></script>
<script type="text/javascript" src="js/jquery-1.10.1.js"></script>
// 释放$的使用权
jQuery.noConflict()
// 调用myLib中的$
$()
// 要想使用jQuery的功能, 只能使用jQuery
jQuery(function () {
	console.log('文档加载完成')
})
console.log('+++++')
```

```javascript
//myLib.js文件
(function () {
	window.$ = function () {
    	console.log('my lib $()...')
  	}
})()
```

#### 27.ready和onload区别

##### 27.1 区别: window.onload与 $(document).ready()

\* window.onload

​	*包括页面的图片加载完后才会回调(晚)

​	\* 只能有一个监听回调

\* $(document).ready()

​	\* 等同于: $(function(){})

​	*页面加载完就回调(早)

​	\* 可以有多个监听回调

##### 27.2 案例

```html
<h1>测试window.onload与$(document).ready()</h1>
<img id="logo" src="https://gss0.bdstatic.com/5bVWsj_p_tVS5dKfpU_Y_D3/res/r/image/2017-05-19/6fec71d56242b74eb24b4ac80b817eac.png">
```

```javascript
//1. 直接打印img的宽度，观察其值
console.log('直接', $('#logo').width())
//2. 在 $(function(){}) 中 打印 img 的宽度 
$(function () {
    console.log('ready', $('#logo').width())
})
$(function () {
    console.log('ready2', $('#logo').width())
})
//3. 在 window.onload 中打印宽度  
window.onload = function () {
	console.log('onload', $('#logo').width())
}
window.onload = function () {
    console.log('onload2', $('#logo').width())
}
//4. 在 img 加载完成后打印宽度  
$('#logo').on('load', function () {
    console.log('img load', $(this).width())
})
```

#### 总结：

##### 1.动画效果

- 在一定的时间内, 不断改变元素样式
- slideDown()/slideUp()/slideToggle()
- fadeOut()/fadeIn()/fadeToggle()
- show()/hide()/toggle()
- animate({结束时的样式}, time, fun)
- stop()

##### 2.插件机制

- 扩展jQuery函数对象的方法
  $.extend({
    xxx: fuction () {} // this是$
  })
  $.xxx()
- 扩展jQuery对象的方法
  $.fn.extend({
    xxx: function(){}  // this是jQuery对象
  })
  $obj.xxx()

##### 3.jQuery文档的结构图


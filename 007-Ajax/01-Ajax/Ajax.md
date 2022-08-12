# Ajax学习笔记

## 前端相关的技术点：

- html（html5） 主要用来实现页面的排版布局
- css（css3） 主要用来实现页面的样式美化
- JavaScript（jQuery） 主要用来实现前端功能特效

> 采用上面的这些技术开发的页面和前端特效脚本需要放到服务器才能够对外提供服务，才能够让互联网上的网友看到。

## 客户端与服务器

> 本质上都是计算机，只不过样子不同，配置不同，应用场景不同（安装的应用软件不同）

- 客户端主要用于普通上网用户
- 服务器主要给上网用户提供后台服务

## 网络相关概念

- IP地址（唯一的确定互联网上的一台计算机）
- 域名 IP地址的别名，方便记忆
- DNS 用于维护IP地址与域名的关系
- 端口 用来确定计算机上的网络应用程序

## 通信协议理解

> 通信双方约定的规则

- http/https 超为本传输协议
- ftp 文件传输协议
- smpt/pop3 邮件收发协议
- ......

## 搭建服务器环境

### wamp集成环境介绍

- windows 操作系统
- Apache 提供静态资源服务（html页面、js文件、css文件、图片。。。）
- MySQL 数据库
- php 编程语言，可以用来开发网站

### wamp的安装配置

- 参见详细文档

## 网站

> 网站由一系列页面组成（页面由js、css、图片、html标签。。。所有的这些文件都被称为资源）

### 静态网站

> 就是提前写好的html页面（包括图片、媒体文件。。。静态资源文件），并且部署到服务器上
> <br>静态网站主要存在的问题：

- 随着网站规模的增大可维护性逐渐降低
- 没有交互性

### 动态网站

> 动态指的是html页面是动态生成的，这里动态生成的不一定是一个完整的页面，有可能仅仅是页面的一部分，或者仅仅是数据(普通字符串、json、xml)
> 实现动态网站的技术：

- php
- java（jsp）
- .net
- Node.js
- python
- ......

## apache安装配置

### 安装

> 安装路径D:\wamp

### 配置根路径

> 默认的网站根路径是安装目录的www子目录（D:\wamp\www），如果不想使用默认目录，可以自己配置。配置方式如下：

- 找到文件D:\wamp\bin\apache\Apache2.4.4\conf\httpd.conf 或者打开如下文件（实际是同一个文件）

   ![](C:\资料备份\学习笔记\01-Web笔记\007-Ajax\01-Ajax\media\2.png)

- 在文件中搜索DocumentRoot，找到239行位置

- 修改根路径为如下形式：(如果要配置虚拟主机，这里配置成根路径；如果不配置根路径，可以配置成D:\ajax；现在配置的是虚拟主机形式；两个位置应该保持一致)

   ![](C:\资料备份\学习笔记\01-Web笔记\007-Ajax\01-Ajax\media\1.png)

### 配置虚拟主机

> 配置虚拟主机可以配置多个网站（域名和网站目录对应），配置步骤如下

- 开启虚拟主机辅配置，在httpd.conf 中找到如下位置,然后把前面的井号去掉

   ![](C:\资料备份\学习笔记\01-Web笔记\007-Ajax\01-Ajax\media\3.png)

- 配置虚拟主机，打开conf/extra/httpd-vhosts.conf

   ![](C:\资料备份\学习笔记\01-Web笔记\007-Ajax\01-Ajax\media\4.png)

  分别修改以下三项，其它项无需指定。

  - DocumentRoot "E:/www/example"
  - ServerName "example.com "
  - ServerAlias "www.example.com"

- 修改DNS（hosts）文件(C:\Windows\System32\drivers\etc\hosts),
  添加如下内容：<br>
  127.0.0.1  example.com  <br>
  127.0.0.1  www.example.com

- 重启apache

- 访问http://www.example.com或者http://example.com

### 配置多个虚拟主机的实例如下：

- httpd-vhosts.conf文件配置

   ![](C:\资料备份\学习笔记\01-Web笔记\007-Ajax\01-Ajax\media\5.png)

- hosts文件配置

   ![](C:\资料备份\学习笔记\01-Web笔记\007-Ajax\01-Ajax\media\6.png)

## AJAX课程

#### 1.1 AJAX-简介

​	AJAX 全称为 Asynchronous JavaScript And XML，就是异步的 JS 和XML。通过 AJAX 可以在浏览器中向服务器发送异步请求，*最大的优势：无刷新获取数据*。

​	AJAX 不是新的编程语言，而是一种将现有的标准组合在一起使用的新方式。

​	AJAX 是一种用于创建快速动态网页的技术。

​	AJAX 通过在后台与服务器进行少量数据交换，使网页实现异步更新。这意味着可以在不重载整个页面的情况下，对网页的某些部分进行更新。

>传统的网页（不使用 AJAX）如果需要更新内容，必须重载整个页面

 ![](C:\资料备份\学习笔记\01-Web笔记\007-Ajax\01-Ajax\media\2022-07-21_103128.png)

**AJAX 基于因特网标准，并使用以下技术组合：**

- XMLHttpRequest 对象（与服务器异步交互数据）
- JavaScript/DOM（显示/取回信息）
- CSS（设置数据的样式）
- XML（常用作数据传输的格式）

![lamp](https://www.runoob.com/images/lamp.gif) AJAX 应用程序与浏览器和平台无关的！

#### 1.2 AJAX-XML的介绍

​	XML 可扩展标记语言。

​	XML 被设计用来传输和存储数据。

​	XML 和 HTML 类似，不同的是 HTML 中都是预定义标签，而 XML 中没有预定义标签，全都是自定义标签，用来表示一些数据。

```xml
比如说我有一个学生数据：
	name = "孙悟空" ; age = 18 ; gender = "男" ;
用 XML 表示：
    <student>
        <name>孙悟空</name>
        <age>18</age>
        <gender>男</gender>
    </student>
现在已经被 JSON 取代了。
用 JSON 表示：
	{"name":"孙悟空","age":18,"gender":"男"}
```

#### 1.3 AJAX-优缺点

##### 	1.3.1 AJAX的优点

​	1)可以无需刷新页面而与服务器端进行通信。

​	2)允许你根据用户事件来更新部分页面内容。

##### 	1.3.2 AJAX的缺点

​	1)没有浏览历史，不能回退 

​	2)存在跨域问题(同源) 

​	3)SEO不友好

#### 1.4 AJAX-HTTP协议请求报文与响应报文

​	HTTP（hypertext transport protocol）协议『超文本传输协议』，协议详细规定了浏览器和万维网服务器之间互相通信的规则。（约定, 规则）

##### 1.4.1 请求报文

重点是格式与参数

```
请求 行      Get、POST  /s?ie=utf-8  HTTP/1.1 
请求 头      Host: atguigu.com   （格式->名字：值）
            Cookie: name=guigu
            Content-type: application/x-www-form-urlencoded
            User-Agent: chrome 83
空行（必须有）
请求 体      username=admin&password=admin （get请求体为空 post请求体可以不为空）
```

##### 1.4.2 响应报文

```
响应 行      HTTP/1.1  200  OK
响应 头      Content-Type: text/html;charset=utf-8
        	Content-length: 2048
        	Content-encoding: gzip
空行（必须有）    
响应 体      <html>
                <head></head>
                <body>
                    <h1>test</h1>
                </body>
        	</html>
```

- 404 （找不到）
- 403 （禁止）
- 401 （未授权）
- 500 （内部错误）
- 200

#### 1.5 AJAX-Chrome网络控制台查看



#### 1.6 AJAX-Node.js安装与介绍

​	Node.js 是一个基于Chrome V8 引擎的JavaScript运行时。其实就是一个应用程序，可以解析js

代码，通过js可以对系统资源进行操作。（安装方式非常简单）

运行：打开window命令窗口--->node -v查看当前安装Node.js版本

#### 1.7 AJAX-express框架介绍和基本使用

​	基于Node.js 平台，快速、开放、极简的Web开发框架

##### 1.7.1 vsCode编辑器：打开全局控制台---> npm项目初始化操作 使用命令npm init

##### 1.7.2 基本使用：

```javascript
//1. 引入express
const express = require('express');

//2. 创建应用对象
const app = express();

//3. 创建路由规则
// request 是对请求报文的封装
// response 是对响应报文的封装
app.get('/', (request, response)=>{
    //设置响应头 设置允许跨域
    response.setHeader('Access-Control-Allow-Origin','*');
    
    //设置响应
    response.send('HELLO express');
});

//4. 监听端口启动服务
app.listen(8000, ()=>{
    console.log("服务已经启动, 8000 端口监听中....");
});
```

##### 1.7.3 项目文件夹--->打开控制台输入--->node + 文件名.js 启动服务--->打开Chorm地址栏输入127.0.0.1:8000

#### 1.8 AJAX-案例准备

##### 1.8.1 AJAX的使用

######  1）核心对象

​	XMLHttpRequest，AJAX 的所有操作都是通过该对象进行的。

######  2）使用步骤

```js
//XMLHttpRequest 用于在后台与服务器交换数据。这意味着可以在不重新加载整个网页的情况下，对网页的某部分进行更新。所有现代浏览器均支持 XMLHttpRequest 对象（IE5 和 IE6 使用 ActiveXObject）
1) 创建 XMLHttpRequest 对象
	var xhr = new XMLHttpRequest();//初始化 HTTP 请求参数
//如需将请求发送到服务器，我们使用 XMLHttpRequest 对象的 open() 和 send() 方法
2) 设置请求信息
	xhr.open(method, url);//可以设置请求头，一般不设置
	/*method参数是用于请求的 HTTP 方法。值包括 GET、POST 和 HEAD。
	(大小写不敏感。
		POST：用"POST"方式发送数据,可以大到4MB
		GET：用"GET"方式发送数据,只能256KB
		如果请求带有参数的化实用POST方式，POST方式将参数放置在页面的隐藏控件内
		没有参数使用GET方式
		对于请求的页面在中途可能发生更改的，也最好用POST方式)*/
	xhr.setRequestHeader('Content-Type', 'application/x-www-form-urlencoded');
3) 发送请求
	xhr.send(body) //get请求不传body参数，只有post请求使用
4) 接收响应	
	//在 onreadystatechange 事件中，我们规定当服务器响应已做好被处理的准备时所执行的任务。当 readyState 等于 4 且状态为 200 时，表示响应已就绪：
	xhr.onreadystatechange = function (){
    if(xhr.readyState == 4 && xhr.status == 200){
		//xhr.responseXML  接收xml格式的响应数据
		//xhr.responseText 接收文本格式的响应数据
        var text = xhr.responseText;
        console.log(text);
	}
}
```

| 方法                         | 描述                                                         |
| ---------------------------- | ------------------------------------------------------------ |
| open(*method*,*url*,*async*) | 规定请求的类型、URL 以及是否异步处理请求。*method*：请求的类型；GET 或 POST*url*：文件在服务器上的位置*async*：true（异步）或 false（同步） |
| send(*string*)               | 将请求发送到服务器。*string*：仅用于 POST 请求               |

**GET 还是 POST？**

​	与 POST 相比，GET 更简单也更快，并且在大部分情况下都能用。

然而，在以下情况中，请使用 POST 请求：

 ![](C:\资料备份\学习笔记\01-Web笔记\007-Ajax\01-Ajax\media\2022-07-21_105747.png)

**onreadystatechange事件：**

>当请求被发送到服务器时，我们需要执行一些基于响应的任务。每当 readyState 改变时，就会触发 onreadystatechange 事件。readyState 属性存有 XMLHttpRequest 的状态信息。下面是 XMLHttpRequest 对象的三个重要的属性：

| 属性               | 描述                                                         |
| ------------------ | ------------------------------------------------------------ |
| onreadystatechange | 存储函数（或函数名），每当 readyState 属性改变时，就会调用该函数。 |
| readyState         | 存有 XMLHttpRequest 的状态。从 0 到 4 发生变化。0: 请求未初始化1: 服务器连接已建立 2: 请求已接收 3: 请求处理中 4: 请求已完成，且响应已就绪。 |
| status             | 200: "OK" 404: 未找到页面                                    |

##### 1.8.2 案例如下

```HTML
//文件：GET.html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<style>
    #box {
        width: 200px;
        height: 80px;
        border: 2px solid rebeccapurple;
    }
</style>
<body>
    <button>点击发送请求</button>
<div id="box">

</div>
<script>
    const btn = document.getElementsByTagName('button')[0]
    const box = document.getElementById('box')
    btn.onclick = function(){
        //1创建对象
        const xhr = new XMLHttpRequest()
        //2初始 设置请求方法 url
        xhr.open('GET', 'http://127.0.0.1:8000/server')
        //可能得到的是缓存的结果。为了避免这种情况，请向 URL 添加一个唯一的 ID。xhr.open('GET', 'http://127.0.0.1:8000/server?t=' + Math.random())
        //3发送
        xhr.send();
        //4事件绑定 处理服务端返回的结果
        // on ---> when 当...时候
        // readystate 是xhr对象中的属性，表示状态 0 1 2 3 4
        // change 改变
        xhr.onreadystatechange = function(){
            //判断（服务端返回了所有的结果）
            if(xhr.readyState === 4){
                //判断响应状态码 200 404 403 401 500
                //2xx 成功
                if(xhr.status >= 200 && xhr.status < 300){
                    //处理结果 行 头 空行 体
                    console.log(xhr.status)//状态码
                    console.log(xhr.statusText)//状态字符串
                    console.log(xhr.getAllResponseHeaders())//所有响应头
                    console.log(xhr.response)//响应体

                    box.innerHTML=xhr.response

                }
            }
        }
    }
</script>
</body>

</html>

```

##### 1.8.3 AJAX 请求状态

​	xhr.readyState 可以用来查看请求当前的状态

​	https://developer.mozilla.org/zh-CN/docs/Web/API/XMLHttpRequest/readyState

​	0: 表示 XMLHttpRequest 实例已经生成，但是 open()方法还没有被调用。

​	1: 表示 send()方法还没有被调用，仍然可以使用 setRequestHeader()，设定HTTP请求的头信息。

​	2: 表示 send()方法已经执行，并且头信息和状态码已经收到。

​	3: 表示正在接收服务器传来的 body 部分的数据。

​	4: 表示服务器数据已经完全接收，或者本次接收已经失败了

```javascript
//文件：server.js
//1. 引入express
const express = require('express');

//2. 创建应用对象
const app = express();

//3. 创建路由规则
// request 是对请求报文的封装
// response 是对响应报文的封装
app.get('/server', (request, response)=>{
    //设置响应头 设置允许跨域
    response.setHeader('Access-Control-Allow-Origin','*');
    
    //设置响应
    response.send('HELLO AJAX');
});

//4. 监听端口启动服务
app.listen(8000, ()=>{
    console.log("服务已经启动, 8000 端口监听中....");
});
```

[^1]: 案例中server.js 假设目录在--->js/server.js，涉及到跨域，设置响应头，才能允许跨域response.setHeader('Access-Control-Allow-Origin','*');
[^2]: xhr.open('GET', 'http://127.0.0.1:8000/server') server是后台服务名--->对应于server.js文件中的路由创建app.get('/server',

#### 1.9 AJAX-设置请求参数

```javascript
xhr.open('GET', 'http://127.0.0.1:8000/server?a=100&b=200&c=300')
```

#### 1.10 AJAX-发送POST请求

```html
//文件：POST.html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<style>
    #box{
        width: 200px;
        height: 80px;
        border: 2px solid rebeccapurple;
    }
</style>
<body>
<div id="box">

</div>

<script>
    const box = document.getElementById('box')
    box.addEventListener("mouseover", function(){
        //1创建对象
        const xhr = new XMLHttpRequest()
        //2初始化 设置类型与URL
        xhr.open('POST', 'http://127.0.0.1:8000/server')
        //3发送
        xhr.send()
        //4事件绑定
        xhr.onreadystatechange = function(){
            if(xhr.readyState === 4){
                if(xhr.status >= 200 && xhr.status < 300){
                    box.innerHTML = xhr.response;
                }
            }
        }

    })
</script>
</body>

</html>
```

```javascript
//文件：server.js添加内容如下
app.post('/server', (request, response)=>{
    //设置响应头 设置允许跨域
    response.setHeader('Access-Control-Allow-Origin','*');
    
    //设置响应
    response.send('HELLO AJAX POST');
});
```

#### 1.11 AJAX-POST设置请求体

```javascript
//文件：POST.html 添加内容如下
//xhr.send('a=100&b=200&c=300');
//xhr.send('a:100&b=200&c=300');
xhr.send('1234567')
```

#### 1.12 AJAX-设置请求头信息

```javascript
//文件：POST.html 添加内容如下
//设置请求头
//下方代码必须放xhr.send()的前面，否则无法设置
xhr.setRequestHeader('Content-Type','application/x-www-form-urlencoded');
xhr.setRequestHeader('name','yrk');// 添加自定义会报错，如果想发必须修改server.js
```

```javascript
//文件：server.js添加内容如下
//注意：需修改可以接收任意类型的请求 因为返回类型不是post 会报错的
app.all('/server', (request, response) => {
    //设置响应头  设置允许跨域
    response.setHeader('Access-Control-Allow-Origin', '*');
    //响应头
    response.setHeader('Access-Control-Allow-Headers', '*');
    //设置响应体
    response.send('HELLO AJAX POST');
});
```

#### 1.13 AJAX-服务端响应JSON数据

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>JSON响应</title>
    <style>
        #result{
            width:200px;
            height:100px;
            border:solid 1px #89b;
        }
    </style>
</head>
<body>
    <div id="result"></div>
    <script>
        const result = document.getElementById('result');
        //绑定键盘按下事件
        window.onkeydown = function(){
            //发送请求
            const xhr = new XMLHttpRequest();
            //设置响应体数据的类型
            xhr.responseType = 'json';
            //初始化
            xhr.open('GET','http://127.0.0.1:8000/json-server');
            //发送
            xhr.send();
            //事件绑定
            xhr.onreadystatechange = function(){
                if(xhr.readyState === 4){
                    if(xhr.status >= 200 && xhr.status < 300){
                        // console.log(xhr.response);
                        // result.innerHTML = xhr.response;
                        // 1. 手动对数据转化
                        // let data = JSON.parse(xhr.response);
                        // console.log(data);
                        // result.innerHTML = data.name;
                        // 2. 自动转换
                        console.log(xhr.response);
                        result.innerHTML = xhr.response.name;
                    }
                }
            }
        }
    </script>
</body>
</html>
```

```javascript
//文件：server.js添加内容如下
//JSON 响应
app.all('/json-server', (request, response) => {
    //设置响应头  设置允许跨域
    response.setHeader('Access-Control-Allow-Origin', '*');
    //响应头
    response.setHeader('Access-Control-Allow-Headers', '*');
    //响应一个数据
    const data = {
        name: 'atguigu'
    };
    //对对象进行字符串转换
    let str = JSON.stringify(data);
    //设置响应体
    response.send(str);
});
```

#### 1.14 AJAX-nodemon自动重启工具

​	以前，我们开发一个node后端服务时，每次更改文件，均需重启一下，服务才能生效。这使我们的开发效率降低了很多。nodemon的出现，可以随时监听文件的变更，自动重启服务，我们开发时只需关注代码即可，不再需要手动重启服务。

全局安装

```text
npm install -g nodemon
```

开发环境安装

```text
npm install --save-dev nodemon
```

使用方法

```
nodemon 文件名.js
```

#### 1.15 AJAX-IE缓存问题解决

##### 1.4.3解决IE缓存问题

​	问题：在一些浏览器中(IE),由于缓存机制的存在，ajax 只会发送的第一次请求，剩余多次请求不会在发送给浏览器而是直接加载缓存中的数据。
​	解决方式：浏览器的缓存是根据 url 地址来记录的，所以我们只需要修改url 地址即可避免缓存问题
​	xhr.open("get","/testAJAX?t="+Date.now());

#### 1.16 AJAX-请求超时与网络异常

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>请求超时与网络异常</title>
    <style>
        #result{
            width:200px;
            height:100px;
            border:solid 1px #90b;
        }
    </style>
</head>
<body>
    <button>点击发送请求</button>
    <div id="result"></div>
    <script>
        const btn = document.getElementsByTagName('button')[0];
        const result = document.querySelector('#result');

        btn.addEventListener('click', function(){
            const xhr = new XMLHttpRequest();
            //超时设置 2s 设置
            xhr.timeout = 2000;
            //超时回调
            xhr.ontimeout = function(){
                alert("网络异常, 请稍后重试!!");
            }
            //网络异常回调
            xhr.onerror = function(){
                alert("你的网络似乎出了一些问题!");
            }

            xhr.open("GET",'http://127.0.0.1:8000/delay');
            xhr.send();
            xhr.onreadystatechange = function(){
                if(xhr.readyState === 4){
                    if(xhr.status >= 200 && xhr.status< 300){
                        result.innerHTML = xhr.response;
                    }
                }
            }
        })
    </script>
</body>
</html>
```

```javascript
//文件：server.js添加内容如下
//延时响应
app.all('/delay', (request, response) => {
    //设置响应头  设置允许跨域
    response.setHeader('Access-Control-Allow-Origin', '*');
    response.setHeader('Access-Control-Allow-Headers', '*');
    setTimeout(() => {
        //设置响应体
        response.send('延时响应');
    }, 1000)
});
```

#### 1.17 AJAX-取消请求

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>取消请求</title>
</head>
<body>
    <button>点击发送</button>
    <button>点击取消</button>
    <script>
        //获取元素对象
        const btns = document.querySelectorAll('button');
        let x = null;

        btns[0].onclick = function(){
            x = new XMLHttpRequest();
            x.open("GET",'http://127.0.0.1:8000/delay');
            x.send();
        }

        // abort取消发送
        btns[1].onclick = function(){
            x.abort();
        }
    </script>
</body>
</html>
```

#### 1.18 AJAX-请求重复发送问题

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>重复请求问题</title>
</head>
<body>
    <button>点击发送</button>
    <script>
        //获取元素对象
        const btns = document.querySelectorAll('button');
        let x = null;
        //标识变量
        let isSending = false; // 是否正在发送AJAX请求

        btns[0].onclick = function(){
            //判断标识变量
            if(isSending) x.abort();// 如果正在发送, 则取消该请求, 创建一个新的请求
            x = new XMLHttpRequest();
            //修改 标识变量的值
            isSending = true;
            x.open("GET",'http://127.0.0.1:8000/delay');
            x.send();
            x.onreadystatechange = function(){
                if(x.readyState === 4){
                    //修改标识变量
                    isSending = false;
                }
            }
        }
    </script>
</body>
</html>
```

#### 1.19 AJAX-jQuery发送AJAX请求

##### 1.19.1get请求

$.get(url, [data], [callback], [type])
	url:请求的 URL 地址。
	data:请求携带的参数。
	callback:载入成功时回调函数。
	type:设置返回内容格式，xml, html, script, json, text, _default。

##### 1.19.2post请求

$.post(url, [data], [callback], [type])
	url:请求的 URL 地址。
	data:请求携带的参数。
	callback:载入成功时回调函数。
	type:设置返回内容格式，xml, html, script, json, text, _default。

#### 1.20 AJAX-jQuery通用方法发送AJAX

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>jQuery 发送 AJAX 请求</title>
    <link crossorigin="anonymous" href="https://cdn.bootcss.com/twitter-bootstrap/3.3.7/css/bootstrap.min.css" rel="stylesheet">
    <script crossorigin="anonymous" src="https://cdn.bootcdn.net/ajax/libs/jquery/3.5.1/jquery.min.js"></script>
</head>
<body>
    <div class="container">
        <h2 class="page-header">jQuery发送AJAX请求 </h2>
        <button class="btn btn-primary">GET</button>
        <button class="btn btn-danger">POST</button>
        <button class="btn btn-info">通用型方法ajax</button>
    </div>
    <script>
        $('button').eq(0).click(function(){
            $.get('http://127.0.0.1:8000/jquery-server', {a:100, b:200}, function(data){
                console.log(data);
            },'json');
        });

        $('button').eq(1).click(function(){
            $.post('http://127.0.0.1:8000/jquery-server', {a:100, b:200}, function(data){
                console.log(data);
            });
        });

        $('button').eq(2).click(function(){
            $.ajax({
                //url
                url: 'http://127.0.0.1:8000/jquery-server',
                //参数
                data: {a:100, b:200},
                //请求类型
                type: 'GET',
                //响应体结果
                dataType: 'json',
                //成功的回调
                success: function(data){
                    console.log(data);
                },
                //超时时间
                timeout: 2000,
                //失败的回调
                error: function(){
                    console.log('出错啦!!');
                },
                //头信息
                headers: {
                    c:300,
                    d:400
                }
            });
        });

    </script>
</body>
</html>
```

```javascript
//文件：server.js添加内容如下
//jQuery 服务
app.all('/jquery-server', (request, response) => {
    //设置响应头  设置允许跨域
    response.setHeader('Access-Control-Allow-Origin', '*');
    response.setHeader('Access-Control-Allow-Headers', '*');
    // response.send('Hello jQuery AJAX');
    const data = {name:'yrk'};
    response.send(JSON.stringify(data));
});
```

#### 1.21 AJAX-Axios发送AJAX请求 

啊可笑s 

啊假可s

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>axios 发送 AJAX请求</title>
    <script crossorigin="anonymous" src="https://cdn.bootcdn.net/ajax/libs/axios/0.19.2/axios.js"></script>
</head>

<body>
    <button>GET</button>
    <button>POST</button>
    <button>AJAX</button>

    <script>
        // https://github.com/axios/axios
        const btns = document.querySelectorAll('button');

        //配置 baseURL
        axios.defaults.baseURL = 'http://127.0.0.1:8000';

        btns[0].onclick = function () {
            //GET 请求
            axios.get('/axios-server', {
                //url 参数
                params: {
                    id: 100,
                    vip: 7
                },
                //请求头信息
                headers: {
                    name: 'atguigu',
                    age: 20
                }
            }).then(value => {
                console.log(value);
            });
        }

        btns[1].onclick = function () {
            axios.post('/axios-server', {
                username: 'admin',
                password: 'admin'
            }, {
                //url 
                params: {
                    id: 200,
                    vip: 9
                },
                //请求头参数
                headers: {
                    height: 180,
                    weight: 180,
                }
            });
        }
    	//Axios函数发送AJAX
        btns[2].onclick = function(){
            axios({
                //请求方法
                method : 'POST',
                //url
                url: '/axios-server',
                //url参数
                params: {
                    vip:10,
                    level:30
                },
                //头信息
                headers: {
                    a:100,
                    b:200
                },
                //请求体参数
                data: {
                    username: 'admin',
                    password: 'admin'
                }
            }).then(response=>{
                //响应状态码
                console.log(response.status);
                //响应状态字符串
                console.log(response.statusText);
                //响应头信息
                console.log(response.headers);
                //响应体
                console.log(response.data);
            })
        }
    </script>
</body>

</html>
```

```javascript
//文件：server.js添加内容如下
//axios 服务
app.all('/axios-server', (request, response) => {
    //设置响应头  设置允许跨域
    response.setHeader('Access-Control-Allow-Origin', '*');
    response.setHeader('Access-Control-Allow-Headers', '*');
    // response.send('Hello jQuery AJAX');
    const data = {name:'尚硅谷'};
    response.send(JSON.stringify(data));
});
```

#### 1.22 AJAX-使用fetch函数发送AJAX

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>fetch 发送 AJAX请求</title>
</head>
<body>
    <button>AJAX请求</button>
    <script>
        //文档地址
        //https://developer.mozilla.org/zh-CN/docs/Web/API/WindowOrWorkerGlobalScope/fetch
        
        const btn = document.querySelector('button');

        btn.onclick = function(){
            fetch('http://127.0.0.1:8000/fetch-server?vip=10', {
                //请求方法
                method: 'POST',
                //请求头
                headers: {
                    name:'atguigu'
                },
                //请求体
                body: 'username=admin&password=admin'
            }).then(response => {
                // return response.text();
                return response.json();
            }).then(response=>{
                console.log(response);
            });
        }
    </script>
</body>
</html>
```

```javascript
//文件：server.js添加内容如下
//fetch 服务
app.all('/fetch-server', (request, response) => {
    //设置响应头  设置允许跨域
    response.setHeader('Access-Control-Allow-Origin', '*');
    response.setHeader('Access-Control-Allow-Headers', '*');
    // response.send('Hello jQuery AJAX');
    const data = {name:'尚硅谷'};
    response.send(JSON.stringify(data));
});
```

#### 1.23 AJAX-同源策略

​	同源策略（Same-Origin Policy）最早由Netscape公司提出，是浏览器的一种安全策略。

​	同源： 协议、域名、端口号 必须完全相同。

​	违背同源策略就是跨域。

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>首页</title>
</head>
<body>
    <h1>尚硅谷</h1>
    <button>点击获取用户数据</button>
    <script>
        const btn = document.querySelector('button');

        btn.onclick = function(){
            const x = new XMLHttpRequest();
            //这里因为是满足同源策略的, 所以 url 可以简写
            x.open("GET",'/data');
            //发送
            x.send();
            //
            x.onreadystatechange = function(){
                if(x.readyState === 4){
                    if(x.status >= 200 && x.status < 300){
                        console.log(x.response);
                    }
                }
            }
        }
    </script>
</body>
</html>
```

```javascript
const express = require('express');

const app = express();

app.get('/home', (request, response)=>{
    //响应一个页面
    response.sendFile(__dirname + '/index.html');
});

app.get('/data', (request, response)=>{
    response.send('用户数据');
});

app.listen(9000, ()=>{
    console.log("服务已经启动...");
});
```

操作步骤：浏览器输入127.0.0.1:9000/home ---> 返回index.html,这里需要注意路径问题。---> 点击按钮获取路由/data里面返回数据。

#### 1.24 AJAX-jsonp的实现原理

1) JSONP 是什么
	JSONP(JSON with Padding)，是一个非官方的跨域解决方案，纯粹凭借程序员的聪明才智开发出来，只支持 get 请求。
2) JSONP 怎么工作的？
	在网页有一些标签天生具有跨域能力，比如：img link iframe script。JSONP 就是利用 script 标签的跨域能力来发送请求的。
3) JSONP 的使用
	1.动态的创建一个 script 标签
		var script = document.createElement("script");
	2.设置 script 的 src，设置回调函数
		script.src = "http://localhost:3000/testAJAX?callback=abc";
		function abc(data) {
			alert(data.name);
		};
	3.将 script 添加到 body 中
		document.body.appendChild(script);
	4.服务器中路由的处理
		router.get("/testAJAX" , function (req , res) {
			console.log("收到请求");
			var callback = req.query.callback;
			var obj = {

​				name:"孙悟空",

​				age:18
​			}
​			res.send(callback+"("+JSON.stringify(obj)+")");
​		});

案例：

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>原理演示</title>
    <style>
        #result {
            width: 300px;
            height: 100px;
            border: solid 1px #78a;
        }
    </style>
</head>

<body>
    <div id="result"></div>
    <script>
        //处理数据
        function handle(data) {
            //获取 result 元素
            const result = document.getElementById('result');
            result.innerHTML = data.name;
        }
    </script>
    <!-- VScode 安装 Live Server插件 -->
    <!-- <script src="js/app.js"></script> -->
    <script src="http://127.0.0.1:5500/7-%E8%B7%A8%E5%9F%9F/2-JSONP/js/app.js"></script>
</body>

</html>
```

```javascript
//文件：js/app.js
const data = {
    name: 'yrk'
};

handle(data);
```

案例变形：

```html
//案例的html文件中
//注释代码：
<script src="http://127.0.0.1:5500/7-%E8%B7%A8%E5%9F%9F/2-JSONP/js/app.js"></script>
//添加代码：
<script src="http://127.0.0.1:8000/jsonp-server"></script>
```

```javascript
//文件：server.js添加内容如下
//jsonp服务
app.all('/jsonp-server',(request, response) => {
    // response.send('console.log("hello jsonp")');
    const data = {
        name: '尚硅谷atguigu'
    };
    //将数据转化为字符串
    let str = JSON.stringify(data);
    //返回结果
    response.end(`handle(${str})`);
});
```

#### 1.25 AJAX-原生jsonp实践

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>案例</title>
</head>
<body>
    用户名: <input type="text" id="username">
    <p></p>
    <script>
        //获取 input 元素
        const input = document.querySelector('input');
        const p = document.querySelector('p');
        
        //声明 handle 函数
        function handle(data){
            input.style.border = "solid 1px #f00";
            //修改 p 标签的提示文本
            p.innerHTML = data.msg;
        }

        //绑定事件
        input.onblur = function(){
            //获取用户的输入值
            let username = this.value;console.log(username)
            //向服务器端发送请求 检测用户名是否存在
            //1.创建 script 标签
            const script = document.createElement('script');
            //2. 设置标签的 src 属性
            script.src = 'http://127.0.0.1:8000/check-username?username='+username;
            //3. 将 script 插入到文档中
            document.body.appendChild(script);
        }
    </script>
</body>
</html>
```

```javascript
//文件：server.js添加内容如下
//用户名检测是否存在
app.all('/check-username',(request, response) => {
    // response.send('console.log("hello jsonp")');
    const data = {
        exist: 1,
        msg: '用户名已经存在'
    };
    //将数据转化为字符串
    let str = JSON.stringify(data);
    //返回结果
    response.end(`handle(${str})`);
});
```

#### 1.26 AJAX-jQuery发送jsonp请求

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>jQuery-jsonp</title>
    <style>
        #result{
            width:300px;
            height:100px;
            border:solid 1px #089;
        }
    </style>
    <script crossorigin="anonymous" src='https://cdn.bootcss.com/jquery/3.5.0/jquery.min.js'></script>
</head>
<body>
    <button>点击发送 jsonp 请求</button>
    <div id="result">

    </div>
    <script>
        $('button').eq(0).click(function(){
            $.getJSON('http://127.0.0.1:8000/jquery-jsonp-server?callback=?', function(data){
                $('#result').html(`
                    名称: ${data.name}<br>
                    校区: ${data.city}
                `)
            });
        });
    </script>
</body>
</html>
```

```javascript
//文件：server.js添加内容如下
//jquery-jsonp服务
app.all('/jquery-jsonp-server',(request, response) => {
    // response.send('console.log("hello jsonp")');
    const data = {
        name:'尚硅谷',
        city: ['北京','上海','深圳']
    };
    //将数据转化为字符串
    let str = JSON.stringify(data);
    //接收 callback 参数
    let cb = request.query.callback;

    //返回结果
    response.end(`${cb}(${str})`);
});
```

#### 1.27 AJAX-设置CORS响应头实现跨域

​	https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Access_control_CORS
1) CORS 是什么？
​	CORS（Cross-Origin Resource Sharing），跨域资源共享。CORS 是官方的跨域解决方案，它的特点是不需要在客户端做任何特殊的操作，完全在服务器中进行处理，支持get 和 post 请求。跨域资源共享标准新增了一组 HTTP 首部字段，允许服务器声明哪些源站通过浏览器有权限访问哪些资源
2) CORS 怎么工作的？
​	CORS 是通过设置一个响应头来告诉浏览器，该请求允许跨域，浏览器收到该响应以后就会对响应放行。
3) CORS 的使用
​	主要是服务器端的设置：
​	router.get("/testAJAX" , function (req , res) {

​		//通过 res 来设置响应头，来允许跨域请求

​		//res.set("Access-Control-Allow-Origin","http://127.0.0.1:3000");

​		res.set("Access-Control-Allow-Origin","*");

​		res.send("testAJAX 返回的响应");
​	});

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>CORS</title>
    <style>
        #result{
            width:200px;
            height:100px;
            border:solid 1px #90b;
        }
    </style>
</head>
<body>
    <button>发送请求</button>
    <div id="result"></div>
    <script>
        const btn = document.querySelector('button');

        btn.onclick = function(){
            //1. 创建对象
            const x = new XMLHttpRequest();
            //2. 初始化设置
            x.open("GET", "http://127.0.0.1:8000/cors-server");
            //3. 发送
            x.send();
            //4. 绑定事件
            x.onreadystatechange = function(){
                if(x.readyState === 4){
                    if(x.status >= 200 && x.status < 300){
                        //输出响应体
                        console.log(x.response);
                    }
                }
            }
        }
    </script>
</body>
</html>
```

```javascript
//文件：server.js添加内容如下
app.all('/cors-server', (request, response)=>{
    //设置响应头
    response.setHeader("Access-Control-Allow-Origin", "*");
    response.setHeader("Access-Control-Allow-Headers", '*');
    response.setHeader("Access-Control-Allow-Method", '*');
    // response.setHeader("Access-Control-Allow-Origin", "http://127.0.0.1:5500");
    response.send('hello CORS');
});
```

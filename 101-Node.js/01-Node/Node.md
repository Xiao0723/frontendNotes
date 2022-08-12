###  1.初识Node.js

#### 1.1 回顾与思考

##### 1.1.1 已经掌握了那些技术

 ![](C:\资料备份\学习笔记\01-Web笔记\101-Node.js\images\2022-07-24_092332.png)

##### 1.1.2 浏览器中的 JavaScript的组成部分

 ![](C:\资料备份\学习笔记\01-Web笔记\101-Node.js\images\2022-07-24_092411.png)

##### 1.1.3 思考：为什么JavaScript 可以在浏览器中被执行

 ![](C:\资料备份\学习笔记\01-Web笔记\101-Node.js\images\2022-07-24_092802.png)

##### 1.1.4 思考：为什么JavaScript可以操作DOM和BOM

 ![](C:\资料备份\学习笔记\01-Web笔记\101-Node.js\images\2022-07-24_092906.png)

##### 1.1.5 浏览器中的JavaScript运行环境

 ![](C:\资料备份\学习笔记\01-Web笔记\101-Node.js\images\2022-07-24_093014.png)

##### 1.1.6 思考：JavaScript能否做后端开发

 ![](C:\资料备份\学习笔记\01-Web笔记\101-Node.js\images\2022-07-24_093752.png)

#### 1.2 Node.js简介

##### 1.2.1 什么是Node.js

​	Node.js® is a JavaScript runtime built on Chrome's V8 JavaScript engine.

Node.js 是一个基于 Chrome V8 引擎的 JavaScript 运行环境。

​	Node.js的官网地址：<https://nodejs.org/zh-cn/>

##### 1.2.2 Node.js中的JavaScript运行环境

 ![](C:\资料备份\学习笔记\01-Web笔记\101-Node.js\images\2022-07-24_094141.png)

##### 1.2.3 Node.js可以做什么

​	Node.js 作为一个 JavaScript 的运行环境，仅仅提供了基础的功能和 API。然而，基于 Node.js 提供的这些基础能，很多强大的工具和框架如雨后春笋，层出不穷，所以学会了 Node.js ，可以让前端程序员胜任更多的工作和岗位：

​	①基于 Express 框架（<http://www.expressjs.com.cn/>），可以快速构建 Web 应用

​	②基于 Electron 框架（<https://electronjs.org/>），可以构建跨平台的桌面应用

​	③基于 restify 框架（<http://restify.com/>），可以快速构建 API 接口项目

​	④读写和操作数据库、创建实用的命令行工具辅助前端开发、etc…

​	总之：Node.js 是大前端时代的“大宝剑”，有了 Node.js 这个超级 buff 的加持，前端程序员的行业竞争力会越来越强！

##### 1.2.4 Node.js如何学习

会javaScript,就能学会Node.js!!!

浏览器中的 JavaScript 学习路径：

​	JavaScript 基础语法 + 浏览器内置 API（DOM + BOM） + 第三方库（jQuery、art-template 等）

Node.js 的学习路径：

​	JavaScript 基础语法 + Node.js 内置 API 模块（fs、path、http等）+ 第三方 API 模块（express、mysql 等）

#### 1.3 Node.js环境的安装

​	如果希望通过 Node.js 来运行 Javascript 代码，则必须在计算机上安装 Node.js 环境才行。

​	安装包可以从 Node.js 的官网首页直接下载，进入到 Node.js 的官网首页（**https://nodejs.org/en/**），点击绿色的按钮，下载所需的版本后，双击直接安装即可。

##### 1.3.1 区分LTS版本和Current版本的不同

​	①LTS 为长期稳定版，对于追求稳定性的企业级项目来说，推荐安装 LTS 版本的 Node.js。

​	②Current 为新特性尝鲜版，对热衷于尝试新特性的用户来说，推荐安装 Current 版本的 Node.js。但是，Current 版本中可能存在隐藏的 Bug 或安全性漏洞，因此不推荐在企业级项目中使用 Current 版本的 Node.js。

##### 1.3.2 查看已安装的Node.js的版本号

​	打开终端，在终端输入命令 node –v 后，按下回车键，即可查看已安装的 Node.js 的版本号。

Windows 系统快速打开终端的方式：

​	使用快捷键（Windows徽标键 + R）打开运行面板，输入 cmd 后直接回车，即可打开终端。

##### 1.3.3 什么是终端

 ![](C:\资料备份\学习笔记\01-Web笔记\101-Node.js\images\2022-07-24_095225.png)

#### 1.4 在Node.js环境中执行JavaScript代码

​	①打开终端

​	②输入 node 要执行的js文件的路径

##### 1.4.1 终端中的快捷键

​	在 Windows 的 powershell 或 cmd 终端中，我们可以通过如下快捷键，来提高终端的操作效率：

​	①使用 ↑ 键，可以快速定位到上一次执行的命令

​	②使用 tab 键，能够快速补全路径

​	③使用 esc 键，能够快速清空当前已输入的命令

​	④输入 cls 命令，可以清空终端

### 2.fs文件系统模块

#### 2.1 什么是fs文件系统模块

​	fs 模块是 Node.js 官方提供的、用来操作文件的模块。它提供了一系列的方法和属性，用来满足用户对文件的操作需求。

例如：

- fs.readFile() 方法，用来读取指定文件中的内容
- fs.writeFile() 方法，用来向指定的文件中写入内容 

如果要在 JavaScript 代码中，使用 fs 模块来操作文件，则需要使用如下的方式先导入它：

```
const fs = require('fs')
```

#### 2.2 读取指定文件中的内容

##### 2.2.1 fs.readFile()的语法格式

使用fs.readFile()方法，可以读取指定文件中的内容，语法格式如下：

```javascript
fs.readFile(path[,options], callback)
```

参数解读：

- 参数1：必选参数，字符串，表示文件的路径。
- 参数2：可选参数，表示以什么编码格式来读取文件。
- 参数3：必选参数，文件读取完成后，通过回调函数拿到读取的结果

##### 2.2.1 fs.readFile()的示例代码

以utf8的编码格式，读取指定文件的内容，并打印err和dataStr的值：

```javascript
const fs = require('fs')
fs.readFile('./files/11.txt', 'utf8', function(err, dataStr) {
    console.log(err)
    console.log('------')
    console.log(dataStr)
})
```

##### 2.2.3 判断文件是否读取成功

可以判断err对象是否为null，从而知晓文件读取的结果：

```
const fs = require('fs')
fs.readFile('./files/1.txt','utf8', function(err, result){
    if(err) {
        return console.log('文件读取失败'+ err.message)
    }
    console.log('文件读取成功，内容是：' +  result)
})
```
#### 2.3先指定的文件中写入内容
##### 2.3.1 fs.writeFile()的语法格式
使用fs.writeFile()方法，可以向指定的文件中写入内容，语法格式如下：
```
fs.writeFile(file, data[,options], callback)
```
参数解读：

- 参数1：必选参数，需要指定一个文件路径的字符串，表示文件的存放路径。
- 参数2：必选参数，表示要写入的内容。
- 参数3：可选参数，表示以什么格式写入文件内容，默认值是 utf8。
- 参数4：必选参数，文件写入完成后的回调函数。
##### 2.3.2 fs.writeFile()的示例代码
向指定的文件路径中，写入文件内容：
```
const fs = require('fs')
fs.writeFile('./files/2.txt', 'hello Node.js', function(err) {
    console.log(err)
})
```
##### 2.3.3判断文件是否写入成功
可以判断err对象是否为null，从而知晓文件写入的结果：
```
const fs = require('fs')
fs.writeFile('F:/files/2.txt', 'Hello Node.js', function(err){
    if(err){
        return console.log('文件写入失败' + err.message)
    }
	console.log('文件写入成功')
})
```
#### 2.4 练习-考试成绩整理
使用fs文件系统模块，将素材目录下成绩.txt文件中的考试数据，整理到成绩-ok.txt文件中。
整理前，成绩.txt文件的数据格式如下：
```
小红=99 小白=100 小黄=70 小黑=66 小绿=88
```
整理完成后，成绩-ok.txt文件中数据格式如下：
```
小红:99
小白:100
小黄:70
小黑:66
小绿:88
```
核心实现步骤
```javascript
// 1. 导入 fs 模块
const fs = require('fs')

// 2. 调用 fs.readFile() 读取文件的内容
fs.readFile('../素材/成绩.txt', 'utf8', function(err, dataStr) {
  // 3. 判断是否读取成功
  if (err) {
    return console.log('读取文件失败！' + err.message)
  }
  // console.log('读取文件成功！' + dataStr)

  // 4.1 先把成绩的数据，按照空格进行分割
  const arrOld = dataStr.split(' ')
  // 4.2 循环分割后的数组，对每一项数据，进行字符串的替换操作
  const arrNew = []
  arrOld.forEach(item => {
    arrNew.push(item.replace('=', '：'))
  })
  // 4.3 把新数组中的每一项，进行合并，得到一个新的字符串
  const newStr = arrNew.join('\r\n')

  // 5. 调用 fs.writeFile() 方法，把处理完毕的成绩，写入到新文件中
  fs.writeFile('./files/成绩-ok.txt', newStr, function(err) {
    if (err) {
      return console.log('写入文件失败！' + err.message)
    }
    console.log('成绩写入成功！')
  })
})

```
#### 2.5 fs模块-路径动态拼接的问题
​	在使用 fs 模块操作文件时，如果提供的操作路径是以 ./ 或 ../ 开头的相对路径时，很容易出现路径动态拼接错误的问题。
​	原因：代码在运行的时候，会以执行 node 命令时所处的目录，动态拼接出被操作文件的完整路径。
​	解决方案：在使用 fs 模块操作文件时，直接提供完整的路径，不要提供 ./ 或 ../ 开头的相对路径，从而防止路径动态拼接的问题。

```javascript
const fs = require('fs')
// 出现路径拼接错误的问题，是因为提供了 ./ 或 ../ 开头的相对路径
// 如果要解决这个问题，可以直接提供一个完整的文件存放路径就行
/* fs.readFile('./files/1.txt', 'utf8', function(err, dataStr) {
  if (err) {
    return console.log('读取文件失败！' + err.message)
  }
  console.log('读取文件成功！' + dataStr)
}) */

// 移植性非常差、不利于维护
/* fs.readFile('C:\\Users\\escook\\Desktop\\Node.js基础\\day1\\code\\files\\1.txt', 'utf8', function(err, dataStr) {
  if (err) {
    return console.log('读取文件失败！' + err.message)
  }
  console.log('读取文件成功！' + dataStr)
}) */

// __dirname 表示当前文件所处的目录
// console.log(__dirname)

fs.readFile(__dirname + '/files/1.txt', 'utf8', function(err, dataStr) {
  if (err) {
    return console.log('读取文件失败！' + err.message)
  }
  console.log('读取文件成功！' + dataStr)
})

```

### 3.path 路径模块

#### 3.1 什么是path路径模块

​	path 模块是 Node.js 官方提供的、用来处理路径的模块。它提供了一系列的方法和属性，用来满足用户对路径的处理需求。

例如：

- path.join() 方法，用来将多个路径片段拼接成一个完整的路径字符串
- path.basename() 方法，用来从路径字符串中，将文件名解析出来

如果要在JavaScript代码中，使用path模块来处理路径，则需要使用如下的方式先导入它：

```javascript
const path = require('path')
```

#### 3.2 路径拼接

##### 3.2.1 path.join()的语法格式

使用path.join()方法，可以把多个路径片段拼接为完整的路径字符串，语法格式如下：

```
path.join([...paths])
```

参数解读：

- ...paths <string> 路径片段的序列
- 返回值: <string>

##### 3.2.2 path.join()的代码示例

使用path.join()方法，可以把多个路径片段拼接为完整的路径字符串：

```javascript
const pathStr = path.join('/a', '/b/c', '../', './d', 'e')  // 注意：../ 会抵消前面的路径
console.log(pathStr) // 输出\a\b\d\e

const pathStr2 = path.join(__dirname, './files/1.txt')
console.log(pathStr2)  
// 输出当前文件所处目录\files\1.txt
```

注意：今后凡是涉及到路径拼接的操作，都要使用 path.join()方法进行处理。不要直接使用 + 进行字符串的拼接。

#### 3.3 获取路径中的文件名

##### 3.3.1 path.basename()的语法格式

使用path.basename()方法，可以获取路径中的最后一部分，经常通过这个方法获取路径中的文件名，语法格式如下：

```
path.basename(path[, ext])
```

参数解读：

- path <string> 必选参数，表示一个路径的字符串
- ext <string> 可选参数，表示文件扩展名
- 返回: <string> 表示路径中的最后一部分

##### 3.3.2 path.basename()的代码示例

使用path.basename()方法，可以从一个文件路径中，获取到文件的名称部分：

```javascript
const fpath = '/a/b/c/index.html'  //文件的存放路径

var fullName = path.basename(fpath)
console.log(fullName)	//输出index.html

var nameWithoutExt = path.basename(fpath, '.html')
console.log(nameWithoutExt)   //输出index
```

#### 3.4 获取路径中的文件扩展名

##### 3.4.1 path.extname()的语法格式

使用path.extname() 方法，可以获取路径中的拓展名部分，语法格式如下：

```
path.extname(path)
```

参数解读：

- path <string>必选参数，表示一个路径的字符串
- 返回: <string> 返回得到的扩展名字符串

##### 3.4.2 path.extname()的代码示例

使用path.extname()方法，可以获取路径中的扩展名部分：

```javascript
const fpath = '/a/b/c/index.html' // 路径字符串

const fext = path.extname(fpath)
console.log(fext) // 输出.html
```

#### 3.5 综合案例 - 时钟案例

##### 3.5.1 案例要实现的功能

 ![](C:\资料备份\学习笔记\01-Web笔记\101-Node.js\images\2022-07-25_104612.png)

##### 3.5.2 案例的实现步骤

​	①创建两个正则表达式，分别用来匹配 <style> 和 <script> 标签

​	②使用 fs 模块，读取需要被处理的 HTML 文件

​	③自定义 resolveCSS 方法，来写入 index.css 样式文件

​	④自定义 resolveJS 方法，来写入 index.js 脚本文件

​	⑤自定义 resolveHTML 方法，来写入 index.html 文件

步骤1 - 导入需要的模块并创建正则表达式

```javascript
// 1.1 导入 fs 模块
const fs = require('fs')
// 1.2 导入 path 模块
const path = require('path')

// 1.3 定义正则表达式，分别匹配 <style></style> 和 <script></script> 标签
const regStyle = /<style>[\s\S]*<\/style>/
const regScript = /<script>[\s\S]*<\/script>/
```

步骤2 - 使用fs模块读取需要被处理的html文件

```javascript
// 2.1 调用 fs.readFile() 方法读取文件
fs.readFile(path.join(__dirname, '../素材/index.html'), 'utf8', function(err, dataStr) {
  // 2.2 读取 HTML 文件失败
  if (err) return console.log('读取HTML文件失败！' + err.message)
  // 2.3 读取文件成功后，调用对应的三个方法，分别拆解出 css, js, html 文件
  resolveCSS(dataStr)
  resolveJS(dataStr)
  resolveHTML(dataStr)
})
```

步骤3 - 自定义resolveCSS方法

```javascript
// 3.1 定义处理 css 样式的方法
function resolveCSS(htmlStr) {
  // 3.2 使用正则提取需要的内容
  const r1 = regStyle.exec(htmlStr)
  // 3.3 将提取出来的样式字符串，进行字符串的 replace 替换操作
  const newCSS = r1[0].replace('<style>', '').replace('</style>', '')
  // 3.4 调用 fs.writeFile() 方法，将提取的样式，写入到 clock 目录中 index.css 的文件里面
  fs.writeFile(path.join(__dirname, './clock/index.css'), newCSS, function(err) {
    if (err) return console.log('写入 CSS 样式失败！' + err.message)
    console.log('写入样式文件成功！')
  })
}
```

步骤4 - 自定义resolveJS方法

```javascript
// 4.1 定义处理 js 脚本的方法
function resolveJS(htmlStr) {
  // 4.2 通过正则，提取对应的 <script></script> 标签内容
  const r2 = regScript.exec(htmlStr)
  // 4.3 将提取出来的内容，做进一步的处理
  const newJS = r2[0].replace('<script>', '').replace('</script>', '')
  // 4.4 将处理的结果，写入到 clock 目录中的 index.js 文件里面
  fs.writeFile(path.join(__dirname, './clock/index.js'), newJS, function(err) {
    if (err) return console.log('写入 JavaScript 脚本失败！' + err.message)
    console.log('写入 JS 脚本成功！')
  })
}
```

步骤5 - 自定义resolveHTML方法

```javascript
// 5.1 定义处理 HTML 结构的方法
function resolveHTML(htmlStr) {
  // 5.2 将字符串调用 replace 方法，把内嵌的 style 和 script 标签，替换为外联的 link 和 script 标签
  const newHTML = htmlStr.replace(regStyle, '<link rel="stylesheet" href="./index.css" />').replace(regScript, '<script src="./index.js"></script>')
  // 5.3 写入 index.html 这个文件
  fs.writeFile(path.join(__dirname, './clock/index.html'), newHTML, function(err) {
    if (err) return console.log('写入 HTML 文件失败！' + err.message)
    console.log('写入 HTML 页面成功！')
  })
}
```

##### 3.5.3 案例的两个注意点

​	①fs.writeFile() 方法只能用来创建文件，不能用来创建路径

​	②重复调用 fs.writeFile() 写入同一个文件，新写入的内容会覆盖之前的旧内容

### 4.http模块

#### 4.1 什么是http模块

回顾：什么是客户端、什么是服务器？

​	在网络节点中，负责消费资源的电脑，叫做客户端；负责对外提供网络资源的电脑，叫做服务器。

​	http 模块是 Node.js 官方提供的、用来创建 web 服务器的模块。通过 http 模块提供的 http.createServer() 方法，就能方便的把一台普通的电脑，变成一台 Web 服务器，从而对外提供 Web 资源服务。

如果要希望使用 http 模块创建 Web 服务器，则需要先导入它：

```
const http = require('http')
```

#### 4.2 进一步理解http模块的作用

​	服务器和普通电脑的区别在于，服务器上安装了web服务器软件，例如：IIS、Apache等。通过安装这些服务器软件，就能把一台普通的电脑变成一台web服务器。

​	在Node.j中，我们不需要使用IIS、Apache等这些第三方web服务器软件。因为我们可以基于Node.js提供的http模块，通过几行简单的代码，就能轻松的手写一个服务器软件，从而对外提供web服务。

#### 4.3 服务器相关的概念

##### 4.3.1 IP地址

​	**IP** **地址**就是互联网上每台计算机的唯一地址，因此 IP 地址具有唯一性。如果把“个人电脑”比作“一台电话”，那么“IP地址”就相当于“电话号码”，只有在知道对方 IP 地址的前提下，才能与对应的电脑之间进行数据通信。

​	IP 地址的格式：通常用“点分十进制”表示成（a.b.c.d）的形式，其中，a,b,c,d 都是 0~255 之间的十进制整数。例如：用点分十进表示的 IP地址（192.168.1.1）

注意：

​	①**互联网中每台** **Web** **服务器，都有自己的** **IP** **地址**，例如：大家可以在 Windows 的终端中运行 ping www.baidu.com 命令，即可查看到百度服务器的 IP 地址。

​	②在开发期间，自己的电脑既是一台服务器，也是一个客户端，为了方便测试，可以在自己的浏览器中输入 127.0.0.1 这个 IP 地址，就能把自己的电脑当做一台服务器进行访问了。

##### 4.3.2 域名和域名服务器

​	尽管 IP 地址能够唯一地标记网络上的计算机，但IP地址是一长串数字，不直观，而且不便于记忆，于是人们又发明了另一套字符型的地址方案，即所谓的域名（Domain Name）地址。

​	IP地址和域名是一一对应的关系，这份对应关系存放在一种叫做**域名服务器**(DNS，Domain name server)的电脑中。使用者只需通过好记的域名访问对应的服务器即可，对应的转换工作由域名服务器实现。因此，**域名服务器就是提供** **IP** **地址和域名之间的转换服务的服务器**。

注意：

​	①单纯使用 IP 地址，互联网中的电脑也能够正常工作。但是有了域名的加持，能让互联网的世界变得更加方便。

​	②在开发测试期间， 127.0.0.1 对应的域名是 localhost，它们都代表我们自己的这台电脑，在使用效果上没有任何区别。

##### 4.3.3 端口号

​	计算机中的端口号，就好像是现实生活中的门牌号一样。通过门牌号，外卖小哥可以在整栋大楼众多的房间中，准确把外卖送到你的手中。

​	同样的道理，在一台电脑中，可以运行成百上千个 web 服务。每个 web 服务都对应一个唯一的端口号。客户端发送过来的网络请求，通过端口号，可以被准确地交给对应的 web 服务进行处理。

 ![](C:\资料备份\学习笔记\01-Web笔记\101-Node.js\images\2022-07-25_112601.png)

#### 4.4 创建最基本的web服务器

##### 4.4.1 创建web服务器的基本步骤

​	①导入 http 模块

​	②创建 web 服务器实例

​	③为服务器实例绑定 **request** 事件，监听客户端的请求

​	④启动服务器

##### 4.4.2 代码实现

```javascript
//步骤1：如果希望在自己的电脑上创建一个 web 服务器，从而对外提供 web 服务，则需要导入 http 模块：
const http = require('http')
//步骤2：调用 http.createServer() 方法，即可快速创建一个 web 服务器实例：
const server = http.createServer()
//步骤3：为服务器实例绑定 request 事件，即可监听客户端发送过来的网络请求：
//使用服务器实例的.on()方法，为服务器绑定一个request事件
server.on('request', (req, res)=> {
    //只有有客户端来请求我们自己的服务器，就会触发request事件，从而调用这个事件处理函数
    console.log('Someone visit our web server.')
})
//步骤4：启动服务器，调用服务器实例的.listen()方法，即可启动当前的web服务器实例：
server.listen(80, () => {
    console.log('http server running at ahttp://127.0.0.1')
})
```

##### 4.4.3 req请求对象

​	只要服务器接收到了客户端的请求，就会调用通过 server.on() 为服务器绑定的 request 事件处理函数。

如果想在事件处理函数中，访问与客户端相关的**数据**或**属性**，可以使用如下的方式：

```javascript
server.on('request', (req, res) => {
    //req 是请求对象，它包含了与客户端相关的数据喝属性，例如：
    //req.url 是客户端请求的URL地址
    //req.method 是客户端的method请求类型
    const str = `Your request url is ${req.url}, and request method is ${req.method}`
    console.log(str)
})
```

##### 4.4.4 res响应对象

在服务器的request事件处理函数中，如果想访问与服务器相关的数据或属性，可以使用如下的方式：

```javascript
server.on('request', (req, res) => {
    // res 是响应对象，它包含了与服务器相关的数据和属性，例如：
    // 要发送到客户端的字符串
    const str = `Your request url is ${req.url}, and request method is ${req.method}`
    // res.end() 方法作用：
    // 向客户端发送指定的内容，并结束这次请求的处理过程
    res.end(str)
})
```

##### 4.4.5 解决中文乱码问题

当调用res.end()方法，向客户端发送中文内容的时候，会出现乱码问题，此时，需要手动设置内容的编码格式：

```javascript
server.on('request', (req, res) => {
	// 发送的内容包含中文
	const str = `您请求的url地址是${req.url},请求的method类型是${req.method}`
	// 为了防止中文显示乱码的问题，需要设置响应头Content-Type的值为text/html;charset=utf-8
    res.setHeader('Content-Type', 'text/html; charset=utf-8')
	// 把包含中文的内容，响应给客户端
	res.end(str)
})
```

#### 4.5 根据不同的url响应不同的htmlneir

##### 4.5.1 核心实现步骤

​	①获取请求的 url 地址

​	②设置默认的响应内容为 404 Not found

​	③判断用户请求的是否为 / 或 /index.html 首页

​	④判断用户请求的是否为 /about.html 关于页面

​	⑤设置 Content-Type 响应头，防止中文乱码

​	⑥使用 res.end() 把内容响应给客户端

##### 4.5.2 动态响应内容

```javascript
server.on('request', (req, res) => {
	const url = req.url	// 1.获取请求的url地址
	let content =  '<h1>404 Not found!</h1>' // 2.设置默认的内容为 404 Not found
    if(url === '/' || url === '/index.html') {
        content = '<h1> 首页 </h1>' // 3.用户请求的是首页
    } else if(url === '/about.html') {
        content ='<h1>关于页面</h1>' // 4.用户请求的是关于页面
    }
    res.setHeader('Content-Type', 'text/html; charset=utf-8') // 5.防止中文乱码
    res.end(content) // 6.把内容发送给客户端

})
```

#### 4.6 案例 - 实现clock时钟的web服务器

##### 4.6.1 核心思路

把文件的实际存放路径，作为每个资源的请求url地址。

 ![](C:\资料备份\学习笔记\01-Web笔记\101-Node.js\images\2022-07-26_095614.png)

##### 4.6.2 实现步骤

​	①导入需要的模块

​	②创建基本的 web 服务器

​	③将资源的请求 url 地址映射为文件的存放路径

​	④读取文件内容并响应给客户端

​	⑤优化资源的请求路径

##### 4.6.3 代码实现

```javascript
// 步骤1 - 导入需要的模块
// 1.1导入http模块
const http = require('http')
// 1.2导入fs文件系统模块
const fs = require('fs')
// 1.3导入path路径处理模块
const path = require('path')

// 步骤2 - 创建基本的web服务器
// 2.1创建web服务器
const server = http.createServer()
// 2.2监听web服务器的request事件
server.on('request', (req, res) => {
    
})
// 2.3启动web服务器
server.listen(80, () => {
    console.log('server listen running at http://127.0.0.1:80')
})

// 步骤3 - 将资源的请求url地址映射为文件的存放路径
// 3.1获取到客户端请求的url地址
const url = req.url
// 3.2把请求的url地址，映射为本地文件的存放路径
const fpath = path.join(__dirname, url)

// 步骤4 - 读取文件的内容并响应给客户端
// 4.1根据“映射”过来的文件路径读取文件
fs.readFile(fpath, 'utf8', (err, dataStr) => {
    // 4.2读取文件失败后，向客户端响应固定的“错误消息”
    if(err) return res.end('404 Not fount.')
    // 4.3读取文件成功后，将“读取成功的内容”响应给客户端
    res.end(dataStr)
})
```

```javascript
// 步骤5 - 优化资源的请求路径
// *** 将3.2的实现方式，改为如下代码 ***
// 5.1预定义空白的文件存放路径
let fpath = ''
if(url === '/') {
    // 5.2如果请求的路径为/,则手动指定文件的存放路径
    fpath = path.join(__dirname, './clock/index.html')
}else {
    // 5.3如果请求路径不为/,则动态拼接文件的存放路径
    fpath = path.join(__dirname, './clock', url)
}
```

### 5.模块化的基本概念

#### 5.1 什么是模块化

​	模块化是指解决一个复杂问题时，自顶向下逐层把系统划分成若干模块的过程。对于整个系统来说，模块是可组合、分解和更换的单元。

##### 5.1.1 现实生活中的模块化

 ![](C:\资料备份\学习笔记\01-Web笔记\101-Node.js\images\2022-07-26_104306.png)

##### 5.1.2  编程领域中的模块化

​	编程领域中的模块化，就是遵循固定的规则，把一个大文件拆成独立并互相依赖的多个小模块。

把代码进行模块化拆分的好处：

​	①提高了代码的复用性

​	②提高了代码的可维护性

​	③可以实现按需加载

#### 5.2 模块化规范

​	模块化规范就是对代码进行模块化的拆分与组合时，需要遵守的那些规则。

例如：

- 使用什么样的语法格式来引用模块
- 在模块中使用什么样的语法格式向外暴露成员

模块化规范的好处：

​	大家都遵守同样的模块化规范写代码，降低了沟通的成本，极大方便了各个模块之间的相互调用，利人利己。

### 6.Node.js中模块化

#### 6.1 Node.js中模块的分类

Node.js中根据模块来源不同，将模块分为了3大类，分别是：

- 内置模块（内置模块是由 Node.js 官方提供的，例如 fs、path、http 等）
- 自定义模块（用户创建的每个 .js 文件，都是自定义模块）
- 第三方模块（由第三方开发出来的模块，并非官方提供的内置模块，也不是用户创建的自定义模块，使用前需要先下载）

#### 6.2 加载模块

​	使用强大的require()方法，可以加载需要的内置模块、用户自定义模块、第三方模块进行使用。

例如：

```javascript
// 1.加载内置的fs模块
const fs = require('fs')

// 2.加载用户的自定义模块
const custom = require('./custom.js')

// 3.加载第三方模块(关于第三方模块的下载和使用，会在后面的课程中进行专门的讲解)
const moment = require('moment')
```

注意： 使用require()方法加载其他模块时，会执行被加载模块中的代码。

#### 6.3 Node.js中的模块作用域

##### 6.3.1 什么是模块作用域

​	和函数作用域类似，在自定义模块定义的变量、方法等成员，只能在当前模块内被访问，这种模块级别的访问限制，叫做模块作用域。

```javascript
// 01.custom.js模块
const username = 'yrk'
function sayHello() {
    console.log('hello, 我是' + username)
}
```

```javascript
const custom = require('01.custom')
console.log(custom) //输出{}空对象，在02.test.js模块中，无法访问到01.custom.js模块中的私有成员
```

##### 6.3.2 模块作用域的好处

​	防止了全局变量污染的问题

 ![](C:\资料备份\学习笔记\01-Web笔记\101-Node.js\images\2022-07-26_114304.png)

#### 6.4 向外共享模块作用域中的成员

##### 6.4.1 module对象

在每个.js自定义模块中都有一个module对象，它里面存储了和当前模块有关的信息，打印如下：

 ![](C:\资料备份\学习笔记\01-Web笔记\101-Node.js\images\2022-07-26_114804.png)

##### 6.4.2 module.exports对象

​	在自定义模块中，可以使用module.exports对象，将模块内的成员共享出去，供外界使用。

​	外界用require()方法导入自定义模块时，得到的就是module.exports所指向的对象。

##### 6.4.3 共享成员时的注意点

使用require()方法导入模块时，导入的结果，永远以module.exports指向的对象为准。

 ![](C:\资料备份\学习笔记\01-Web笔记\101-Node.js\images\2022-07-26_142020.png)

##### 6.4.4 exports对象

​	由于module.exports单词写起来比较复杂，为了简化向外共享成员的代码，Node提供了exports对象。默认情况下，exports 和module.exports 指向同一个对象。最终共享的结果，还是以 module.exports指向的对象为准。

 ![](C:\资料备份\学习笔记\01-Web笔记\101-Node.js\images\2022-07-26_143327.png)

##### 6.4.5 exports和module.exports的使用误区

时刻谨记，require()模块时，得到的永远是module.exports指向的对象：

 ![](C:\资料备份\学习笔记\01-Web笔记\101-Node.js\images\2022-07-26_143645.png)

注意：为了防止混乱，建议大家不要在同一个模块中同时使用exports和module.exports

#### 6.5 Node.js中的模块化规范

​	Node.js遵循了CommonJS模块化规范，CommonJS规定了模块的特性和各模块之间如何相互依赖。

**CommonJS规定:**

​	①每个模块内部，module 变量代表当前模块。

​	②module 变量是一个对象，它的 exports 属性（即 module.exports）是对外的接口。

​	③加载某个模块，其实是加载该模块的 module.exports 属性。require() 方法用于加载模块。

### 7.npm与包

#### 7.1 包

##### 7.1.1 什么是包

​	Node.js中的第三方模块又叫做包。

​	就像电脑和计算机指的是相同的东西，第三方模块和包指的是同一个概念，只不过叫法不同。

##### 7.1.2 包的来源

​	不同Node.js中的内置模块与自定义模块，包是由第三方个人或团队开发出来的，免费供所有人使用。

注意：Node.js中的包都是免费且开源的，不需要付费即可免费下载使用。

##### 7.1.3 为什么需要包

​	由于 Node.js 的内置模块仅提供了一些底层的 API，导致在基于内置模块进行项目开发的时，效率很低。

​	包是基于内置模块封装出来的，提供了更高级、更方便的 API，极大的提高了开发效率。

​	包和内置模块之间的关系，类似于 jQuery 和 浏览器内置 API 之间的关系。

##### 7.1.4 从哪里下载包

​	国外有一家 IT 公司，叫做 **npm, Inc.** 这家公司旗下有一个非常著名的网站： <https://www.npmjs.com/> ，它是**全球最大的包共享平台**，你可以从这个网站上搜索到任何你需要的包，只要你有足够的耐心！

​	到目前位置，全球约 1100 多万的开发人员，通过这个包共享平台，开发并共享了超过 120 多万个包 供我们使用。

​	**npm, Inc.** **公司**提供了一个地址为 <https://registry.npmjs.org/> 的服务器，来对外共享所有的包，我们可以从这个服务器上下载自己所需要的包。

**注意：**

- 从 <https://www.npmjs.com/> 网站上搜索自己所需要的包
- 从 <https://registry.npmjs.org/>  服务器上下载自己需要的包

##### 7.1.5 如何下载包

​	**npm, Inc.** **公司**提供了一个包管理工具，我们可以使用这个包管理工具，从 <https://registry.npmjs.org/> 服务器把需要的包下载到本地使用。

​	这个包管理工具的名字叫做 Node Package Manager（简称 npm 包管理工具），这个包管理工具随着 Node.js 的安装包一起被安装到了用户的电脑上。

​	大家可以在终端中执行 **npm -v** 命令，来查看自己电脑上所安装的 npm 包管理工具的版本号：

 ![](C:\资料备份\学习笔记\01-Web笔记\101-Node.js\images\2022-07-26_145249.png)

#### 7.2 npm初体验

##### 7.2.1 格式化时间的传统做法

​	①创建格式化时间的自定义模块

​	②定义格式化时间的方法

​	③创建补零函数

​	④从自定义模块中导出格式化时间的函数

​	⑤导入格式化时间的自定义模块

​	⑥调用格式化时间的函数

 ![](C:\资料备份\学习笔记\01-Web笔记\101-Node.js\images\2022-07-26_152250.png)

##### 7.2.2 格式化时间的高级做法

​	①使用 npm 包管理工具，在项目中安装格式化时间的包 moment

​	②使用 require() 导入格式化时间的包

​	③参考 moment 的官方 API 文档对时间进行格式化

 ![](C:\资料备份\学习笔记\01-Web笔记\101-Node.js\images\2022-07-26_193925.png)

##### 7.2.3 在项目中安装包的命令

如果想在项目中安装指定指定名称的包，需要运行如下的命令：

```
// npm init -y 初始化项目
npm install 包的完整名称
```

上述的装包命令，可以简写成如下格式：

```
npm i 完整的包名称
```

##### 7.2.4 初次装包后多了哪些文件

​	初次装包完成后，在项目文件夹下多一个叫做 node_modules 的文件夹和 package-lock.json 的配置文件。

其中：

​	node_modules 文件夹用来存放所有已安装到项目中的包。require() 导入第三方包时，就是从这个目录中查找并加载包。

​	package-lock.json 配置文件用来记录 node_modules 目录下的每一个包的下载信息，例如包的名字、版本号、下载地址等。

注意：

​	程序员不要手动修改 node_modules 或 package-lock.json 文件中的任何代码，npm 包管理工具会自动维护它们。

##### 7.2.5 安装指定版本的包

​	默认情况下，使用npm install 命令安装包的时候，会自动安装最新版本的包。如果需要安装指定版本的包，可以在包名之后，通过@符号指定具体的版本，例如：

```
npm i moment@2.22.2
```

##### 7.2.6 包的语义化版本规范

​	包的版本号是以“点分十进制”形式进行定义的，总共有三位数字，例如 **2.24.0**

其中每一位数字所代表的的含义如下：

​	第1位数字：大版本

​	第2位数字：功能版本

​	第3位数字：Bug修复版本

​	版本号提升的规则：只要前面的版本号增长了，则后面的版本号归零。

#### 7.3 包管理配置文件

​	npm 规定，在项目根目录中，**必须**提供一个叫做 package.json 的包管理配置文件。用来记录与项目有关的一些配置信息。例如：

- 项目的名称、版本号、描述等
- 项目中都用到了哪些包
- 哪些包只在开发期间会用到
- 那些包在开发和部署时都需要用到

##### 7.3.1 多人协作的问题

 ![](C:\资料备份\学习笔记\01-Web笔记\101-Node.js\images\2022-07-26_175946.png)

##### 7.3.2 如何记录项目中安装了哪些包

​	在项目根目录中，创建一个叫做 package.json 的配置文件，即可用来记录项目中安装了哪些包。从而方便剔除 node_modules 目录之后，在团队成员之间共享项目的源代码。

**注意**：今后在项目开发中，一定要把 node_modules 文件夹，添加到 .gitignore 忽略文件中。

##### 7.3.3 快速创建package.json

​	npm包管理工具提供了一个快捷命令，可以在执行命令时所处的目录中，快速创建package.json这个包管理。

配置文件：

```
// 作用：在执行命令所处的目录中，快速新建package.json文件
npm init -y
```

注意：

​	①上述命令只能在英文的目录下成功运行！所以，项目文件夹的名称一定要使用英文命名，不要使用中文，不能出现空格。

​	②运行 npm install 命令安装包的时候，npm 包管理工具会自动把包的名称和版本号，记录到 package.json 中。

##### 7.3.4 dependencies节点

package.json文件中，有一个dependencies节点，专门用来记录您使用npm install 命令安装了哪些包。

 ![](C:\资料备份\学习笔记\01-Web笔记\101-Node.js\images\2022-07-26_195155.png)

##### 7.3.5 一次性安装所有的包

当我们拿到一个剔除了node_modules的项目之后，需要先把所有的包下载到项目中，才能将项目运行起来。否则会报类似于下面的错误：

>Error: Cannot find module 'moment'

可以运行 npminstall 命令（或 npm i）一次性安装所有的依赖包：

>npm install

##### 7.3.6 卸载包

可以运行npm uninstall 命令，来卸载指定的包：

>npm uninstall moment

注意：npm uninstall 命令执行成功后，会把卸载的包，自动从package.json的 dependencies中移除掉。

##### 7.3.7 devDependencies节点

​	如果某些包**只在项目开发阶段**会用到，在**项目上线之后不会用到**，则建议把这些包记录到 devDependencies 节点中。

​	与之对应的，如果某些包在开发和项目上线之后都需要用到，则建议把这些包记录到 dependencies 节点中。

您可以使用如下的命令，将包记录到 devDependencies 节点中：

> npm i 包名 -D 	//安装指定的包，并记录到devDependencies节点中
>
> npm install 包名 --save-dev	//注意：（完整形式）等价于上述命令（简写形式）

#### 7.4 解决下包速度慢的问题

##### 7.4.1 为什么下包速度慢

​	在使用 npm 下包的时候，默认从国外的 <https://registry.npmjs.org/> 服务器进行下载，此时，网络数据的传输需要经过漫长的海底光缆，因此下包速度会很慢。

扩展阅读 - 海底光缆：

- <https://baike.baidu.com/item/%E6%B5%B7%E5%BA%95%E5%85%89%E7%BC%86/4107830>
- <https://baike.baidu.com/item/%E4%B8%AD%E7%BE%8E%E6%B5%B7%E5%BA%95%E5%85%89%E7%BC%86/10520363>
- <https://baike.baidu.com/item/APG/23647721?fr=aladdin>

##### 7.4.2 淘宝NPM镜像服务器

 ![](C:\资料备份\学习笔记\01-Web笔记\101-Node.js\images\2022-07-26_202051.png)

##### 7.4.3 切换npm的下包镜像源

下包的镜像源，指的就是下包的服务器地址。

```javascript
// 查看当前的下包镜像源
npm config get registry
// 将下包的镜像源切换为淘宝镜像源
npm config set registry=https://registry.npm.taobao.org/
// 检查镜像源是否下载成功
npm config get registry
```

##### 7.4.4 nrm

​	为了更方便的切换下包的镜像源，我们可以安装nrm这个小工具，利用nrm提供的终端命令，可以快速查看和切换下包的镜像源。

```javascript
// 通过npm包管理器，将nrm安装为全局可用的工具
npm i nrm -g
// 查看所有可用的镜像源
nrm ls
// 将下包的镜像源切换为taobao镜像
nrm use taobao
```

#### 7.5 包的分类

使用npm包管理工具下载的包，共分为两大类，分别是：

- 项目包

- 全局包

##### 7.5.1 项目包

那些被安装到项目的node_modules目录中的包，都是项目包。

项目包又分为两类，分别是：

- 开发依赖包（被记录到 devDependencies 节点中的包，只在开发期间会用到）
- 核心依赖包（被记录到 dependencies 节点中的包，在开发期间和项目上线之后都会用到）

> npm i 包名 -D	// 开发依赖包（会被记录到 devDependencies 节点下）
>
> npm i 包名 	    // 核心依赖包（会被记录到 dependencies 节点下）

##### 7.5.2 全局包

在执行 npm install 命令时，如果提供了 -g 参数，则会把包安装为全局包。

全局包会被安装到C:\Users\用户目录\AppData\Roaming\npm\node_modules目录下。

> npm i 包名 -g 	// 全局安装指定的包
>
> npm uninstall 包名 -g 	//卸载全局安装的包

注意：

​	①只有工具性质的包，才有全局安装的必要性。因为它们提供了好用的终端命令。

​	②判断某个包是否需要全局安装后才能使用，可以参考官方提供的使用说明即可。

##### 7.5.3 i5ting_toc

i5ting_toc 是一个可以把md文档转为html页面的小工具，使用步骤如下：

```javascipt
// 将i5ting_toc安装为全局包
npm install -g i5ting_toc
// 调用i5ting_toc,轻松实现md转html的功能
i5ting_toc -f 要转换的md文件路径 -o
```

#### 7.6 规范的包结构

​	在清楚了包的概念、以及如何下载和使用包之后，接下来，我们深入了解一下包的内部结构。

一个规范的包，它的组成结构，必须符合以下 3 点要求：

​	①包必须以单独的目录而存在

​	②包的顶级目录下要必须包含 package.json 这个包管理配置文件

​	③package.json 中必须包含 name，version，main 这三个属性，分别代表包的名字、版本号、包的入口。

注意：以上 3 点要求是一个规范的包结构必须遵守的格式，关于更多的约束，可以参考如下网址：

<https://yarnpkg.com/zh-Hans/docs/package-json>

#### 7.7 开发属于自己的包

##### 7.7.1 需要实现的功能

​	① 格式化日期

​	② 转义 HTML 中的特殊字符

​	③ 还原 HTML 中的特殊字符

##### 7.7.2 初始化包的基本结构

​	①新建 itheima-tools 文件夹，作为包的根目录

​	②在 itheima-tools 文件夹中，新建如下三个文件：

​		1.package.json （包管理配置文件）

​		2.index.js          （包的入口文件）

​		3.README.md  （包的说明文档）

##### 7.7.3 初始化package.json

> npm init -y	//初始化，命令在目录终端中执行

 ![](C:\资料备份\学习笔记\01-Web笔记\101-Node.js\images\2022-07-27_111725.png)

关于更多 license 许可协议相关的内容，可参考 <https://www.jianshu.com/p/86251523e898>

##### 7.7.4 在index.js中定义格式化时间的方法

```javascript
// 格式化时间的方法
function dateFormat(dateStr) {
    const dt = new Date(dateStr)

    const y = dt.getFullYear()
    const m = padZero(dt.getMonth() + 1)
    const d = padZero(dt.getDate())

    const hh = padZero(dt.getHours())
    const mm = padZero(dt.getMinutes())
    const ss = padZero(dt.getSeconds())

    return `${y}-${m}-${d} ${hh}:${mm}:${ss}`
}

// 补零的方法
function padZero(n) {
    return n > 9 ? n : '0' + n
}
```

##### 7.7.5 在index.js中定义转义HTML的方法

```javascript
// 定义转义HTML字符的函数
function htmlEscape(htmlstr){
    return htmlstr.replace(/<|>|"|&/g, match => {
        switch(match) {
            case '<' :
                return '&lt;'
            case '>' : 
                return '&gt;'
            case '"' : 
                return '&quot;'
            case '&' : 
                return '&amp;'
        }
    })
}
```

##### 7.7.6 在index.js中定义还原HTML的方法

```javascript
// 定义还原HTML字符串的函数
function htmlUnEscape(htmlstr) {
    return htmlstr.replace(/&lt;|&gt;|&quot;|&amp;/g, match => {
        switch(match) {
            case '&lt;':
                return '<'
              case '&gt;':
                return '>'
              case '&quot;':
                return '"'
              case '&amp;':
                return '&'
        }
    })
}
```

##### 7.7.7 将不同的功能进行模块化拆分

​	①将格式化时间的功能，拆分到 src -> dateFormat.js 中

​	②将处理 HTML 字符串的功能，拆分到 src -> htmlEscape.js 中

​	③在 index.js 中，导入两个模块，得到需要向外共享的方法

​	④在 index.js 中，使用 module.exports 把对应的方法共享出去

 ![](C:\资料备份\学习笔记\01-Web笔记\101-Node.js\images\2022-07-27_125749.png)

![](C:\资料备份\学习笔记\01-Web笔记\101-Node.js\images\2022-07-27_125926.png)

##### 7.7.8 编写包的说明文档

​	包根目录中的 README.md 文件，是包的使用说明文档。通过它，我们可以事先把包的使用说明，以 markdown 的格式写出来，方便用户参考。

​	README 文件中具体写什么内容，没有强制性的要求；只要能够清晰地把包的作用、用法、注意事项等描述清楚即可。

​	我们所创建的这个包的 README.md 文档中，会包含以下 6 项内容：

​	安装方式、导入方式、格式化时间、转义 HTML 中的特殊字符、还原 HTML 中的特殊字符、开源协议

~~~markdown
## 安装
```
npm install yrk-tools
```

## 导入
```js
const yrk = require('yrk-tools')
```

## 格式化时间
```js
// 调用 dateFormat 对时间进行格式化
const dtStr = yrk.dateFormat(new Date())
// 结果  2020-04-03 17:20:58
console.log(dtStr)
```

## 转义 HTML 中的特殊字符
```js
// 带转换的 HTML 字符串
const htmlStr = '<h1 title="abc">这是h1标签<span>123&nbsp;</span></h1>'
// 调用 htmlEscape 方法进行转换
const str = yrk.htmlEscape(htmlStr)
// 转换的结果 &lt;h1 title=&quot;abc&quot;&gt;这是h1标签&lt;span&gt;123&amp;nbsp;&lt;/span&gt;&lt;/h1&gt;
console.log(str)
```

## 还原 HTML 中的特殊字符
```js
// 待还原的 HTML 字符串
const str2 = yrk.htmlUnEscape(str)
// 输出的结果 <h1 title="abc">这是h1标签<span>123&nbsp;</span></h1>
console.log(str2)
```

## 开源协议
ISC
~~~

#### 7.8 发布包

##### 7.8.1 注册npm账号

​	①访问 <https://www.npmjs.com/> 网站，点击 sign up 按钮，进入注册用户界面

​	②填写账号相关的信息：Full Name、Public Email、Username、Password

​	③点击 Create an Account 按钮，注册账号

​	④登录邮箱，点击验证链接，进行账号的验证

##### 7.8.2 登录npm账号

​	npm 账号注册完成后，可以在终端中执行npm login 命令，依次输入用户名、密码、邮箱后，即可登录成功。

![](C:\资料备份\学习笔记\01-Web笔记\101-Node.js\images\2022-07-27_145546.png)

注意：

​	在运行 npm login 命令之前，必须先把下包的服务器地址切换为 npm 的官方服务器。否则会导致发布包失败！

##### 7.8.3  把包发布到npm上

> 将终端切换到包的根目录之后，运行 **npm publish** 命令，即可将包发布到npm上（注意：包名不能雷同）。

 ![](C:\资料备份\学习笔记\01-Web笔记\101-Node.js\images\2022-07-27_150611.png)

##### 7.8.4 删除已发布的包

> 运行 **npm unpublish 包名 --force**  命令，即可从npm删除已发布的包。

 ![](C:\资料备份\学习笔记\01-Web笔记\101-Node.js\images\2022-07-27_150626.png)

注意：

​	①npm unpublish 命令只能删除 72 小时以内发布的包

​	②npm unpublish 删除的包，在 24 小时内不允许重复发布

​	③发布包的时候要慎重，尽量不要往 npm 上发布没有意义的包！

### 8.模块的加载机制

#### 8.1 优先从缓存中加载

​	模块在第一次加载后会被缓存。这也意味着多次调用require() 不会导致模块的代码被执行多次。

​	注意：不论是内置模块、用户自定义模块、还是第三方模块，它们都会优先从缓存中加载，从而提高模块的加载效率。

#### 8.2 内置模块的加载机制

​	内置模块是由Node.js官方提供的模块，内置模块的加载优先级最高。

​	例如，require('fs')始终返回内置的fs模块，即使在node_modules目录下有名字相同的包也叫做fs。

#### 8.3 自定义模块的加载机制

​	使用 require() 加载自定义模块时，必须指定以 ./ 或 ../ 开头的路径标识符。在加载自定义模块时，如果没有指定 ./ 或 ../ 这样的路径标识符，则 node 会把它当作内置模块或第三方模块进行加载。

​	同时，在使用 require() 导入自定义模块时，如果省略了文件的扩展名，则 Node.js 会按顺序分别尝试加载以下的文件：

​	①按照确切的文件名进行加载

​	②补全 .js 扩展名进行加载

​	③补全 .json 扩展名进行加载

​	④补全 .node 扩展名进行加载

​	⑤加载失败，终端报错

#### 8.4 第三方模块的加载机制

​	如果传递给 require() 的模块标识符不是一个内置模块，也没有以 ‘./’ 或 ‘../’ 开头，则 Node.js 会从当前模块的父目录开始，尝试从 /node_modules 文件夹中加载第三方模块。

​	如果没有找到对应的第三方模块，则移动到再上一层父目录中，进行加载，直到文件系统的根目录。

​	例如，假设在 'C:\Users\itheima\project\foo.js' 文件里调用了 require('tools')，则 Node.js 会按以下顺序查找：

​	① C:\Users\itheima\project\node_modules\tools

​	② C:\Users\itheima\node_modules\tools

​	③ C:\Users\node_modules\tools

​	④ C:\node_modules\tools

#### 8.5 目录作为模块

​	当把目录作为模块标识符，传递给 require() 进行加载的时候，有三种加载方式：

​	①在被加载的目录下查找一个叫做 package.json 的文件，并寻找 main 属性，作为 require() 加载的入口

​	②如果目录里没有 package.json 文件，或者 main 入口不存在或无法解析，则 Node.js 将会试图加载目录下的 index.js 文件。

​	③如果以上两步都失败了，则 Node.js 会在终端打印错误消息，报告模块的缺失：Error: Cannot find module 'xxx'

### 9.初识Express

#### 9.1 Express简介

##### 9.1.1 什么是Express

​	官方给出的概念：Express 是基于 Node.js 平台，快速、开放、极简的 Web 开发框架。

​	通俗的理解：Express 的作用和 Node.js 内置的 http 模块类似，是专门用来创建 Web 服务器的。

​	**Express** **的本质**：就是一个 npm 上的第三方包，提供了快速创建 Web 服务器的便捷方法。

Express 的中文官网：[ http://www.expressjs.com.cn/](http://www.expressjs.com.cn/)

##### 9.1.2 进一步理解Express

思考：不使用 Express 能否创建 Web 服务器？

> 答案：能，使用 Node.js 提供的原生 http 模块即可。

思考：既生瑜何生亮（有了 http 内置模块，为什么还有用 Express）？

> 答案：http 内置模块用起来很复杂，开发效率低；Express 是基于内置的 http 模块进一步封装出来的，能够极大的提高开发效率。

思考：http 内置模块与 Express 是什么关系？

> 答案：类似于浏览器中 Web API 和 jQuery 的关系。后者是基于前者进一步封装出来的。

##### 9.1.3 Express能做什么

对于前端程序员来说，最常见的两种服务器，分别是：

- Web 网站服务器：专门对外提供 Web 网页资源的服务器。
- API 接口服务器：专门对外提供 API 接口的服务器。

使用 Express，我们可以方便、快速的创建 Web 网站的服务器或 API 接口的服务器。

#### 9.2 Express的基本使用

##### 9.2.1 安装

在项目所处的目录中，运行如下的终端命令，即可将express安装到项目中使用：

> npm i express@4.17.1

##### 9.2.2 创建基本的Web服务器

```js
// 1.导入express
const express = require('express')
// 2.创建web服务器
const app = express()

// 3.调用app.listen(端口号，启动成功后的回调函数)，启动服务器
app.listen(80, () => {
    console.log('express server running at http://127.0.0.1')
})
```

##### 9.2.3 监听GET请求

通过app.get()方法，可以监听客户端GET请求，具体的语法格式如下：

```javascript
// 参数1：给客户端请求的URL地址
// 参数2：请求对应的处理函数
		//req: 请求对象（包含了与请求相关的属性与方法）
		//res: 响应对象（包含了与响应相应的属性与方法）
app.get('请求URL', function(req, res) {/*处理函数*/})
```

##### 9.2.4 监听POST请求

通过app.post()方法，可以监听客户端POST请求，具体的语法格式如下：

```javascript
// 参数1：给客户端请求的URL地址
// 参数2：请求对应的处理函数
		//req: 请求对象（包含了与请求相关的属性与方法）
		//res: 响应对象（包含了与响应相应的属性与方法）
app.post('请求URL', function(req, res) {/*处理函数*/})
```

##### 9.2.5 把内容响应给客户端

通过res.send()方法，可以把处理好的内容，发送给客户端：

```javascript
const express = require('express')
const app = express()
app.get('', (req, res) => {
    // 向客户端发送JSON对象
    res.send({
        name: 'zs',
        age: 20,
        gender: '男'
    })
})
app.post('', (req, res) => {
    // 向客户端发送文本内容
    res.send('请求成功')
})
```

##### 9.2.6 获取URL中携带的查询参数

通过req.query对象，可以访问到客户端通过查询字符串的形式，发送到服务器的参数：

```javascript
app.get('/', (req, res) => {
    // req.qurery默认是一个空对象
    // 客户端使用?name=zs&age=20 这种查询字符串形式，发送到服务器的参数,
    // 可以通过req.query对象访问到，例如：
    // req.query.name req.query.age
    console.log(req.query)
})
```

##### 9.2.7 获取URL中的动态参数

通过req.params对象，可以访问到URL中，通过:匹配到的动态参数：

```javascript
// URL地址中，可以通过 :参数名 的形式，匹配动态参数值
app.get('/user/:id', (req, res) => {
    // req.params 默认是一个空对象
    // 里面存放着通过 : 动态匹配到的参数值
    console.log(req.params)
})
```

#### 9.3 托管静态资源

##### 9.3.1 express.static()

​	express提供了一个非常好用的函数，叫做express.static()，通过它，我们可以非常方便地创建一个静态资源服务器，例如，通过如下代码就可以将 public目录下的图片、CSS文件、JavaScript文件对外开放访问了：

> app.use(express.static('public'))

现在，你就可以访问public目录中的所有文件了：

​	http://localhost:3000/images/bg.jpg

​	http://localhost:3000/css/style.css

​	http://localhost:3000/js/login.js

**注意：**Express 在指定的静态目录中查找文件，并对外提供资源的访问路径。因此，存放静态文件的目录名不会出现在 URL 中。

##### 9.3.2 托管多个静态资源目录

如果要托管多个静态资源目录，请多次调用express.static()函数：

> app.use(express.static('public'))
>
> app.use(express.static('files'))

访问静态资源文件时，，express.static()函数会根据目录的添加顺序查找所需的文件。

##### 9.3.3 挂载路径前缀

如果希望在托管的静态资源访问路径之前，挂载路径前缀，则可以使用如下的方式：

> app.use('/public', express.static('public'))

现在，你就可以通过带有/public前缀地址来访问public目录中的文件了:

​	http://localhost:3000/public/images/kitten.jpg

​	http://localhost:3000/public/css/style.css

​	http://localhost:3000/public/js/app.js

#### 9.4 nodemon

##### 9.4.1 为什么要使用nodemon

​	在编写调试 Node.js 项目的时候，如果修改了项目的代码，则需要频繁的手动 close 掉，然后再重新启动，非常繁琐。

​	现在，我们可以使用 nodemon（<https://www.npmjs.com/package/nodemon>） 这个工具，它能够监听项目文件的变动，当代码被修改后，nodemon 会自动帮我们重启项目，极大方便了开发和调试。

##### 9.4.2 安装nodemon

在终端中，运行如下命令，即可将nodemon安装为全局可用的工具：

> npm install -g nodemon

##### 9.4.3 使用nodemon

​	当基于 Node.js 编写了一个网站应用的时候，传统的方式，是运行 node app.js 命令，来启动项目。这样做的坏处是：代码被修改之后，需要手动重启项目。

​	现在，我们可以将 node 命令替换为 nodemon 命令，使用 nodemon app.js 来启动项目。这样做的好处是：代码被修改之后，会被 nodemon 监听到，从而实现自动重启项目的效果。

```javascript
node app.js 
// 将上面的终端命令，替换为下面的终端命令，即可实现自动重启项目的效果
nodemon app.js
```

### 10.Express路由

#### 10.1 路由的概念

##### 10.1.1 什么是路由

​	广义上来讲，路由就是映射关系。

##### 10.1.2 现实生活中的路由

 ![](C:\资料备份\学习笔记\01-Web笔记\101-Node.js\images\2022-07-28_175454.png)

##### 10.1.3 Express 中的路由

在 Express 中，路由指的是客户端的请求与服务器处理函数之间的映射关系。

Express 中的路由分 3 部分组成，分别是请求的类型、请求的 URL 地址、处理函数，格式如下：

> app.METHOD(PATH, HANDLER)

##### 10.1.4 Express中的路由的例子

```javascript
// 匹配GET请求，且请求URL为/
app.get('/', function(req, res) {
    res.send('Hello World!')
})

// 匹配POST请求，且请求URL为/
app.post('/', function(req, res) {
    res.send('Got a POST request')
})
```

##### 10.1.5 路由的匹配过程

​	每当一个请求到达服务器之后，需要先经过路由的匹配，只有匹配成功之后，才会调用对应的处理函数。

​	在匹配时，会按照路由的顺序进行匹配，如果请求类型和请求的 URL 同时匹配成功，则 Express 会将这次请求，转交给对应的 function 函数进行处理。

 ![](C:\资料备份\学习笔记\01-Web笔记\101-Node.js\images\2022-07-28_180222.png)

#### 10.2 路由的使用

##### 10.2.1 最简单的用法

在Express中使用路由最简单的方式，就是把路由挂载到app上，示例代码如下：

```javascript
const express = require('express')
// 创建Web服务器，命名为app
const app = express()

// 挂载路由
app.get('/', (req, res) => {
    res.send('Hello World')
})
app.post('/', (req, res) => {
    res.send('Post Request')
})

// 启动Web服务器
app.listen(80, () => {
    console.log('server running at http://127.0.0.1')
})
```

##### 10.2.2 模块化路由

​	为了方便对路由进行模块化的管理，Express **不建议**将路由直接挂载到 app 上，而是推荐将路由抽离为单独的模块。

将路由抽离为单独模块的步骤如下：

​	①创建路由模块对应的 .js 文件

​	②调用 express.Router() 函数创建路由对象

​	③向路由对象上挂载具体的路由

​	④使用 module.exports 向外共享路由对象

​	⑤使用 app.use() 函数注册路由模块

##### 10.2.3 创建路由模块

```javascript
const express = require('express') // 1.导入express
const router = express.Router() // 2.创建路由对象
router.get('/user/list', (req, res) => { // 3.挂载获取用户列表的路由
    res.send('Get user list')
})
router.post('/user/add', (req, res) => { // 4.挂载添加用户的路由
    res.send('Post user add')
})

module.exports = router // 5.向外导出路由对象
```

##### 10.2.4 注册路由模块

```javascript
const userRouter = require('./router/user.js') // 1.导入路由模块
app.use(userRouter) // 2.使用app.use()注册路由模块
```

##### 10.2.5 为路由模块添加前缀

类似于托管静态资源时，为静态资源统一挂载访问前缀一样，路由模块添加前缀的方式也非常简单：

```javascript
// 1.导入路由模块
const userRouter = require('./router/user.js')

// 2.使用app.use()注册路由模块，并添加统一的访问前缀/api
app.use('/api', userRouter)
```

### 11.Express中间件

#### 11.1 中间件的概念

##### 11.1.1 什么是中间件

中间件（Middleware），特指业务流程的中间处理环节。

##### 11.1.2 现实生活中的例子

 ![](C:\资料备份\学习笔记\01-Web笔记\101-Node.js\images\2022-07-29_085354.png)

##### 11.1.3 Express中间件的调用流程

当一个请求到达Express的服务器之后，可以连续调用多个中间件，从而对这次请求进行预处理。

 ![](C:\资料备份\学习笔记\01-Web笔记\101-Node.js\images\2022-07-29_085558.png)

##### 11.1.4 Express中间件的格式

Express的中间件，本质上就是一个function处理函数，Express中间件的格式如下：

 ![](C:\资料备份\学习笔记\01-Web笔记\101-Node.js\images\2022-07-29_085907.png)

注意： 中间件函数的形参列表中，必须包含next参数。而路由处理函数中只包含req和res。

##### 11.1.5 next函数的作用

next函数是实现多个中间件连续调用的关键，它表示把流转关系转交给下一个中间件或路由。

 ![](C:\资料备份\学习笔记\01-Web笔记\101-Node.js\images\2022-07-29_090100.png)

##### 11.2.1 定义中间件函数

可以通过如下的方式，定义一个最简单的中间件函数：

```javascript
// 常量mw所指向的，就是一个中间件函数
const mw = function(req, res, next) {
    console.log('这是一个最简单的中间件函数')
    // 注意： 在当前中间件的业务处理完毕后，必须调用next()函数
    // 表示把流转关系转交给下一个中间件或路由
    next()
}
```

##### 11.2.2 全局生效的中间件

客户端发起的任何请求，到达服务器之后，都会触发的中间件，叫做全局生效的中间件。

通过调用 app.use(中间件函数)，即可定义一个全局生效的中间件，示例代码如下：

```javascript
// 常量mw所指向的，就是一个中间件函数
const mw = function(req, res, next){
    console.log('这是一个最简单的中间件函数')
	next()
}

// 全局生效的中间件
app.use(mw)
```

##### 11.2.3 定义全局中间件的简化形式

```javascript
// 全局生效的中间件
app.use(function (req, res, next){
    console.log('这是一个最简单的中间件函数')
    next()
})
```

##### 11.2.4 中间件的作用

​	多个中间件之间，**共享同一份** **req** **和** **res**。基于这样的特性，我们可以在上游的中间件中，统一为req或res对象添加自定义的属性或方法，供下游的中间件或路由进行使用。

 ![](C:\资料备份\学习笔记\01-Web笔记\101-Node.js\images\2022-07-29_091310.png)

##### 11.2.5 定义多个全局中间件

​	可以使用app.use()连续定义多个全局中间件。客户端请求到达服务器之后，会按照中间件定义的先后顺序依次进行调用，示例代码如下：

```javascript
app.use(function(req, res, next()) {
    console.log('调用了第1个全局中间件')
    next()
})
app.use(function(req, res, next()) {
    console.log('调用了第2个全局中间件')
    next()
})
app.get('/user', (req, res) => {	// 请求这个路由会依次触发上述两个全局中间件
    res.send('Home page.')
})
```

##### 11.2.6 局部生效的中间件

不使用app.use()定义的中间件，叫做局部生效的中间件，示例代码如下：

```javascript
// 定义中间件函数 mw
const mw = function(req, res, next){
    console.log('这是中间件函数')
    next()
}
// mw这个中间件只在“当前路由中生效”，这种用法属于“局部生效的中间件”
app.get('/', mw, function(req, res) {
    res.send('Home page.')
})
// mw这个中间件不会影响下面这个路由
app.get('/user', function(req, res) {
    res.send('User page')
})
```

##### 11.2.7 定义多个局部中间件

可以在路由中，通过如下两种等价的方式，使用多个局部中间件

```javascript
// 以下两种写法是“完全等价”的，可根据自己的喜好，选择任意一种方式进行使用
app.get('/', mw1, mw2 (req, res) => {
	res.send('Home page.')
})
app.get('/', [mw1, mw2], (req, res) => {
    res.send('Home page')
})
```

##### 11.2.8 了解中间件的5个使用注意事项

​	①一定要在路由之前注册中间件

​	②客户端发送过来的请求，可以连续调用多个中间件进行处理

​	③执行完中间件的业务代码之后，不要忘记调用 next() 函数

​	④为了防止代码逻辑混乱，调用 next() 函数后不要再写额外的代码

​	⑤连续调用多个中间件时，多个中间件之间，共享 req 和 res 对象

##### 11.3 中间件的分类

为了方便大家理解和记忆中间件的使用，Express官方把常见的中间件用法，分成了5大类，分别是：

​	① 应用级别的中间件

​	② 路由级别的中间件

​	③ 错误级别的中间件

​	④ Express 内置的中间件

​	⑤ 第三方的中间件

##### 11.3.1 应用级别的中间件

通过app.use() 或 app.get() 或 app.post() ，绑定到app实例上的中间件，叫做应用级别的中间件，代码示例如下：

```javascript
// 应用级别的中间件（全局中间件）
app.use(req, res, next) {
    next()
}
// 应用级别的中间件（局部中间件）
app.get('/', mw, {
    res.send('Home page.')
})
```

##### 11.3.2 路由级别的中间件

​	绑定到express.Router() 实例上的中间件，叫做路由级别的中间件。它的用法和应用级别中间件没有任何区别。只不过，应用级别中间件是绑定到 app实例上，路由级别中间件绑定到 router实例上，代码示例如下：

```javascript
const app = express()
var router = express.Router()

// 路由级别的中间件
router.use(function(req, res, next) {
    console.log('Time:', Date.now())
    next()
})

app.use('/', router)
```

##### 11.3.3 错误级别的中间件

错误级别中间件的**作用**：专门用来捕获整个项目中发生的异常错误，从而防止项目异常崩溃的问题。

**格式**：错误级别中间件的function处理函数中，必须有 4 个形参，形参顺序从前到后，分别是(err,req, res, next)。

```javascript
app.get('/', function(req, res) {			// 1.路由
    throw new Error('服务器内部发生了错误！')·  // 1.1抛出一个自定义的错误
    res.send('Home Page.')
})
app.use(function(err, req, res, next) {		// 2.错误级别的中间件
    console.log('发生了错误' + err.message)	 // 2.1在服务器打印错误消息
    res.send('Error!' + err.message)		// 2.2向客户端响应错误相关的内容
})
```

**注意：**错误级别的中间件，必须注册在所有路由之后！

##### 11.3.4 Express 内置的中间件

​	自 Express 4.16.0 版本开始，Express 内置了 3 个常用的中间件，极大的提高了 Express 项目的开发效率和体验：

​	① express.static 快速托管静态资源的内置中间件，例如： HTML 文件、图片、CSS 样式等（无兼容性）

​	② express.json 解析 JSON 格式的请求体数据（有兼容性，仅在 4.16.0+ 版本中可用）

​	③ express.urlencoded 解析 URL-encoded 格式的请求体数据（有兼容性，仅在 4.16.0+ 版本中可用）

```javascript
// 配置解析application/json 格式数据的内置中间件
app.use(express.json())
// 配置解析application/x-www-form-urlencoded格式数据的内置中间件
app.use(express.urlencoded({extended: false}))
```

##### 11.3.5 第三方的中间件

​	非Express官方内置的，而是由第三方开发出来的中间件，叫做第三方中间件。在项目中，大家可以按需下载并配置第三方中间件，从而提高项目的开发效率。

例如：在 express@4.16.0之前的版本中，经常使用body-parser这个第三方中间件，来解析请求体数据。使用步骤如下：

​	①运行 npm install body-parser 安装中间件

​	②使用 require 导入中间件

​	③调用 app.use() 注册并使用中间件

注意：Express 内置的express.urlencoded中间件，就是基于body-parser这个第三方中间件进一步封装出来的

#### 11.4 自定义中间件

##### 11.4.1 需求描述与实现步骤

自己手动模拟一个类似于express.urlencoded这样的中间件，来解析POST提交到服务器的表单数据。

实现步骤：

①定义中间件

> 使用 app.use()来定义全局生效的中间件

②监听 req 的 data 事件

> 在中间件中，需要监听 req 对象的 data 事件，来获取客户端发送到服务器的数据。
>
> 如果数据量比较大，无法一次性发送完毕，则客户端会把数据切割后，分批发送到服务器。所以 data 事件可能会触发多次，每一次触发 data 事件时，获取到数据只是完整数据的一部分，需要手动对接收到的数据进行拼接。

③监听 req 的 end 事件

> 当请求体数据接收完毕之后，会自动触发 req 的 end 事件。
>
> 因此，我们可以在 req 的 end 事件中，拿到并处理完整的请求体数据。

④使用 querystring 模块解析请求体数据

> Node.js内置了一个querystring模块，专门用来处理查询字符串。通过这个模块提供的 parse() 函数，可以轻松把查询字符串，解析成对象的格式。

⑤将解析出来的数据对象挂载为 req.body

> 上游的中间件和下游的中间件及路由之间，**共享同一份** **req** **和** **res**。因此，我们可以将解析出来的数据，挂载为req的自定义属性，命名为req.body，供下游使用。

```javascript
// 导入 express 模块
const express = require('express')
// 创建 express 的服务器实例
const app = express()
// 导入 Node.js 内置的 querystring 模块
const qs = require('querystring')

// 1. 这是解析表单数据的中间件
app.use((req, res, next) => {
  // 定义中间件具体的业务逻辑
  // 定义一个 str 字符串，专门用来存储客户端发送过来的请求体数据
  let str = ''
  // 2. 监听 req 的 data 事件
  req.on('data', (chunk) => {
    str += chunk
  })
  // 3. 监听 req 的 end 事件
  req.on('end', () => {
    // 在 str 中存放的是完整的请求体数据
    // console.log(str)
    // TODO: 把字符串格式的请求体数据，解析成对象格式
    const body = qs.parse(str)
    req.body = body
    next()
  })
})

app.post('/user', (req, res) => {
  res.send(req.body)
})

// 调用 app.listen 方法，指定端口号并启动web服务器
app.listen(80, function () {
  console.log('Express server running at http://127.0.0.1')
})

```

⑥将自定义中间件封装为模块

>  为了优化代码的结构，我们可以把自定义的中间件函数，封装为独立的模块，示例代码如下：

```javascript
// custom-body-parser.js 模块中的代码
// 导入 Node.js 内置的 querystring 模块
const qs = require('querystring')

const bodyParser = (req, res, next) => {
  // 定义中间件具体的业务逻辑
  // 1. 定义一个 str 字符串，专门用来存储客户端发送过来的请求体数据
  let str = ''
  // 2. 监听 req 的 data 事件
  req.on('data', (chunk) => {
    str += chunk
  })
  // 3. 监听 req 的 end 事件
  req.on('end', () => {
    // 在 str 中存放的是完整的请求体数据
    // console.log(str)
    // TODO: 把字符串格式的请求体数据，解析成对象格式
    const body = qs.parse(str)
    req.body = body
    next()
  })
}

module.exports = bodyParser
```

```javascript
// 导入 express 模块
const express = require('express')
// 创建 express 的服务器实例
const app = express()

// 1. 导入自己封装的中间件模块
const customBodyParser = require('./14.custom-body-parser')
// 2. 将自定义的中间件函数，注册为全局可用的中间件
app.use(customBodyParser)

app.post('/user', (req, res) => {
  res.send(req.body)
})

// 调用 app.listen 方法，指定端口号并启动web服务器
app.listen(80, function () {
  console.log('Express server running at http://127.0.0.1')
})
```

### 12.使用Express写接口

#### 12.1 创建基本的服务器

**app.js**

```javascript
// 导入express模块
const express = require('express')
// 创建express的服务器实例
const app = express()

// write your code here...
// [导入并注册路由模板]
const apiRouter = require('./apiRouter')
app.use('/api', apiRouter)	

// 调用app.listen方法，指定端口号并启动web服务器
app.listen(80, () => {
    console.log('Express server running at http://127.0.0.1:80')
})
```

**apiRouter.js [路由模块]**

```javascript
const express = require('express')
const apiRouter = express.Router()

// bind you router here...
// [编写GET接口]
apiRouter.get('/get', (req, res) => {
    // 1.获取到客户端通过查询字符串，发送到服务器
    const query = res.query
    res.send({
        status: 0,
        msg: 'GET请求成功',
        data: query
    })
})
// [编写POST接口]
apiRouter.post('/post', (req, res) => {
    // 2.获取到客户端通过请求体，发送到服务器的URL-encoded数据
    const body =req.body
    res.send({
        status: 0,
        msg: 'POST请求成功',
        data: body
    })
})
module.exports = apiRouter	// 此处不要画蛇添足加上{}
```

#### 12.2 CORS跨域资源共享

##### 12.2.1 接口的跨域问题

刚才编写的 GET 和 POST接口，存在一个很严重的问题：不支持跨域请求。

解决接口跨域问题的方案主要有两种：

​	① CORS（主流的解决方案，推荐使用）

​	② JSONP（有缺陷的解决方案：只支持 GET 请求）

##### 12.2.2 使用cors中间件解决跨域问题

cors 是 Express 的一个第三方中间件。通过安装和配置 cors 中间件，可以很方便地解决跨域问题。

使用步骤分为如下 3 步：

​	①运行 npm install cors 安装中间件

​	②使用 const cors = require('cors') 导入中间件

​	③在路由之前调用 app.use(cors()) 配置中间件

##### 12.2.3 什么是CORS

​	CORS （Cross-Origin Resource Sharing，跨域资源共享）由一系列 HTTP 响应头组成，这些 HTTP 响应头决定浏览器是否阻止前端 JS 代码跨域获取资源。

​	浏览器的同源安全策略默认会阻止网页“跨域”获取资源。但如果接口服务器配置了 CORS 相关的 HTTP 响应头，就可以解除浏览器端的跨域访问限制。

 ![](C:\资料备份\学习笔记\01-Web笔记\101-Node.js\images\2022-07-29_154321.png)

##### 12.2.4 CORS的注意事项

​	①CORS 主要在服务器端进行配置。客户端浏览器**无须做任何额外的配置**，即可请求开启了 CORS 的接口。

​	②CORS 在浏览器中有兼容性。只有支持 XMLHttpRequest Level2 的浏览器，才能正常访问开启了 CORS 的服务端接口（例如：IE10+、Chrome4+、FireFox3.5+）。

##### 12.2.5 CORS响应头部 - Access-Control-Allow-Origin

响应头部中可以携带一个Access-Control-Allow-Origin字段，其语法如下：

> Access-Control-Allow-Origin: <origin> | *

其中，origin 参数的值指定了允许访问该资源的外域 URL。

例如，下面的字段值将只允许来自 http://itcast.cn 的请求：

> res.setHeader('Access-Control-Allow-Origin',  'http://itcast.cn')

如果指定了Access-Control-Allow-Origin字段的值为通配符*，表示允许来自任何域的请求，示例代码如下：

> res.setHeader('Access-Control-Allow-Origin', '*')

##### 12.2.6 CORS响应头部 - Access-Control-Allow-Headers

默认情况下，CORS 仅支持客户端向服务器发送如下的 9 个请求头：

​	Accept、Accept-Language、Content-Language、DPR、Downlink、Save-Data、Viewport-Width、Width 、Content-Type （值仅限于 text/plain、multipart/form-data、application/x-www-form-urlencoded 三者之一）

​	如果客户端向服务器发送了额外的请求头信息，则需要在服务器端，通过 Access-Control-Allow-Headers 对额外的请求头进行声明，否则这次请求会失败！

```javascript
// 允许客户端额外向服务器发送Content-Type请求头和X-Custom-Header请求头
// 注意：多个请求头之间使用英文的逗号进行分割
res.setHeader('Access-Control-Allow-Headers', 'Content-Type, X-Custom-Header')
```

##### 12.2.7 CORS响应头部 - Access-Control-Allow-Methods

默认情况下，CORS 仅支持客户端发起 GET、POST、HEAD 请求。

​	如果客户端希望通过 PUT、DELETE 等方式请求服务器的资源，则需要在服务器端，通过 Access-Control-Alow-Methods来指明实际请求所允许使用的 HTTP 方法。

示例代码如下：

```javascript
// 只允许 POST|GET|DELETE|HEAD 请求方法
res.setHeader('Access-Control-Allow-Methods', 'POST, GET, DELETE, HEAD')
// 允许所有的HTTP请求方法
res.setHeader('Access-Control-Allow-Methods', '*')
```

##### 12.2.8 CORS请求的分类

客户端在请求 CORS 接口时，根据请求方式和请求头的不同，可以将 CORS 的请求分为两大类，分别是：

①简单请求

②预检请求

##### 12.2.9 简单请求

同时满足以下两大条件的请求，就属于简单请求：

① 请求方式：GET、POST、HEAD 三者之一

② HTTP 头部信息不超过以下几种字段：无自定义头部字段、Accept、Accept-Language、Content-Language、DPR、Downlink、Save-Data、Viewport-Width、Width 、Content-Type（只有三个值application/x-www-form-urlencoded、multipart/form-data、text/plain）

##### 12.2.10 预检请求

只要符合以下任何一个条件的请求，都需要进行预检请求：

① 请求方式为 GET、POST、HEAD 之外的请求 Method 类型

② 请求头中包含自定义头部字段

③ 向服务器发送了 application/json 格式的数据

​	在浏览器与服务器正式通信之前，浏览器会先发送 OPTION 请求进行预检，以获知服务器是否允许该实际请求，所以这一次的 OPTION 请求称为“预检请求”。服务器成功响应预检请求后，才会发送真正的请求，并且携带真实数据。

##### 12.2.11 简单请求和预检请求的区别

简单请求的特点：客户端与服务器之间只会发生一次请求。

预检请求的特点：客户端与服务器之间会发生两次请求，OPTION 预检请求成功之后，才会发起真正的请求。

#### 12.3 JSONP接口 

##### 12.3.1 回顾JSONP的概念与特点

​	概念：浏览器端通过 <script> 标签的 src 属性，请求服务器上的数据，同时，服务器返回一个函数的调用。这种请求数据的方式叫做 JSONP。

特点：

​	①JSONP 不属于真正的 Ajax 请求，因为它没有使用 XMLHttpRequest 这个对象。

​	②JSONP 仅支持 GET 请求，不支持 POST、PUT、DELETE 等请求。

##### 12.3.2 创建JSONP接口的注意事项

​	如果项目中已经配置了 CORS 跨域资源共享，为了**防止冲突**，必须在配置 CORS 中间件之前声明 JSONP 的接口。否则JSONP接口会被处理成开启了CORS的接口。示例代码如下：

```javascript
// 优先创建JSONP接口【这个接口不会被处理成CORS接口】
app.get('/api/jsonp', (req, res) => {})

// 再配置CORS中间件【后续的所有接口，都会被处理成CORS接口】
app.use(cors())

// 这是一个开启了CORS的接口
app.get('/api/get', (req, res) => {})
```

##### 12.3.3 实现JSONP接口的步骤

①获取客户端发送过来的回调函数的名字

②得到要通过 JSONP 形式发送给客户端的数据

③根据前两步得到的数据，拼接出一个函数调用的字符串

④把上一步拼接得到的字符串，响应给客户端的 <script> 标签进行解析执行

```javascript
// 导入 express
const express = require('express')
// 创建服务器实例
const app = express()

// 配置解析表单数据的中间件
app.use(express.urlencoded({ extended: false }))

// 必须在配置 cors 中间件之前，配置 JSONP 的接口
app.get('/api/jsonp', (req, res) => {
  // TODO: 定义 JSONP 接口具体的实现过程
  // 1. 得到函数的名称
  const funcName = req.query.callback
  // 2. 定义要发送到客户端的数据对象
  const data = { name: 'zs', age: 22 }
  // 3. 拼接出一个函数的调用
  const scriptStr = `${funcName}(${JSON.stringify(data)})`
  // 4. 把拼接的字符串，响应给客户端
  res.send(scriptStr)
})

// 一定要在路由之前，配置 cors 这个中间件，从而解决接口跨域的问题
const cors = require('cors')
app.use(cors())

// 导入路由模块
const router = require('./apiRouter')
// 把路由模块，注册到 app 上
app.use('/api', router)

// 启动服务器
app.listen(800, () => {
  console.log('express server running at http://127.0.0.1')
})
```

在网页中使用jQuery发起JSONP请求，调用$.ajax()函数，提供 JSONP 的配置选项，从而发起JSONP请求，示例代码如下：

```javascript
// 4. 为 JSONP 按钮绑定点击事件处理函数
$('#btnJSONP').on('click', function () {
    $.ajax({
        type: 'GET',
        url: 'http://127.0.0.1/api/jsonp',
        dataType: 'jsonp',
        success: function (res) {
            console.log(res)
        },
    })
})
```

apiRouter.js文件

```javascript
const express = require('express')
const router = express.Router()

router.get('/get', (req, res) => {
    const query = req.query
    
    res.send({
        status: 0,
        msg: 'Get 请求成功',
        date: query
    })
})

router.post('/post', (req, res) => {
    const body = req.body

    res.send({
        status: 0,
        msg: 'Post 请求成功',
        date: body
    })

})

router.delete('/delete', (req, res) => {
    res.send({
        status: 0,
        msg: 'Delete请求成功'
    })
})

module.exports = router
```

### 13.数据库的基本概念

#### 13.1 什么是数据库

数据库（database）是用来组织、存储和管理数据的仓库。

​	当今世界是一个充满着数据的互联网世界，充斥着大量的数据。数据的来源有很多，比如出行记录、消费记录、浏览的网页、发送的消息等等。除了文本类型的数据，图像、音乐、声音都是数据。

​	为了方便管理互联网世界中的数据，就有了数据库管理系统的概念（简称：数据库）。用户可以对数据库中的数据进行新增、查询、更新、删除等操作。

#### 13.2 常见的数据库及分类

市面上的数据库有很多种，最常见的数据库有如下几个：

- MySQL 数据库（目前使用最广泛、流行度最高的开源免费数据库；Community + Enterprise）
- Oracle 数据库（收费）
- SQL Server 数据库（收费）
- Mongodb 数据库（Community + Enterprise）

​	其中，MySQL、Oracle、SQL Server 属于**传统型数据库**（又叫做：关系型数据库 或 SQL 数据库），这三者的设计理念相同，用法比较类似。

​	而 Mongodb 属于**新型数据库**（又叫做：非关系型数据库 或 NoSQL 数据库），它在一定程度上弥补了传统型数据库的缺陷。

#### 13.3 传统型数据库的数据组织结构

数据的组织结构：指的就是数据以什么样的结构进行存储。

 ![](C:\资料备份\学习笔记\01-Web笔记\101-Node.js\images\2022-08-01_114402.png)

##### 13.3.1 Excel的数据组织结构

 ![](C:\资料备份\学习笔记\01-Web笔记\101-Node.js\images\2022-08-01_114700.png)

##### 13.3.2 传统型数据库的数据组织结构

 ![](C:\资料备份\学习笔记\01-Web笔记\101-Node.js\images\2022-08-01_115155.png)

##### 13.3.3 实际开发中库、表、行、字段的关系

​	①在实际项目开发中，一般情况下，每个项目都对应独立的数据库。

​	②不同的数据，要存储到数据库的不同表中，例如：用户数据存储到 users 表中，图书数据存储到 books 表中。

​	③每个表中具体存储哪些信息，由字段来决定，例如：我们可以为 users 表设计 id、username、password 这 3 个字段。

​	④表中的行，代表每一条具体的数据。

### 14.安装并配置MySQL

#### 14.1 了解需要安装哪些MySQL相关的软件

对于开发人员来说，只需要安装 MySQL Server 和 MySQL Workbench 这两个软件，就能满足开发的需要了。

- MySQL Server：专门用来提供数据存储和服务的软件。
- MySQL Workbench：可视化的 MySQL 管理工具，通过它，可以方便的操作存储在 MySQL Server 中的数据。

#### 14.2 MySQL在Mac环境下的安装

在 Mac 环境下安装 MySQL 的过程比 Windows 环境下的步骤简单很多：

①先运行 **mysql-8.0.19-macos10.15-x86_64.dmg** 这个安装包，将 MySQL Server 安装到 Mac 系统

②再运行 **mysql-workbench-community-8.0.19-macos-x86_64.dmg** 这个安装包，将可视化的 MySQL Workbench 工具安装到 Mac 系统

具体的安装教程，可以参考 素材-> MySQL for Mac ->安装教程 - Mac系统安装MySql -> README.md

#### 14.3 MySQL在Windows环境下的安装

在 Windows 环境下安装 MySQL，只需要运行 **mysql-installer-community-8.0.19.0.msi** 这个安装包，就能一次性将 MySQL Server  和 MySQL Workbench 安装到自己的电脑上。

具体的安装教程，可以参考 素材 -> MySQL for Windows ->安装教程 - Windows系统安装MySql -> README.md 

### 15.MySQL的基本使用

#### 15.1 使用MySQL Workbench 管理数据库

##### 15.1.1 连接数据库

 ![](C:\资料备份\学习笔记\01-Web笔记\101-Node.js\images\2022-08-01_123302.png)

##### 15.1.2 了解主界面的组成部分

 ![](C:\资料备份\学习笔记\01-Web笔记\101-Node.js\images\2022-08-01_123520.png)

#### 15.2 使用SQL管理数据库

##### 15.2.1 什么是SQL

​	SQL（英文全称：Structured Query Language）是结构化查询语言，专门用来访问和处理数据库的编程语言。能够让我们**以编程的形式**，**操作数据库里面的数据**。

三个关键点：

​	①SQL 是一门数据库编程语言

​	②使用 SQL 语言编写出来的代码，叫做 SQL 语句

​	③SQL 语言只能在关系型数据库中使用（例如 MySQL、Oracle、SQL Server）。非关系型数据库（例如 Mongodb）不支持 SQL 语言

##### 15.2.2 SQL能做什么

​	① 从数据库中查询数据

​	② 向数据库中插入新的数据

​	③ 更新数据库中的数据

​	④ 从数据库删除数据

​	⑤ 可以创建新数据库

​	⑥ 可在数据库中创建新表

​	⑦ 可在数据库中创建存储过程、视图

​	⑧ etc…

### 16.在项目中操作MySQL

#### 16.1 在项目中操作数据库的步骤

​	①安装操作 MySQL 数据库的第三方模块（mysql）

​	②通过 mysql 模块连接到 MySQL 数据库

​	③通过 mysql 模块执行 SQL 语句

 ![](C:\资料备份\学习笔记\01-Web笔记\101-Node.js\images\2022-08-01_125328.png)

#### 16.2 安装与配置mysql模块

##### 16.2.1 安装mysql模块

​	mysql 模块是托管于 npm 上的第三方模块。它提供了在 Node.js 项目中连接和操作 MySQL 数据库的能力。

​	想要在项目中使用它，需要先运行如下命令，将 mysql 安装为项目的依赖包：

> npm install mysql

##### 16.2.2 配置mysql模块

​	在使用mysql模块操作MySQL数据库之前，必须先对mysql模块进行必要的配置，主要的配置步骤如下：

```javascript
// 1.导入mysql模块
const mysql = require('mysql')
// 2.建立与MySQL数据库的连接
const db = mysql.createPool({
    host: '127.0.0.1',		// 数据库的IP地址
    user: 'root',			// 登录数据库的账号
    password: 'root',   // 登录数据库的密码
    database: 'test'    // 指定要操作哪个数据库
})
```

##### 16.2.3 测试mysql模块能否正常工作

调用db.query()函数，指定要执行的SQL语句，通过回调函数拿到执行的结果：

```javascript
// 检测mysql模块能否正常工作
db.query('select 1', (err, results) => {
    if(err) return console.log(err.message)
    // 只要能打印出 [ RowDataPacket { '1': 1 } ] 的结果，就证明数据库连接正常
    console.log(results)
})
```

#### 16.3 使用mysql模块操作MySQL数据库

##### 16.3.1 查询数据

查询users表中所有的数据：

```javascript
// 查询users表中所有的用户数据
db.query('select * from users', (err, results) => {
    // 查询失败
    if (err) return console.log(err.message)
    // 查询成功
    console.log(results)
})
```

##### 16.3.2 插入数据

向users表中新增数据，其中username为yrk，password为123456，示例代码如下：

```javascript
// 1.要插入到users表中的数据对象
const user = {
    username: 'yrk',
    password: '123456'
}
// 2.待执行的SQL语句，其中英文的?表示占位符
const sqlStr = 'insert into users (username, password) values (?, ?)'

// 3.使用数组的形式，依次为?占位符指定具体的值
db.query(sqlStr, [user.username, user.password], (err, results) => {
    if (err) return console.log(err.message)	//失败
    // 注意：如果执行的是 insert into 插入语句，则 results 是一个对象可以通过 affectedRows属性，来判断是否插入数据成功
    if (results.affectedRows === 1) {
        console.log('插入数据成功')	//成功
    }
})
```

##### 16.3.3 插入数据的便携方式

向表中新增数据时，如果数据对象的每个属性和数据表的字段一一对应，则可以通过如下方式快速插入数据：

```javascript
const user = {
    username: 'yyy',
    password: '654321'
}
const sqlStr = 'insert into users set ?'
db.query(sqlStr, user, (err, results) => {
    if (err) return console.log(err.message)
    if (results.affectedRows === 1) {
        console.log('插入数据成功')
    }
})
```

##### 16.3.4 更新数据

可以通过如下方式，更新表中的数据：

```javascript
// 1.要更新的数据对象
const user = {
    id: 6,
    username: 'aaa',
    password: '000'	
}
// 2.要执行的SQL语句
const sqlStr = 'update users set username = ?, password = ? where id = ?'
// 3.调用db.query()执行SQL语句的同时，使用数组依次为占位符指定具体的值
db.query(sqlStr, [user.username, user.password, user.id], (err, results) => {
    if (err) return console.log(err.message)	// 失败
    if (results.affectedRows === 1) {
        console.log('更新数据成功')	// 成功
    }
})
```

##### 16.3.5 更新数据的便捷方式

更新表数据时，如果数据对象的每个属性和数据表的字段一一对应，则可以通过如下方式快速更新表数据：

```javascript
const user = {
    id: 6,
    username: 'bbb',
    password: '111'
}
const sqlStr = 'update users set ? where id = ?'
db.query(sqlStr, [user, user.id], (err, resulst) => {
    if (err) return console.log(err.message)
    if (resulst.affectedRows === 1) {
        console.log('更新数据成功')
    }
})
```

##### 16.3.6 删除数据

在删除数据时，推荐根据id这样的唯一标识，来删除对应的数据。示例如下：

```javascript
// 1.要执行的SQL语句
const sqlStr = 'delete from users where id = ?'
// 2.调用db.query()执行SQL语句的同时，为占位符指定具体的值
// 注意：如果SQL语句中有多个占位符，则必须使用数组为每个占位符指定具体的值
// 		如果SQL语句中只有一个占位符，则可以省略数组
db.query(sqlStr, 6, (err, results) => {
    if (err) return console.log(err.message)	// 失败
    if (results.affectedRows === 1) {
        console.log('删除数据成功')	// 成功
    }
})
```

##### 16.3.7 标记删除

​	使用 DELETE 语句，会把真正的把数据从表中删除掉。为了保险起见，**推荐使用**标记删除的形式，来**模拟删除的动作**。

​	所谓的标记删除，就是在表中设置类似于 **status** 这样的**状态字段**，来**标记**当前这条数据是否被删除。

​	当用户执行了删除的动作时，我们并没有执行 DELETE 语句把数据删除掉，而是执行了 UPDATE 语句，将这条数据对应的 status 字段标记为删除即可。

```javascript
// 标记删除: 使用update语句替代delete语句；只更新数据的状态，并没有真正删除
db.query('update users set status = 1 where id = ?', 5, (err, results) => {
    if (err) return console.log(err.message)	// 失败
    if (results.affectedRows === 1) {
        console.log('删除数据成功')	// 成功
    } 
})
```

### 17.前后端的身份认证

#### 17.1 Web开发模式

目前主流的Web开发模式有两种，分别是：

​	①基于服务端渲染的传统 Web 开发模式

​	②基于前后端分离的新型 Web 开发模式

##### 17.1.1 服务端渲染的Web开发模式

服务端渲染的概念：服务器发送给客户端的HTML页面，是在服务器通过字符串的拼接，动态生成的。因此，客户端不需要使用Ajax这样的技术额外请求页面的数据。代码示例如下：

```javascript
app.get('/index.html', (req, res) => {
    // 1.要渲染的数据
    const user = {
        name: 'zs',
        age: 20
    }
    // 2.服务器端通过字符串的拼接，动态生成HTML内容
    const html = `<h1>姓名：${user.name}, 年龄：${user.age}</h1>`
    // 3.把生成好的页面内容响应给客户端。因此，客户端拿到的是带有真实数据的HTML页面
    res.send(html)
})
```

##### 17.1.2 服务端渲染的优缺点

**优点：**

​	① 前端耗时少。因为服务器端负责动态生成 HTML 内容，浏览器只需要直接渲染页面即可。尤其是移动端，更省电。

​	② 有利于SEO。因为服务器端响应的是完整的 HTML 页面内容，所以爬虫更容易爬取获得信息，更有利于 SEO。

**缺点：**

​	① 占用服务器端资源。即服务器端完成 HTML 页面内容的拼接，如果请求较多，会对服务器造成一定的访问压力。

​	② 不利于前后端分离，开发效率低。使用服务器端渲染，则无法进行分工合作，尤其对于前端复杂度高的项目，不利于项目高效开发。

##### 17.1.3 前后端分离的Web开发模式

前后端分离的概念：前后端分离的开发模式，依赖于Ajax技术的广泛应用。简而言之，前后端分离的 Web开发模式，就是后端只负责提供API接口，前端使用Ajax调用接口的开发模式。

##### 17.1.4 前后端分离的优缺点

**优点：**

​	① 开发体验好。前端专注于 UI 页面的开发，后端专注于api 的开发，且前端有更多的选择性。

​	②用户体验好。Ajax 技术的广泛应用，极大的提高了用户的体验，可以轻松实现页面的局部刷新。

​	③减轻了服务器端的渲染压力。因为页面最终是在每个用户的浏览器中生成的。

**缺点：**

​	① 不利于SEO。因为完整的 HTML 页面需要在客户端动态拼接完成，所以爬虫对无法爬取页面的有效信息。（解决方案：利用 Vue、React 等前端框架的 **SSR** （server side render）技术能够很好的解决 SEO 问题！）

##### 17.1.5 如何选择Web开发模式

不谈业务场景而盲目选择使用何种开发模式都是耍流氓。

- 比如企业级网站，主要功能是展示而没有复杂的交互，并且需要良好的 SEO，则这时我们就需要使用服务器端渲染；
- 而类似后台管理项目，交互性比较强，不需要考虑 SEO，那么就可以使用前后端分离的开发模式。

另外，具体使用何种开发模式并不是绝对的，为了同时兼顾了首页的渲染速度和前后端分离的开发效率，一些网站采用了首屏服务器端渲染 + 其他页面前后端分离的开发模式。

#### 17.2 身份认证

##### 17.2.1 什么是身份认证

身份认证（Authentication）又称“身份验证”、“鉴权”，是指通过一定的手段，完成对用户身份的确认。

- 日常生活中的身份认证随处可见，例如：高铁的验票乘车，手机的密码或指纹解锁，支付宝或微信的支付密码等。
- 在 Web 开发中，也涉及到用户身份的认证，例如：各大网站的手机验证码登录**、**邮箱密码登录**、**二维码登录等。

##### 17.2.2 为什么需要身份认证

​	身份认证的目的，是为了确认当前所声称为某种身份的用户，确实是所声称的用户。例如，你去找快递员取快递，你要怎么证明这份快递是你的。

​	在互联网项目开发中，如何对用户的身份进行认证，是一个值得深入探讨的问题。例如，如何才能保证网站不会错误的将“马云的存款数额”显示到“马化腾的账户”上。

##### 17.2.3 不同开发模式下的身份认证

对于服务端渲染和前后端分离这两种开发模式来说，分别有着不同的身份认证方案：

​	① 服务端渲染推荐使用Session认证机制

​	② 前后端分离推荐使用 JWT认证机制

#### 17.3 Session认证机制

##### 17.3.1 HTTP协议的无状态性

​	了解 HTTP 协议的无状态性是进一步学习 Session 认证机制的必要前提。
​	HTTP 协议的无状态性，指的是客户端的每次 HTTP 请求都是独立的，连续多个请求之间没有直接的关系，服务器不会主动保留每次 HTTP 请求的状态。

 ![](C:\资料备份\学习笔记\01-Web笔记\101-Node.js\images\2022-08-02_084015.png)

##### 17.3.2 如何突破HTTP无状态的限制

对于超市来说，为了方便收银员在进行结算时给VIP用户打折，超市可以为每个VIP用户发放会员卡。

 ![](C:\资料备份\学习笔记\01-Web笔记\101-Node.js\images\2022-08-02_084226.png)

注意：现实生活中的会员卡身份认证方式，在Web开发中的专业术语叫做Cookie。

##### 17.3.3 什么是Cookie

​	Cookie 是存储在用户浏览器中的一段不超过 4 KB 的字符串。它由一个名称（Name）、一个值（Value）和其它几个用于控制 Cookie 有效期、安全性、使用范围的可选属性组成。
​	不同域名下的 Cookie 各自独立，每当客户端发起请求时，会自动把当前域名下所有未过期的 Cookie 一同发送到服务器。
Cookie的几大特性：

​	①自动发送

​	②域名独立

​	③过期时限

​	④4KB 限制

##### 17.3.4 Cookie在身份认证中的作用

​	客户端第一次请求服务器的时候，服务器通过响应头的形式，向客户端发送一个身份认证的 Cookie，客户端会自动将 Cookie 保存在浏览器中。
​	随后，当客户端浏览器每次请求服务器的时候，浏览器会自动将身份认证相关的 Cookie，通过请求头的形式发送给服务器，服务器即可验明客户端的身份。

 ![](C:\资料备份\学习笔记\01-Web笔记\101-Node.js\images\2022-08-02_084635.png)



##### 17.3.5 Cookie不具有安全性

​	由于 Cookie 是存储在浏览器中的，而且浏览器也提供了读写 Cookie 的 API，因此 Cookie 很容易被伪造，不具有安全性。因此不建议服务器将重要的隐私数据，通过 Cookie 的形式发送给浏览器。

 ![](C:\资料备份\学习笔记\01-Web笔记\101-Node.js\images\2022-08-02_084850.png)

注意：千万不要使用Cookie存储重要且隐私的数据！比如用户的身份信息、密码等。

##### 17.3.6 提高身份认证的安全性

为了防止客户伪造会员卡，收银员在拿到客户出示的会员卡之后，可以在收银机上进行刷卡认证。只有收银机确认存在的会员卡，才能被正常使用。

 ![](C:\资料备份\学习笔记\01-Web笔记\101-Node.js\images\2022-08-02_085225.png)

这种“会员卡 + 刷卡认证”的设计理念，就是Session认证机制的精髓。

##### 17.3.7 Session的工作原理

 ![](C:\资料备份\学习笔记\01-Web笔记\101-Node.js\images\2022-08-02_085438.png)

#### 17.4 在Express中使用Session认证

##### 17.4.1 安装express-session中间件

在Express项目中，只需要安装express-session中间件，即可在项目中使用Session认证：

> npm install express-session

##### 17.4.2 配置express-session中间件

express-session中间件安装成功后，需要通过app.user()来注册session中间件，示例代码如下：

```javascript
// 1.导入session中间件
var session = require('express-session')

// 2.配置session中间件
app.use(session({
    secret: 'keyboard cat',		// secret属性的值可以为任意字符串
    resave: false,				// 固定写法
    saveUninitialized: true		// 固定写法
}))
```

##### 17.4.3 向session中存数据

当express-session中间件配置成功后，即可通过req.session来访问和使用session对象，从而存储用户的关键信息：

```javascript
app.post('/api/login', (req, res) => {
    if (req.body.username !== 'admin' || req.body.password !== '000000') {
        return res.send({
            status: 1,
            msg: '登录失败'
        })
    }
    req.session.user = req.body  // 将用户信息，存储到Session中
    req.session.islogin = true 	 // 将用户的登录状态，存储到Session中
    
    res.send({
        status: 0, 
        msg: '登录成功'
    })
})
```

##### 17.4.4 从session中取数据

可以直接从req.session对象上获取之前存储的数据，示例代码如下：

```javascript
// 获取用户姓名的接口
app.get('/api/username', (req, res) => {
    // 判断用户是否登录
    if (!req.session.islogin) {
        return res.send({
            status: 1,
            msg: 'fail'
        })
     res.send({
         status: 0,
         msg: 'success',
         username: req.session.user.username
     })
    }
})
```

##### 17.4.5 清空session

调用req.session.destroy()函数，即可清空服务器保存的session信息。

```javascript
// 退出登录的接口
app.post('/api/logout', (req, res) => {
    // 清空当前客户端对应的session信息
    req.session.destroy()
    res.send({
        status: 0,
        msg: '退出登录成功'
    })
})
```

##### 17.4.6 session案例代码

 ![](C:\资料备份\学习笔记\01-Web笔记\101-Node.js\images\2022-08-02_104352.png)

package.json

```json
{
  "name": "code",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "dependencies": {
    "express": "^4.17.1",
    "express-session": "^1.17.1"
  }
}
```

app.js

```javascript
// 导入 express 模块
const express = require('express')
// 创建 express 的服务器实例
const app = express()

// TODO_01：请配置 Session 中间件
const session = require('express-session')
app.use(
  session({
    secret: 'itheima',
    resave: false,
    saveUninitialized: true,
  })
)

// 托管静态页面
app.use(express.static('./pages'))
// 解析 POST 提交过来的表单数据
app.use(express.urlencoded({ extended: false }))

// 登录的 API 接口
app.post('/api/login', (req, res) => {
  // 判断用户提交的登录信息是否正确
  if (req.body.username !== 'admin' || req.body.password !== '000000') {
    return res.send({ status: 1, msg: '登录失败' })
  }

  // TODO_02：请将登录成功后的用户信息，保存到 Session 中
  // 注意：只有成功配置了 express-session 这个中间件之后，才能够通过 req 点出来 session 这个属性
  req.session.user = req.body // 用户的信息
  req.session.islogin = true // 用户的登录状态

  res.send({ status: 0, msg: '登录成功' })
})

// 获取用户姓名的接口
app.get('/api/username', (req, res) => {
  // TODO_03：请从 Session 中获取用户的名称，响应给客户端
  if (!req.session.islogin) {
    return res.send({ status: 1, msg: 'fail' })
  }
  res.send({
    status: 0,
    msg: 'success',
    username: req.session.user.username,
  })
})

// 退出登录的接口
app.post('/api/logout', (req, res) => {
  // TODO_04：清空 Session 信息
  req.session.destroy()
  res.send({
    status: 0,
    msg: '退出登录成功',
  })
})

// 调用 app.listen 方法，指定端口号并启动web服务器
app.listen(80, function () {
  console.log('Express server running at http://127.0.0.1:80')
})

```

pages>index.html

```javascript
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>后台主页</title>
  <script src="./jquery.js"></script>
</head>

<body>
  <h1>首页</h1>

  <button id="btnLogout">退出登录</button>

  <script>
    $(function () {

      // 页面加载完成后，自动发起请求，获取用户姓名
      $.get('/api/username', function (res) {
        // status 为 0 表示获取用户名称成功；否则表示获取用户名称失败！
        if (res.status !== 0) {
          alert('您尚未登录，请登录后再执行此操作！')
          location.href = './login.html'
        } else {
          alert('欢迎您：' + res.username)
        }
      })

      // 点击按钮退出登录
      $('#btnLogout').on('click', function () {
        // 发起 POST 请求，退出登录
        $.post('/api/logout', function (res) {
          if (res.status === 0) {
            // 如果 status 为 0，则表示退出成功，重新跳转到登录页面
            location.href = './login.html'
          }
        })
      })
    })
  </script>
</body>

</html>
```

pages>login.html

```javascript
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>登录页面</title>
  <script src="./jquery.js"></script>
</head>

<body>
  <!-- 登录表单 -->
  <form id="form1">
    <div>账号：<input type="text" name="username" autocomplete="off" /></div>
    <div>密码：<input type="password" name="password" /></div>
    <button>登录</button>
  </form>

  <script>
    $(function () {
      // 监听表单的提交事件
      $('#form1').on('submit', function (e) {
        // 阻止默认提交行为
        e.preventDefault()
        // 发起 POST 登录请求
        $.post('/api/login', $(this).serialize(), function (res) {
          // status 为 0 表示登录成功；否则表示登录失败！
          if (res.status === 0) {
            location.href = './index.html'
          } else {
            alert('登录失败！')
          }
        })
      })
    })
  </script>
</body>

</html>
```

#### 17.5 JWT认证机制

##### 17.5.1 了解Session认证的局限性

​	Session 认证机制需要配合 Cookie 才能实现。由于 Cookie 默认不支持跨域访问，所以，当涉及到前端跨域请求后端接口的时候，需要做很多额外的配置，才能实现跨域 Session 认证。

注意：

- 当前端请求后端接口不存在跨域问题的时候，推荐使用 Session 身份认证机制。
- 当前端需要跨域请求后端接口的时候，不推荐使用 Session 身份认证机制，推荐使用 JWT 认证机制。

##### 17.5.2 什么是JWT

JWT（英文全称：JSON Web Token）是目前最流行的跨域认证解决方案。

##### 17.5.3 JWT的工作原理

 ![](C:\资料备份\学习笔记\01-Web笔记\101-Node.js\images\2022-08-02_105440.png)

​	总结：用户的信息通过Token字符串的形式，保存在客户端浏览器中。服务器通过还原Token字符串的形式来认证用户的身份。

##### 17.5.4 JWT的组成部分

​	JWT通常由三部分组成，分别是Header（头部）、Payload（有效荷载）、Signature（签名）。

三者之间使用英文的 ”.“ 分隔，格式如下：

> Header.Payload.Signature

其中：

-  Payload 部分才是真正的用户信息，它是用户信息经过加密之后生成的字符串。

-  Header 和 Signature 是安全性相关的部分，只是为了保证 Token 的安全性。

 ![](C:\资料备份\学习笔记\01-Web笔记\101-Node.js\images\2022-08-02_110306.png)

##### 17.5.5 JWT的使用方式

​	客户端收到服务器返回的 JWT 之后，通常会将它储存在 localStorage 或 sessionStorage 中。
​	此后，客户端每次与服务器通信，都要带上这个 JWT 的字符串，从而进行身份认证。推荐的做法是把 JWT 放在 HTTP 请求头的 Authorization 字段中，格式如下：

> Authorization: Bearer <token>

#### 17.6 在Express中使用JWT

##### 17.6.1 安装JWT相关的包

运行如下命令，安装如下两个JWT相关的包：

> npm install jsonwebtoken express-jwt

其中：

- jsonwebtoken用于生成JWT字符串
- express-jwt用于将JWT字符串解析还原成JSON对象

##### 17.6.2 导入JWT相关的包

使用require()函数，分别导入JWT相关的两个包：

```javascript
// 1.导入用于生成JWT字符串的包
const jwt = require('jsonwebtoken')
// 2.导入用于将客户端发送过来的JWT字符串，解析还原成JSON对象的包
const expressJWT = require('express-jwt)
```

##### 17.6.3 定义secret密钥

​	为了保证 JWT 字符串的安全性，防止 JWT 字符串在网络传输过程中被别人破解，我们需要专门定义一个用于加密和解密的 secret 密钥：

​	①当生成 JWT 字符串的时候，需要使用 secret 密钥对用户的信息进行加密，最终得到加密好的 JWT 字符串

​	②当把 JWT 字符串解析还原成 JSON 对象的时候，需要使用 secret 密钥进行解密

``` javascript
// 3.secret密钥的本质：就是一个字符串
const secretKey = 'yrk No1 ^_^'
```

##### 17.6.4 在登录成功后生成JWT字符串

调用jsonwebtoken包提供的sign()方法，将用户的信息加密成JWT字符串，响应给客户端：

```javascript
// 登录接口
app.post('/api/login', function (req, res) {
  // 将 req.body 请求体中的数据，转存为 userinfo 常量
  const userinfo = req.body
  // 登录失败
  if (userinfo.username !== 'admin' || userinfo.password !== '000000') {
    return res.send({
      status: 400,
      message: '登录失败！',
    })
  }
  // 登录成功
  // TODO_03：在登录成功之后，调用 jwt.sign() 方法生成 JWT 字符串。并通过 token 属性发送给客户端
  // 参数1：用户的信息对象
  // 参数2：加密的秘钥
  // 参数3：配置对象，可以配置当前 token 的有效期
  // 记住：千万不要把密码加密到 token 字符中
  const tokenStr = jwt.sign({ username: userinfo.username }, secretKey, { expiresIn: '30s' })
  res.send({
    status: 200,
    message: '登录成功！',
    token: tokenStr, // 要发送给客户端的 token 字符串
  })
})
```

##### 17.6.5 将JWT字符串还原为JSON对象

​	客户端每次在访问那些有权限接口的时候，都需要主动通过请求头中的 Authorization 字段，将 Token 字符串发送到服务器进行身份认证。
​	此时，服务器可以通过 express-jwt 这个中间件，自动将客户端发送过来的 Token 解析还原成 JSON 对象：

```javascript
// 使用app.use()来注册中间件
// expressJWT({secret: secretKey})就是用来解析Token的中间件
// .unless({path: [/^\/api\//]})用来指定哪些接口不需要访问权限
app.use(expressJWT({secret: secreKey}).unless({path: [/^\/api\//]}))
```

##### 17.6.6 使用req.user获取用户信息

​	当 express-jwt 这个中间件配置成功之后，即可在那些有权限的接口中，使用 req.user 对象，来访问从 JWT 字符串中解析出来的用户信息了，示例代码如下：

```javascript
// 这是一个有权限的API接口
app.get('/admin/getinfo', function(req, res) {
    console.log(req.user)
    res.send({
        status: 200,
        message: '获取用户信息成功',
        data: req.user
    })
})
```

##### 17.6.7 捕获解析JWT失败后产生的错误

​	当使用 express-jwt 解析 Token 字符串时，如果客户端发送过来的 Token 字符串过期或不合法，会产生一个解析失败的错误，影响项目的正常运行。我们可以通过 Express 的错误中间件，捕获这个错误并进行相关的处理，示例代码如下：

```javascript
app.use((err, req, res, next) => {
    //token解析失败导致的错误
    if (err.name === 'UnauthorizedError') {
        return res.send({
            status: 401,
            message: '无效的token'
        })
    }
    // 其他原因导致的错误
    res.send({
        status: 500,
        message: '未知错误'
    })
})
```

##### 17.6.8 JWT案例代码

app.js

```javascript
// 导入 express 模块
const express = require('express')
// 创建 express 的服务器实例
const app = express()

// TODO_01：安装并导入 JWT 相关的两个包，分别是 jsonwebtoken 和 express-jwt
const jwt = require('jsonwebtoken')
// const expressJWT = require('express-jwt')旧版使用方法
var { expressjwt: expressJWT } = require("express-jwt"); //新版使用方法
// 允许跨域资源共享
const cors = require('cors')
app.use(cors())

// 解析 post 表单数据的中间件
const bodyParser = require('body-parser')
app.use(bodyParser.urlencoded({ extended: false }))

// TODO_02：定义 secret 密钥，建议将密钥命名为 secretKey
const secretKey = 'itheima No1 ^_^'

// TODO_04：注册将 JWT 字符串解析还原成 JSON 对象的中间件
// 注意：只要配置成功了 express-jwt 这个中间件，就可以把解析出来的用户信息，挂载到 req.user 属性上
app.use(
  expressJWT({ 
    secret: secretKey,
    algorithms: ["HS256"] //新版需要加该属性和值
  }).unless({ path: [/^\/api\//] }))

// 登录接口
app.post('/api/login', function (req, res) {
  // 将 req.body 请求体中的数据，转存为 userinfo 常量
  const userinfo = req.body
  // 登录失败
  if (userinfo.username !== 'admin' || userinfo.password !== '000000') {
    return res.send({
      status: 400,
      message: '登录失败！',
    })
  }
  // 登录成功
  // TODO_03：在登录成功之后，调用 jwt.sign() 方法生成 JWT 字符串。并通过 token 属性发送给客户端
  // 参数1：用户的信息对象
  // 参数2：加密的秘钥
  // 参数3：配置对象，可以配置当前 token 的有效期
  // 记住：千万不要把密码加密到 token 字符中
  const tokenStr = jwt.sign({ username: userinfo.username }, secretKey, { expiresIn: '30s' })
  res.send({
    status: 200,
    message: '登录成功！',
    token: tokenStr, // 要发送给客户端的 token 字符串
  })
})

// 这是一个有权限的 API 接口
app.get('/admin/getinfo', function (req, res) {
  // TODO_05：使用 req.user 获取用户信息，并使用 data 属性将用户信息发送给客户端
  console.log(req.user)
  res.send({
    status: 200,
    message: '获取用户信息成功！',
    //data: req.user 旧版
    data: req.auth, // （新版方法）要发送给客户端的用户信息
  })
})

// TODO_06：使用全局错误处理中间件，捕获解析 JWT 失败后产生的错误
app.use((err, req, res, next) => {
  // 这次错误是由 token 解析失败导致的
  if (err.name === 'UnauthorizedError') {
    return res.send({
      status: 401,
      message: '无效的token',
    })
  }
  res.send({
    status: 500,
    message: '未知的错误',
  })
})

// 调用 app.listen 方法，指定端口号并启动web服务器
app.listen(8888, function () {
  console.log('Express server running at http://127.0.0.1:8888')
})
```

package.json

```json
{
  "name": "backend",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "dependencies": {
    "body-parser": "^1.19.0",
    "cors": "^2.8.5",
    "express": "^4.17.1",
    "express-jwt": "^7.7.5",
    "jsonwebtoken": "^8.5.1"
  }
}
```

 ![](C:\资料备份\学习笔记\01-Web笔记\101-Node.js\images\2022-08-02_150118.png)

 ![](C:\资料备份\学习笔记\01-Web笔记\101-Node.js\images\2022-08-02_150133.png)

注意：token设置三十秒有效，必须在过期范围内使用token值，访问带有权限的页面，发送请求头Authorization：Bearer + 生成的token。






















































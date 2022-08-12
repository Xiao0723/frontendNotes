### 第1章 ECMASript相关介绍

#### 1.1 什么是ECMA

ECMA（European Computer Manufacturers Association）中文名称为欧洲计算机制造商协会，这个组织的目标是评估、开发和认可电信和计算机标准。1994 年后该组织改名为 Ecma 国际。

#### 1.2 什么是ECMAScript

ECMAScript 是由 Ecma 国际通过 ECMA-262 标准化的脚本程序设计语言。

#### 1.3 什么是ECMA-262

Ecma 国际制定了许多标准，而 ECMA-262 只是其中的一个，所有标准列表查看
http://www.ecma-international.org/publications/standards/Standard.htm

#### 1.4 ECMA-262历史

ECMA-262（ECMAScript）历史版本查看网址
http://www.ecma-international.org/publications/standards/Ecma-262-arch.htm
第 1 版 1997 年 制定了语言的基本语法
第 2 版 1998 年 较小改动
第 3 版 1999 年 引入正则、异常处理、格式化输出等。IE 开始支持
第 4 版 2007 年 过于激进，未发布
第 5 版 2009 年 引入严格模式、JSON，扩展对象、数组、原型、字符串、日期方法
第 6 版 2015 年 模块化、面向对象语法、Promise、箭头函数、let、const、数组解构赋值等等
第 7 版 2016 年 幂运算符、数组扩展、Async/await 关键字
第 8 版 2017 年 Async/await、字符串扩展
第 9 版 2018 年 对象解构赋值、正则扩展
第 10 版 2019 年 扩展对象、数组方法

注：从 ES6 开始，每年发布一个版本，版本号比年份最后一位大 1

#### 1.5 谁在维护ECMA-262

TC39（Technical Committee 39）是推进 ECMAScript 发展的委员会。其会员都是公司（其中主要是浏览器厂商，有苹果、谷歌、微软、因特尔等）。TC39 定期召开会议，会议由会员公司的代表与特邀专家出席。

#### 1.6 为什么要学习ES6

- ES6 的版本变动内容最多，具有里程碑意义
- ES6 加入许多新的语法特性，编程实现更简单、高效
- ES6 是前端发展趋势，就业必备技能

#### 1.7 ES6兼容性

http://kangax.github.io/compat-table/es6/ 可查看兼容性

### 第2章 ECMASript6新特性

#### 2.1 let 关键字

let 关键字用来声明变量，使用 let 声明的变量有几个特点：

​	1) 不允许重复声明

​	2) 块儿级作用域

​	3) 不存在变量提升

​	4) 不影响作用域链

应用场景：以后声明变量使用 let 就对了

```js
//声明变量
let a;
let b,c,d;
let e = 100;
let f = 521, g = 'iloveyou', h = [];

//1. 变量不能重复声明(控制台报错)
let star = '罗志祥';
let star = '小猪';

//2. 块儿级作用域  全局, 函数, eval
if else while for 
{
	let girl = '周扬青';
}
console.log(girl);

//3. 不存在变量提升(控制台报错)
console.log(song);
let song = '恋爱达人';

//4. 不影响作用域链
{
let school = '尚硅谷';
function fn(){
console.log(school);
}
fn();
}
```

实践案例

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>点击 DIV 换色</title>
    <link crossorigin="anonymous" href="https://cdn.bootcss.com/twitter-bootstrap/3.3.7/css/bootstrap.min.css"
        rel="stylesheet">
    <style>
        .item {
            width: 100px;
            height: 50px;
            border: solid 1px rgb(42, 156, 156);
            float: left;
            margin-right: 10px;
        }
    </style>
</head>

<body>
    <div class="container">
        <h2 class="page-header">点击切换颜色</h2>
        <div class="item"></div>
        <div class="item"></div>
        <div class="item"></div>
    </div>
    <script>
        //获取div元素对象
        let items = document.getElementsByClassName('item');

        //遍历并绑定事件 以往做法用var绑定事件需要用this，现在用let块儿级作用域特点就可以不使用this
        for(let i = 0;i<items.length;i++){
            items[i].onclick = function(){
                //修改当前元素的背景颜色
                // this.style.background = 'pink';
                items[i].style.background = 'pink';
            }
        }
        
    </script>
</body>

</html>
```

#### 2.2 const 关键字

const 关键字用来声明常量，const 声明有以下特点

​	1) 声明必须赋初始值

​	2) 标识符一般为大写

​	3) 不允许重复声明

​	4) 值不允许修改

​	5) 块儿级作用域

注意: 对象属性修改和数组元素变化不会出发 const 错误

应用场景：声明对象类型使用 const，非对象类型声明选择 let

```js
//声明常量
const SCHOOL = '尚硅谷';

//1. 一定要赋初始值
const A;
//2. 一般常量使用大写(潜规则)
const a = 100;
//3. 常量的值不能修改
SCHOOL = 'ATGUIGU';
//4. 块儿级作用域
{
const PLAYER = 'UZI';
}
console.log(PLAYER);
//5. 对于数组和对象的元素修改, 不算做对常量的修改, 不会报错
const TEAM = ['UZI','MXLG','Ming','Letme'];
TEAM.push('Meiko');
```

#### 2.3 变量的解构赋值

ES6 允许按照一定模式，从数组和对象中提取值，对变量进行赋值，这被称
为解构赋值。

```js
//1. 数组的解构赋值
const F4 = ['小沈阳','刘能','赵四','宋小宝'];
let [xiao, liu, zhao, song] = F4;
console.log(xiao);
console.log(liu);
console.log(zhao);
console.log(song);

//2. 对象的解构赋值
const zhao = {
    name: '赵本山',
    age: '不详',
    xiaopin: function(){
    	console.log("我可以演小品");
    }
};

//3. 复杂的解构赋值
let wangfei = {
    name: '王菲',
    age: 18,
    songs: ['红豆', '流年', '暧昧', '传奇'],
    history: [
        {name: '窦唯'},
        {name: '李亚鹏'},
        {name: '谢霆锋'}
    ]
};
let {songs: [one, two, three], history: [first, second, third]} =
wangfei;
```

注意：频繁使用对象方法、数组元素，就可以使用解构赋值形式

#### 2.4 模块字符串

模板字符串（template string）是增强版的字符串，用反引号（`）标识，特点：

1) 字符串中可以出现换行符

2) 可以使用 ${xxx} 形式输出变量

```js
// 定义字符串
let str = 
    `<ul>
        <li>沈腾</li>
        <li>玛丽</li>
        <li>魏翔</li>
        <li>艾伦</li>
	</ul>`;
// 变量拼接
let star = '王宁';
let result = `${star}在前几年离开了开心麻花`;
```

注意：当遇到字符串与变量拼接的情况使用模板字符串

#### 2.5 简化对象写法

ES6 允许在大括号里面，直接写入变量和函数，作为对象的属性和方法。这样的书写更加简洁。

```js
let name = '尚硅谷';
let slogon = '永远追求行业更高标准';
let improve = function () {
	console.log('可以提高你的技能');
}
//属性和方法简写
let atguigu = {
    name,
    slogon,
    improve,
    change() {
    	console.log('可以改变你')
    }
};
```

注意：对象简写形式简化了代码，所以以后用简写就对了

#### 2.6 箭头函数

ES6 允许使用「箭头」（=>）定义函数。

```js
/**
* 1. 通用写法
*/
let fn = (arg1, arg2, arg3) => {
 return arg1 + arg2 + arg3;
}
```

箭头函数的注意点:

1) 如果形参只有一个，则小括号可以省略

2) 函数体如果只有一条语句，则花括号可以省略，函数的返回值为该条语句的
执行结果

3) 箭头函数 this 指向声明时所在作用域下 this 的值

4) 箭头函数不能作为构造函数实例化

5) 不能使用 arguments

```js
/**
* 1. 省略小括号的情况
*/
let fn2 = num => {
	return num * 10;
};
/**
* 2. 省略花括号的情况
*/
let fn3 = score => score * 20;
/**
* 3. this 指向声明时所在作用域中 this 的值
*/
function getName(){
    console.log(this.name);
}
//箭头函数this是静态的. this 始终指向函数声明时所在作用域下的 this 的值
let getName2 = () => {
    console.log(this.name);
}

//设置 window 对象的 name 属性
window.name = '尚硅谷';
const school = {
    name: "ATGUIGU"
}

//直接调用
getName();	//尚硅谷
getName2(); //尚硅谷

//call方法调用
getName.call(school);	//ATGUIGU
getName2.call(school);	//尚硅谷

/**
* 4. 不能作为构造函数实例化(控制台报错)
*/
let Person = (name, age) => {
    this.name = name;
    this.age = age;
}
let me = new Person('xiao',30);
console.log(me);

/**
* 5. 不能使用 arguments(控制台报错)
*/
let fn = () => {
    console.log(arguments);
}
fn(1,2,3);
```

注意：箭头函数不会更改 this 指向，用来指定回调函数会非常合适

箭头函数的实践

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>箭头函数实践</title>
    <style>
        div {
            width: 200px;
            height: 200px;
            background: #58a;
        }
    </style>
</head>
<body>
    <div id="ad"></div>
    <script>
        //需求-1  点击 div 2s 后颜色变成『粉色』
        //获取元素
        let ad = document.getElementById('ad');
        /*
        //函数做法
        ad.addEventListener("click", function(){
            // 以往的做法保存 this 的值
            let _this = this;
            //定时器
            setTimeout(function(){  
                //修改背景颜色
                // console.log(this);
                _this.style.background = 'pink'; //通过作用域找到外层_this
            }, 2000);
        });
        */
        //箭头函数做法
        ad.addEventListener("click", function(){
            //定时器
            setTimeout(() => {  
                // console.log(this);
                this.style.background = 'pink';
            }, 2000);
        });

        //需求-2  从数组中返回偶数的元素
        const arr = [1,6,9,10,100,25];
        /*
        //函数做法
        const result = arr.filter(function(item){
            if(item % 2 === 0){
                return true;
            }else{
                return false;
            }
        });
        */
        //箭头函数做法
        const result = arr.filter(item => item % 2 === 0);
        console.log(result);

        // 箭头函数适合与 this 无关的回调. 定时器, 数组的方法回调
        // 箭头函数不适合与 this 有关的回调. 事件回调, 对象的方法

    </script>
</body>

</html>
```

#### 2.7 参数默认值

```js
//ES6 允许给函数参数赋值初始值
//1. 形参初始值 具有默认值的参数, 一般位置要靠后(潜规则)
function add(a,c=10,b) {
    return a + b + c;
}
let result = add(1,2);
console.log(result);

//2. 与解构赋值结合
function connect({host="127.0.0.1", username,password, port}){
    console.log(host)
    console.log(username)
    console.log(password)
    console.log(port)
}
connect({
    host: 'atguigu.com',
    username: 'root',
    password: 'root',
    port: 3306
})
```

#### 2.8 rest参数

```js
// ES6 引入 rest 参数，用于获取函数的实参，用来代替 arguments
// ES5 获取实参的方式
function date(){
	console.log(arguments);
}
date('白芷','阿娇','思慧');

// rest 参数
function date(...args){
	console.log(args);// filter some every map 
}
date('阿娇','柏芝','思慧');

// rest 参数必须要放到参数最后
function fn(a,b,...args){
    console.log(a);
    console.log(b);
    console.log(args);
}
fn(1,2,3,4,5,6);
```

#### 2.9 spread扩展运算符

```js
// 『...』 扩展运算符能将『数组』转换为逗号分隔的『参数序列』
//声明一个数组 ...
const tfboys = ['易烊千玺','王源','王俊凯'];
// => '易烊千玺','王源','王俊凯'

// 声明一个函数
function chunwan(){
    console.log(arguments);
}

chunwan(...tfboys);// chunwan('易烊千玺','王源','王俊凯')   
```

扩展运算符应用

```js
//1. 数组的合并 情圣  误杀  唐探
const kuaizi = ['王太利','肖央'];
const fenghuang = ['曾毅','玲花'];
// const zuixuanxiaopingguo = kuaizi.concat(fenghuang);
const zuixuanxiaopingguo = [...kuaizi, ...fenghuang];
console.log(zuixuanxiaopingguo);

//2. 数组的克隆
const sanzhihua = ['E','G','M'];
const sanyecao = [...sanzhihua];//  ['E','G','M']
console.log(sanyecao);

//3. 将伪数组转为真正的数组
const divs = document.querySelectorAll('div');
const divArr = [...divs];
console.log(divArr);// arguments
```

#### 2.10 Symbol

```js
//创建Symbol
let s = Symbol();
// console.log(s, typeof s);
let s2 = Symbol('尚硅谷');
let s3 = Symbol('尚硅谷');
console.log(s2===s3) //false
//Symbol.for 创建
let s4 = Symbol.for('尚硅谷');
let s5 = Symbol.for('尚硅谷');
console.log(s4===s5) //ture

//不能与其他数据进行运算(控制台报错)
let result = s + 100;
let result = s > 100;
let result = s + s;

// USONB  you are so niubility 
// u  undefined
// s  string  symbol
// o  object
// n  null number
// b  boolean
```

symbol创建对象属性

```js
//向对象中添加方法 up down
let game = {
    name:'俄罗斯方块',
    up: function(){},
    down: function(){}
};

//声明一个对象 很安全和快速创建对象的方法，不会导致冲突
let methods = {
    up: Symbol(),
    down: Symbol()
};

game[methods.up] = function(){
    console.log("我可以改变形状");
}

game[methods.down] = function(){
    console.log("我可以快速下降!!");
}

console.log(game);

// 为对象添加独一无二的方法
let youxi = { 
    name:"狼人杀",
    [Symbol('say')]: function(){
        console.log("我可以发言")
    },
    [Symbol('zibao')]: function(){
        console.log('我可以自爆');
    }
}

console.log(youxi)
```

Symbol内置值

​	除了定义自己使用的 Symbol 值以外，ES6 还提供了 11 个内置的 Symbol 值，指向语言内部使用的方法。可以称这些方法为魔术方法，因为它们会在特定的场景下自动执行。

| 方法                      | 描述                                                         |
| ------------------------- | ------------------------------------------------------------ |
| Symbol.hasInstance        | 当其他对象使用 instanceof 运算符，判断是否为该对<br/>象的实例时，会调用这个方法 |
| Symbol.isConcatSpreadable | 对象的 Symbol.isConcatSpreadable 属性等于的是一个<br/>布尔值，表示该对象用于 Array.prototype.concat()时，
是否可以展开。 |
| Symbol.species            | 创建衍生对象时，会使用该属性                                 |
| Symbol.match              | 当执行 str.match(myObject) 时，如果该属性存在，会<br/>调用它，返回该方法的返回值。 |
| Symbol.replace            | 当该对象被 str.replace(myObject)方法调用时，会返回<br/>该方法的返回值。 |
| Symbol.search             | 当该对象被 str.search (myObject)方法调用时，会返回<br/>该方法的返回值。 |
| Symbol.split              | 当该对象被 str.split(myObject)方法调用时，会返回该<br/>方法的返回值。 |
| Symbol.iterator           | 对象进行 for...of 循环时，会调用 Symbol.iterator 方法，<br/>返回该对象的默认遍历器 |
| Symbol.toPrimitive        | 该对象被转为原始类型的值时，会调用这个方法，返<br/>回该对象对应的原始类型值。 |
| Symbol. toStringTag       | 在该对象上面调用 toString 方法时，返回该方法的返<br/>回值    |
| Symbol. unscopables       | 该对象指定了使用 with 关键字时，哪些属性会被 with<br/>环境排除。 |

#### 2.11 迭代器

遍历器（Iterator）就是一种机制。它是一种接口，为各种不同的数据结构提供统一的访问机制。任何数据结构只要部署 Iterator 接口，就可以完成遍历操作。

1) ES6 创造了一种新的遍历命令 for...of 循环，Iterator 接口主要供 for...of 消费

2) 原生具备 iterator 接口的数据(可用 for of 遍历)
	a) Array

​	b) Arguments

​	c) Set

​	d) Map

​	e) String

​	f) TypedArray

​	g) NodeList

3) 工作原理

​	a) 创建一个指针对象，指向当前数据结构的起始位置

​	b) 第一次调用对象的 next 方法，指针自动指向数据结构的第一个成员

​	c) 接下来不断调用 next 方法，指针一直往后移动，直到指向最后一个成员

​	d) 每调用 next 方法返回一个包含 value 和 done 属性的对象

注: 需要自定义遍历数据的时候，要想到迭代器。

```js
//声明一个数组
const xiyou = ['唐僧','孙悟空','猪八戒','沙僧'];

//使用 for...of 遍历数组
for(let v of xiyou){	//of返回是数组值，in返回是数组下标值
console.log(v);
}

let iterator = xiyou[Symbol.iterator]();

//调用对象的next方法
console.log(iterator.next());
console.log(iterator.next());
console.log(iterator.next());
console.log(iterator.next());
console.log(iterator.next());
```

使用迭代器自定义遍历数据

```js
//声明一个对象
const banji = {
    name: "终极一班",
    stus: [
        'xiaoming',
        'xiaoning',
        'xiaotian',
        'knight'
    ],
    [Symbol.iterator]() {
    //索引变量
        let index = 0;
        //
        let _this = this;
        return {
            next: function () {
                if (index < _this.stus.length) {
                    const result = { value: _this.stus[index], done: false };
                    //下标自增
                    index++;
                    //返回结果
                    return result;
                }else{
                    return {value: undefined, done: true};
                }
            }
        }
    }
}

//遍历这个对象 
for (let v of banji) {
	console.log(v);
}
```

#### 2.12 生成器

生成器函数是 ES6 提供的一种异步编程解决方案，语法行为与传统函数完全不同

```js
//生成器其实就是一个特殊的函数
//异步编程  纯回调函数  node fs  ajax mongodb
//函数代码的分隔符
function * gen(){
    // console.log(111);
    yield '一只没有耳朵';
    // console.log(222);
    yield '一只没有尾部';
    // console.log(333);
    yield '真奇怪';
    // console.log(444);
}

let iterator = gen();
console.log(iterator.next());
console.log(iterator.next());
console.log(iterator.next());
console.log(iterator.next());

//遍历
for(let v of gen()){
	console.log(v);
}
```

代码说明：

​	1) * 的位置没有限制

​	2) 生成器函数返回的结果是迭代器对象，调用迭代器对象的 next 方法可以得到
yield 语句后的值

​	3) yield 相当于函数的暂停标记，也可以认为是函数的分隔符，每调用一次 next
方法，执行一段代码

​	4) next 方法可以传递实参，作为 yield 语句的返回值

生成器函数参数

```js
function * gen(arg){
    console.log(arg);
    let one = yield 111;
    console.log(one);
    let two = yield 222;
    console.log(two);
    let three = yield 333;
    console.log(three);
}

//执行获取迭代器对象
let iterator = gen('AAA');
console.log(iterator.next());
//next方法可以传入实参
console.log(iterator.next('BBB'));
console.log(iterator.next('CCC'));
console.log(iterator.next('DDD'));
```

生成器函数实例1

```js
// 异步编程  文件操作 网络操作(ajax, request) 数据库操作
// 1s 后控制台输出 111  2s后输出 222  3s后输出 333 
// 回调地狱
setTimeout(() => {
	console.log(111);
	setTimeout(() => {
		console.log(222);
		setTimeout(() => {
			console.log(333);
		}, 3000);
	}, 2000);
}, 1000);

function one(){
    setTimeout(()=>{
        console.log(111);
        iterator.next();
    },1000)
}

function two(){
    setTimeout(()=>{
        console.log(222);
        iterator.next();
    },2000)
}

function three(){
    setTimeout(()=>{
        console.log(333);
        iterator.next();
    },3000)
}

function * gen(){
    yield one();
    yield two();
    yield three();
}

//调用生成器函数
let iterator = gen();
iterator.next();
```

生成器函数实例2

```js
//模拟获取  用户数据  订单数据  商品数据 
function getUsers(){
    setTimeout(()=>{
        let data = '用户数据';
        //调用 next 方法, 并且将数据传入
        iterator.next(data);
    }, 1000);
} 

function getOrders(){
    setTimeout(()=>{
        let data = '订单数据';
        iterator.next(data);
    }, 1000)
}

function getGoods(){
    setTimeout(()=>{
        let data = '商品数据';
        iterator.next(data);
    }, 1000)
}

function * gen(){
    let users = yield getUsers();
    let orders = yield getOrders();
    let goods = yield getGoods();
}

//调用生成器函数
let iterator = gen();
iterator.next();
```

#### 2.13 Promise

​	Promise 是 ES6 引入的异步编程的新解决方案。语法上 Promise 是一个构造函数，用来封装异步操作并可以获取其成功或失败的结果。

​	1) Promise 构造函数: Promise (excutor) {}

​	2) Promise.prototype.then 方法

​	3) Promise.prototype.catch 方法

```js
//实例化 Promise 对象
const p = new Promise(function(resolve, reject){
    setTimeout(function(){
        //
        // let data = '数据库中的用户数据';
        // resolve
        // resolve(data);

        let err = '数据读取失败';
        reject(err);
    }, 1000);
});

//调用 promise 对象的 then 方法
p.then(function(value){
	console.log(value);
}, function(reason){
	console.error(reason);
})
```

Promise读取文件

```js
//1. 引入 fs 模块
const fs = require('fs');

//2. 调用方法读取文件
fs.readFile('./resources/为学.md', (err, data)=>{
    //如果失败, 则抛出错误
    if(err) throw err;
    //如果没有出错, 则输出内容
    console.log(data.toString());
});

//3. 使用 Promise 封装
const p = new Promise(function(resolve, reject){
    fs.readFile("./resources/为学.mda", (err, data)=>{
        //判断如果失败
        if(err) reject(err);
        //如果成功
        resolve(data);
    });
});

p.then(function(value){
    console.log(value.toString());
}, function(reason){
    console.log("读取失败!!");
});
```

Promise封装AJAX

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>发送 AJAX 请求</title>
</head>

<body>
    <script>
        // 接口地址: https://api.apiopen.top/getJoke
        const p = new Promise((resolve, reject) => {
            //1. 创建对象
            const xhr = new XMLHttpRequest();

            //2. 初始化
            xhr.open("GET", "https://api.apiopen.top/getJ");

            //3. 发送
            xhr.send();

            //4. 绑定事件, 处理响应结果
            xhr.onreadystatechange = function () {
                //判断
                if (xhr.readyState === 4) {
                    //判断响应状态码 200-299
                    if (xhr.status >= 200 && xhr.status < 300) {
                        //表示成功
                        resolve(xhr.response);
                    } else {
                        //如果失败
                        reject(xhr.status);
                    }
                }
            }
        })
        
        //指定回调
        p.then(function(value){
            console.log(value);
        }, function(reason){
            console.error(reason);
        });
    </script>
</body>

</html>
```

Promise-then方法

```js
//创建 promise 对象
const p = new Promise((resolve, reject)=>{
    setTimeout(()=>{
        resolve('用户数据');
        // reject('出错啦');
    }, 1000)
});

//调用 then 方法  then方法的返回结果是 Promise 对象, 对象状态由回调函数的执行结果决定
//1. 如果回调函数中返回的结果是 非 promise 类型的属性, 状态为成功, 返回值为对象的成功的值
const result = p.then(value => {
    console.log(value);
    //1. 非 promise 类型的属性
    // return 'iloveyou';
    //2. 是 promise 对象
    // return new Promise((resolve, reject)=>{
    //     // resolve('ok');
    //     reject('error');
    // });
    //3. 抛出错误
    // throw new Error('出错啦!');
    throw '出错啦!';
}, reason=>{
    console.warn(reason);
});

//链式调用
p.then(value=>{

}).then(value=>{

});
```

Promise实践-读取多个文件

```js
//引入 fs 模块
const fs = require("fs");

// fs.readFile('./resources/为学.md', (err, data1)=>{
//     fs.readFile('./resources/插秧诗.md', (err, data2)=>{
//         fs.readFile('./resources/观书有感.md', (err, data3)=>{
//             let result = data1 + '\r\n' +data2  +'\r\n'+ data3;
//             console.log(result);
//         });
//     });
// });

//使用 promise 实现
const p = new Promise((resolve, reject) => {
    fs.readFile("./resources/为学.md", (err, data) => {
        resolve(data);
    });
});

p.then(value => {
    return new Promise((resolve, reject) => {
        fs.readFile("./resources/插秧诗.md", (err, data) => {
            resolve([value, data]);
        });
    });
}).then(value => {
    return new Promise((resolve, reject) => {
        fs.readFile("./resources/观书有感.md", (err, data) => {
            //压入
            value.push(data);
            resolve(value);
        });
    })
}).then(value => {
    console.log(value.join('\r\n'));
});
```

Promise-catch方法

```js
const p = new Promise((resolve, reject)=>{
    setTimeout(()=>{
    	//设置 p 对象的状态为失败, 并设置失败的值
    	reject("出错啦!");
    }, 1000)
});

// p.then(function(value){}, function(reason){
//     console.error(reason);
// });

p.catch(function(reason){
	console.warn(reason);
});
```

#### 2.14 Set

​	ES6 提供了新的数据结构 Set（集合）。它类似于数组，但成员的值都是唯一的，集合实现了 iterator 接口，所以可以使用『扩展运算符』和『for…of…』进行遍历，集合的属性和方法：

​	1) size 返回集合的元素个数

​	2) add 增加一个新元素，返回当前集合

​	3) delete 删除元素，返回 boolean 值

​	4) has 检测集合中是否包含某个元素，返回 boolean 值

​	5) clear 清空集合，返回 undefined

```js
//声明一个 set
let s = new Set();
let s2 = new Set(['大事儿','小事儿','好事儿','坏事儿','小事儿']);

//元素个数
console.log(s2.size);
//添加新的元素
s2.add('喜事儿');
//删除元素
s2.delete('坏事儿');
//检测
console.log(s2.has('糟心事'));
//清空
s2.clear();
console.log(s2);

for(let v of s2){
	console.log(v);
}
```

Set集合实践

```js
let arr = [1,2,3,4,5,4,3,2,1];
//1. 数组去重
let result = [...new Set(arr)];
console.log(result);
//2. 交集
let arr2 = [4,5,6,5,6];
let result = [...new Set(arr)].filter(item => {
    let s2 = new Set(arr2);// 4 5 6
    if(s2.has(item)){
    	return true;
    }else{
    	return false;
    }
});
let result = [...new Set(arr)].filter(item => new Set(arr2).has(item));
console.log(result);

//3. 并集
let union = [...new Set([...arr, ...arr2])];
console.log(union);

//4. 差集
let diff = [...new Set(arr)].filter(item => !(new Set(arr2).has(item)));
console.log(diff);
```

#### 2.15 Map

ES6 提供了 Map 数据结构。它类似于对象，也是键值对的集合。但是“键”的范围不限于字符串，各种类型的值（包括对象）都可以当作键。Map 也实现了iterator 接口，所以可以使用『扩展运算符』和『for…of…』进行遍历。Map 的属性和方法：

​	1) size 返回 Map 的元素个数

​	2) set 增加一个新元素，返回当前 Map

​	3) get 返回键名对象的键值

​	4) has 检测 Map 中是否包含某个元素，返回 boolean 值

​	5) clear 清空集合，返回 undefined

```js
//声明 Map
let m = new Map();

//添加元素
m.set('name','尚硅谷');
m.set('change', function(){
    console.log("我们可以改变你!!");
});
let key = {
    school : 'ATGUIGU'
};
m.set(key, ['北京','上海','深圳']);

//size
console.log(m.size);

//删除
m.delete('name');

//获取
console.log(m.get('change'));
console.log(m.get(key));

//清空
m.clear();

//遍历
for(let v of m){
    console.log(v);
}

// console.log(m);
```

#### 2.16 class 类

ES6 提供了更接近传统语言的写法，引入了 Class（类）这个概念，作为对象的模板。通过 class 关键字，可以定义类。基本上，ES6 的 class 可以看作只是一个语法糖，它的绝大部分功能，ES5 都可以做到，新的 class 写法只是让对象原型的写法更加清晰、更像面向对象编程的语法而已。
知识点：
	1) class 声明类

​	2) constructor 定义构造函数初始化

​	3) extends 继承父类

​	4) super 调用父级构造方法

​	5) static 定义静态方法和属性

​	6) 父类方法可以重写

```js
//手机
function Phone(brand, price){
    this.brand = brand;
    this.price = price;
}

//添加方法
Phone.prototype.call = function(){
	console.log("我可以打电话!!");
}

//实例化对象
let Huawei = new Phone('华为', 5999);
Huawei.call();
console.log(Huawei);

//class
class Shouji{
    //构造方法 名字不能修改
    constructor(brand, price){
        this.brand = brand;
        this.price = price;
    }

    //方法必须使用该语法, 不能使用 ES5 的对象完整形式
    call(){
    console.log("我可以打电话!!");
    }
}

let onePlus = new Shouji("1+", 1999);

console.log(onePlus);
```

类的静态成员

```js
function Phone(){

}
Phone.name = '手机';
Phone.change = function(){
	console.log("我可以改变世界");
}
Phone.prototype.size = '5.5inch';

let nokia = new Phone();

console.log(nokia.name); //undefined
nokia.change(); //报错
console.log(nokia.size); //5.5inch
// 原因是name属性和change方法属于Phone函数的，通过实例对象的nokia是没办法访问到的

class Phone{
	//静态属性
	static name = '手机';
    static change(){
    	console.log("我可以改变世界");
    }
}

let nokia = new Phone();
console.log(nokia.name); //underfined
console.log(Phone.name); //手机
```

类继承-1

```js
//手机
function Phone(brand, price){
    this.brand = brand;
    this.price = price;
}

Phone.prototype.call = function(){
	console.log("我可以打电话");
}

//智能手机
function SmartPhone(brand, price, color, size){
    Phone.call(this, brand, price);
    this.color = color;
    this.size = size;
}

//设置子级构造函数的原型
SmartPhone.prototype = new Phone;
SmartPhone.prototype.constructor = SmartPhone;

//声明子类的方法
SmartPhone.prototype.photo = function(){
	console.log("我可以拍照")
}

SmartPhone.prototype.playGame = function(){
	console.log("我可以玩游戏");
}

const chuizi = new SmartPhone('锤子',2499,'黑色','5.5inch');

console.log(chuizi);
```

类继承-2

```js
class Phone{
    //构造方法
    constructor(brand, price){
        this.brand = brand;
        this.price = price;
    }
    //父类的成员属性
    call(){
        console.log("我可以打电话!!");
    }
}

class SmartPhone extends Phone {
    //构造方法
    constructor(brand, price, color, size){
        super(brand, price);// Phone.call(this, brand, price)
        this.color = color;
        this.size = size;
    }

    photo(){
    	console.log("拍照");
    }

    playGame(){
    	console.log("玩游戏");
    }
	//对父类的方法进行重写，需要注意js不能直接在子类调用父类同名方法
    call(){
        //super()该条语句会报错
    	console.log('我可以进行视频通话');
    }
}

const xiaomi = new SmartPhone('小米',799,'黑色','4.7inch');
console.log(xiaomi);
xiaomi.call();
xiaomi.photo();
xiaomi.playGame();
```

class的set-get

```js
// get 和 set  
class Phone{
    get price(){
        console.log("价格属性被读取了");
        return 'iloveyou';
    }

    set price(newVal){
    	console.log('价格属性被修改了');
    }
}

//实例化对象
let s = new Phone();

// console.log(s.price);
s.price = 'free';
```

#### 2.17数值扩展

```js
//0. Number.EPSILON 是 JavaScript 表示的最小精度
//EPSILON 属性的值接近于 2.2204460492503130808472633361816E-16
function equal(a, b){
    if(Math.abs(a-b) < Number.EPSILON){
        return true;
    }else{
        return false;
    }
}
console.log(0.1 + 0.2 === 0.3);
console.log(equal(0.1 + 0.2, 0.3))

//1. 二进制和八进制
let b = 0b1010;
let o = 0o777;
let d = 100;
let x = 0xff;
console.log(x);

//2. Number.isFinite  检测一个数值是否为有限数
console.log(Number.isFinite(100));
console.log(Number.isFinite(100/0));
console.log(Number.isFinite(Infinity));

//3. Number.isNaN 检测一个数值是否为 NaN 
console.log(Number.isNaN(123)); 

//4. Number.parseInt Number.parseFloat字符串转整数
console.log(Number.parseInt('5211314love'));
console.log(Number.parseFloat('3.1415926神奇'));

//5. Number.isInteger 判断一个数是否为整数
console.log(Number.isInteger(5));
console.log(Number.isInteger(2.5));

//6. Math.trunc 将数字的小数部分抹掉  
console.log(Math.trunc(3.5));

//7. Math.sign 判断一个数到底为正数 负数 还是零
console.log(Math.sign(100));
console.log(Math.sign(0));
console.log(Math.sign(-20000));
```

#### 2.18 对象方法扩展

ES6 新增了一些 Object 对象的方法
	1) Object.is 比较两个值是否严格相等，与『===』行为基本一致（+0 与 NaN）

​	2) Object.assign 对象的合并，将源对象的所有可枚举属性，复制到目标对象

​	3) __proto__、setPrototypeOf、 setPrototypeOf 可以直接设置对象的原型

```js
//1. Object.is 判断两个值是否完全相等 
console.log(Object.is(120, 120));// === 
console.log(Object.is(NaN, NaN));// true
console.log(NaN === NaN);// false 

//2. Object.assign 对象的合并
const config1 = {
    host: 'localhost',
    port: 3306,
    name: 'root',
    pass: 'root',
    test: 'test'
};
const config2 = {
    host: 'http://atguigu.com',
    port: 33060,
    name: 'atguigu.com',
    pass: 'iloveyou',
    test2: 'test2'
}
console.log(Object.assign(config1, config2));

//3. Object.setPrototypeOf 设置原型对象  Object.getPrototypeof
const school = {
	name: '尚硅谷'
}
const cities = {
	xiaoqu: ['北京','上海','深圳']
}
Object.setPrototypeOf(school, cities);
console.log(Object.getPrototypeOf(school));
console.log(school);
```

#### 2.19 模块化

模块化是指将一个大的程序文件，拆分成许多小的文件，然后将小文件组合起来。

##### 2.18.1 模块化的好处

模块化的优势有以下几点：

​	1) 防止命名冲突

​	2) 代码复用

​	3) 高维护性

##### 2.18.2 模块化规范产品

ES6 之前的模块化规范有：

​	1) CommonJS => NodeJS、Browserify

​	2) AMD => requireJS

​	3) CMD => seaJS

##### 2.18.3 ES6 模块化语法

模块功能主要由两个命令构成：export 和 import。

- export 命令用于规定模块的对外接口
- import 命令用于输入其他模块提供的功能

使用方式1：

 ![](C:\资料备份\学习笔记\01-Web笔记\101-Node.js\02-项目实战\media\2022-08-09_160809.png)

使用方式2：

 ![](C:\资料备份\学习笔记\01-Web笔记\101-Node.js\02-项目实战\media\2022-08-09_160943.png)



### 第3章 ECMASript7新特性



### 第4章 ECMASript8新特性



### 第5章 ECMASript9新特性



### 第6章 ECMASript7新特性



### 第7章 ECMASript7新特性



### 第8章 ECMASript7新特性
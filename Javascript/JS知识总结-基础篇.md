#### Javascript的组成
- Javascript的组成由以下三部分组成

```
ECMAScript（核心）：Javascript语言基础-ECMA标准
DOM（文档对象模型）：规定了访问HTML和XML的接口-W3C标准
BOM（浏览器对象模型）：提供了浏览器窗口之间进行交互的对象和方法。-W3C标准
```

#### JS有哪几种数据类型
1. 值类型:String Number Boolean Null Undefined Symbol

1. 引用类型:Function Array Object

- null和undefined的区别

```
null:空对象指针
undefined:变量声明但未赋值
```

#### typeof判断数据类型
- typeof主要用于判断String number boolean undefined等基本数据类型，也可以判断function类型，但是无法分辨object类型;示例如下：

```
typeof 'abc' -> string
typeof 123 -> number
typeof true -> boolean
typeof undefined  -> undefined
typeof console.log('hello world')  ->  function
typeof null  ->  object
typeof [1,2,3] -> object
typeof {name: 'Jack'} -> object
```

- instanceof可以判断对象类型，主要判断instanceof右边函数的原型是否在instanceof左边对象的原型链上。

#### js有哪些内置函数
- String,
- Number,
- Boolean
- Array,
- Object,
- Function,
- Date,
- Regexp
- Error
- 内置对象：Math、JSON

#### 强制类型转换有几种情况
1. 字符串拼接

```
let a = 100 + 10 // 110
let b = 100 + '10' // 10010
```

2. == 运算符

```
100 == '100' -> true
0 == '' -> true
// 何时使用 ==
因为null == undefined -> true
if(obj.a == null) {
    // 这里相当于 obj.a === null || obj.a === undefined
    // jquery源码推荐写法
    // 其余情况建议使用===
}
```

3. if语句

```
let a = true;
if(a) {
    console.log('123');
}

let b = 1;
if(b) {
    console.log('456');
}

let c = '';
if(c) {
    console.log('789');
}
```

4. 逻辑运算

```
console.log(10 && 0) -> true
console.log('' || 'edf') -> 'edf'
console.log(!edf) -> true
// 判断一个变量会被当做true或false
let b = 100;
console.log(!!b);
```

#### JSON的了解
- 是js内置的函数（JSON.stringfy、JSON.parse）
- 是一种轻量级的数据交换格式
- JSON和XML的区别

```
1.JSON体积更小，传递的的速度更快；
2.JSON更易于与javascript进行交互
3.XML对语言的描述性更好

```

#### window有哪些对象
- window.document
- window.navigator
- window.location
- window.history
- window.screen

#### 检测浏览器版本有哪些方式
- navigator.userAgentUA.toLowerCase().indexOf('chrome');
- 'ActiveXObject' in window

#### 堆栈数据结构
> 堆栈数据结构是一种支持后进先出的集合，例如：上电梯、叠盘子。js数组的几个方法可以让我们很方便实现堆栈：

```
shift:从数组中把第一个元素删除，并且返回被删除元素的值
unshift:在数组的开头添加一个或者多个元素，并返回新数组的长度
push:在数组的末尾添加一个或者多个元素，并返回新数组的长度
pop:从数组中把最后一个元素删除，并且返回被删除元素的值
```

#### 回调函数
> 回调函数是一个通过函数指针调用的函数，一般是将回调函数作为参数传给另一个函数，并且在该函数中执行。

#### 异步编程有哪几种方式，并且说下每种方式的优缺点
1. 回调函数：优点是简单、容易理解，缺点是不利于代码的维护，各个部分高度耦合，流程混乱，而且每个异步任务只能指定一个回调函数(回调地狱)。
2. 事件监听：优点是可以绑定多个事件，每个事件可以指定多个回调函数，而且去耦合，有利于实现模块化编程；缺点是整个程序都会变成事件驱动型，运行流程不清晰。
3. 发布/订阅，性质与事件监听类似，但是明显优于事件监听。
4. Promise对象：Promise是CommonJS工作组提供的一种规范，它让每个异步任务返回一个Promise对象，该对象有个then方法，通过链式调用指定不同的回调函数，结构清晰、利于阅读和维护,流程也会变得很清晰。

#### 对Promise的理解
> Promise对象接收一个函数，并向函数传递两个参数（resolve、reject）,分别对应异步操作执行成功后的回调函数和操作执行失败后的回调函数。
- Promise缺点：

```
1.一旦执行就无法终止
2.在pending状态时，无法得知执行成功还是失败
```

#### 什么是自执行函数？用于什么场景？有什么好处？
> 自执行函数：声明一个匿名函数，马上调用这个匿名函数。
- 好处：创建一个独立的作用域，防止变量对全局造成污染
- 场景：一般用于开发框架、插件。

#### window.onload和DOMContented之间的区别
- window.onload是在页面加载完成的时候才执行，包括图片等元素的加载。
- DOMContented是在DOMtree构建完后执行，因为有时候图片加载缓慢，不需要等到页面加载完成才触发事件。

#### 堆栈溢出和内存泄露
- 堆栈溢出：不顾堆栈中分配的局部数据块的大小，而向该数据块写入了过多的数据，导致数据越界覆盖了别的数据块中的数据，经常在递归中发生。
- 内存泄漏：指内存空间在使用完成后未释放，导致一直占据内存。
- 造成内存泄露的原因：

```
1.seeTimeout第一个参数是字符串而非函数
2.闭包
3.控制台日志
4.循环（两个对象的相互引用）
```

#### 什么是移动端点击穿透
> 移动段点击穿透有三种情况

1. 点击蒙层的关闭按钮，蒙层消失后触发了关闭按钮下边元素的click事件；
2. 跨页面点击穿透，如果关闭按钮下边是个带有href属性的a标签，那么页面就会跳转；
3. 非蒙层，点击页面按钮跳转至新的页面，触发了新页面同样位置元素的click事件。

- 最佳解决方案：只用touch

#### 什么是移动端300ms延迟
> 移动端300ms延迟：当用户点击浏览器里的一个链接，由于用户可以进行双击缩放和双击滚动操作，当用户点击屏幕一次后，浏览器无法立刻判断用户是想打开这个链接还是进行双击操作，因此浏览器就等待300ms后判断用户是否再次点击了屏幕。

#### git和svn的区别
- svn是集中版本控制系统，版本库是集中放在中央服务器上的。缺点：必须联网才能工作，网速比较慢的时候，影响开发。
- git是分布式版本控制系统。

#### 对ajax的理解和ajax的执行流程
> ajax：数据持久化技术，通过ajax请求后端数据而实现前端页面的局部刷新。
- 代码示例
```
let xhr = null;
if(XMLHttpRequest) {
    xhr = new XMLHttpRequest
} else {
    xhr = new ActiveXObject('Microsoft.XMLHTTP')
}
xhr.open(method,url,flag); // 初始化请求
xhr.setRequestHeader(); // 设置请求头信息
xhr.onreadystatechange = function(res) {
    if(res.readyState == 4) {
        if(res.status = 200) {
            console.log(res.resposeText);
        }
    }
}； // 指定回调函数
xhr.send(); // 发送请求
```
- ajax的执行流程

```
0：未初始化，还未调用send方法
1：发送，已调用send方法，正在发送请求
2：发送完成，send方法执行完成，已接受到全部响应内容
3：交互，正在解析响应内容
4：完成，响应内容解析完成，可以在客户端调用
```

#### ajax和jsonp的区别
- 相同点：都是请求一个url;
- 不同点：ajax的核心是通过xmlHttpRequest对象来获取内容的；jsponp的核心则是动态创建<script>标签来调用服务器提供的js脚本。
- ajax缺点：

```
1.不支持浏览器back返回
2.安全问题：暴露了与服务器交互细节
3.对搜索引擎支持较弱
4.破坏了程序的异常机制
5.不容易调试
```

- jsonp的缺点：只支持GET请求，是一种脚本注入行为，存在安全风险，如果返回失败并不会报错。

#### 有哪几种跨域方式
- jsonp
- iframe
- postMessage
- fetch
- webSocket

#### Gc机制是什么？为什么闭包不会被回收？
> Gc:垃圾回收机制（分为标记清除法和计数清除法）
> 闭包不会被回收是因为闭包引用的外部变量未得到释放，导致包含此变量的外部函数无法得到释放，那么函数内的函数也就无法被回收。

#### 如何确保ajax不走缓存路线
- url后边加上上ranNum:Math.random()生成一个随机数字，拼接在url后边；
- url后边加上时间戳；
- 设置control-cache:no-store

#### sessionStorage、loaclStorage和cookie之间的区别
1. cookie在客户端和服务器端来回传递，浪费带宽，而sessionStorage、loaclStorage仅在浏览器本地保存；
2. cookie存量小，不能超过4k，而sessionStorage、loaclStorage存量可达到5M;
3. cookie在设置过期时间之前一直有效，即使窗口关闭；sessionStorage在窗口关闭后清除；而loaclStorage可以永久保存。
4. 在不同浏览器打开同源窗口，cookie和localStorage数据可以共享，而sesionStorage数据不可以共享。

#### 模块化
- AMD:异步加载模式，在Require推广过程中产生；依赖前置
- CMD:SeaJS在推广过程中产生；依赖就近
- UMD:通用模式，用于解决跨平台，先判断是否支持CommonJs模式
- CommonJs:NodeJs是这种规范的实现，因为js没有模块功能，所以CommonJs应运而生，但是不能再浏览器运行；require module.export
- ES6:import export

#### Javascript垃圾回收机制
- 标记清除
> 当变量进入执行环境的时候，比如函数中声明一个变量，垃圾回收器将其标记为“进入环境”，当变量离开环境的时候（函数执行结束）将其标记为“离开环境”。垃圾回收器会在执行的时候给存储在内存中的所有变量加上标记，然后去掉环境中的变量已经被闭包所引用的变量，然后将剩下仍存在标记的变量清除掉。
- 引用计数
> 引用计数的策略就是跟踪记录每个值被使用的次数。当声明了一个变量并将一个引用类赋值给该变量的时候，这个值的引用次数就加1，如果该变量的值重新赋值给另外一个值，则这个值的引用次数减1，当该值的引用次数变为0的时候，说明没有变量在使用该值，这个值不再访问了，因此可以将其占有的空间用垃圾回收器回收。

#### Javascript的同源策略

> 同源策略是一种安全协议，指协议、域名、端口相同。指一段脚本只能读取来自同一来源的窗口和文档属性。
- 为什么要用同源限制
> 举例说明：比如一个黑客程序，他利用iframe把真实的银行登录页面嵌到他的页面上，当你使用真实的用户名和密码登录时，他的页面就可以通过js读取你的表单内容，这样你的用户名和密码就被盗取了。

#### 函数声明提升和变量声明提升的区别
> js引擎在执行上下文的时候会将变量声明和函数声明提升到作用域的顶部。在js中函数为第一等公民，若声明的变量名和函数名相同，函数会覆盖变量。

#### 作用域
- js作用域分为函数作用域和全局作用域。

```
// 无块级作用域
if (true) {
    var name = 'liubang';
}
console.log(name) -> liubang

// 函数和全局作用域
var a = 10;
function fo() {
    var a = 11;
    console.log('fn', a)
}
console.log('global', a) -> global 10
fo(); -> fn 11
```

- 执行上下文
1. 范围：一段<script>或者一个函数
2. 全局执行上下文：变量定义、函数声明（一段<script>）
3. 函数执行上下文：变量定义、函数声明、this、argument（一个函数）
4. js在执行上下文的时候，会将this、argument、变量定义、函数申明提升到作用域的顶部（函数为第一等公民，若变量名和函数名重复，函数名会覆盖变量名）

```
// 例子
console.log(a) // undefined
var a = 10

fo('liubang') // 'liubei' 20
function fo(name) {
    age = 20
    console.log(name, age)
    var age
}
```

- 作用域链：在所在函数作用域内找不到自由变量，则向父级作用域(定义该函数的作用域)去查找。

```
var a = 10;
function fo1() {
    var b = 20;
    function fo2() {
        var c = 30;
        // 当前作用域没有定义的变量，即‘自由变量’
        console.log(a)
        console.log(b)
        console.log(c)
    }
    fo2()
}
fo1();
```

#### 什么是闭包？闭包的优缺点
> 闭包：就是能够读取函数内部变量的函数。

- 闭包的使用场景

```
1.函数作为返回值

    function Fo1() {
        var a = 10;
        
        // 函数作为返回值
        return function() {
            console.log(a)
        }
    }
    var f1 = Fo1();
    var a = 20;
    f1() -> 10

2.函数作为参数传递

    function Fo1() {
        var a = 10;
        
        return function() {
            console.log(a) // a是自由变量，去父作用域查找
        }
    }
    var f1 = Fo1();
    
    function Fo2(fn) {
        var a = 20;
        fn()
    }
    Fo2(f1); -> 10
```
- 闭包应用实例

```
实例一：创建10个<a>标签，点击的时候弹出对应标签的序号

// 错误写法
var i,a;
for(i = 0; i < 10; i++) {
    a = document.createElement('a')
    a.innerHtml = i + '<br>'
    a.addEventListener('click', function(e) {
      e.prevetDefault()
      alert(i)
    })
} -> 弹出的都是9

// 正确写法
var i;
for(i = 0; i < 10; i++) {
    (function(i){
        var a = document.createElement('a')
        a.innerHtml = i + '<br>'
        a.addEventListener('click', function(e) {
          e.prevetDefault()
          alert(i) // i作为参数传递到自执行函数作用域中
        })
    })(i)
}

实例二：封装变量，收敛权限
function isFirstLoad() {
    var _list = []
    return function (id) {
        if(_list.indexOf(id) >= 0) {
            return false
        } else {
            _list.push(id)
            return true
        }
    }
}

var firstLoad = isFirstLoad()
firstLoad(10) // true
firstLoad(10) // false
firstLoad(20) // true
```

- 优点：

```
1.设计了私有变量和方法，避免了全局变量的污染
2.使得闭包所引用的变量一直保存在内存中
```
- 缺点：

```
1.由于闭包引用外部变量，就导致变量所在的函数一直保存在内存中，而无法得到释放，使用不当会导致内存泄露。
```
[详见：为什么要使用闭包](https://blog.csdn.net/caimouse/article/details/78076457)

#### this的有几种指向
> 只有在函数被执行的时候才可以确认this的指向，this指向调用函数的那个对象。分为以下几种情况：

- 作为普通函数被调用（包括匿名函数）

```
let name = 'Mack'; 
function person() {
    let name = 'Jack';
    console.log(this.name );
    console.log(this);
}
person(); 
// this指向window
```

- 作为对象的方法被调用

```
let obj1 = {
    name: 'Jack',
    say: function() {
        console.log(this.name)
        console.log(this);
    }
}

obj1.say();
-> Jack
-> {name: "Jack", say: ƒ}
```


- 指向构造函数的实例

```
function Foo (name,age) {
    this.name = name;
    this.age = age;
    console.log(this);
}

let foo1 = new Foo('Jack', 11);
-> Foo {name: "Jack", age: 11}
```

- 指向call、apply和bind第一个参数

```
let obj3 = {
    name: 'Jack',
    say: function () {
        console.log(this);
    }
}
let obj4 = {
    name: 'Rub',
    age: 25
}

obj3.say.call(obj4);
-> {name: "Rub", age: 25}
```

#### javascript代码规范
- 1.代码缩进；
- 2.语句结束用双引号；
- 3.语句块用花括号包起来；
- 4.函数变量在使用前声明；
- 5.构造函数第一个字母大写；
- 5.用字面量创建数组或者对象；
- 6.规范化Json对象，补齐双引号；

#### 如何写出高性能javascript
- 1.js脚本引用放在页面的底部；
- 2.js分组打包，减少http请求；
- 3.使用局部变量引用全局变量；
- 4.引用window属性和方法时，去掉window；
- 5.使用字面量创建数组和对象；
- 6.缓存Dom结点的访问；
- 7.避免使用Eval和Function构造函数；
- 8.避免使用闭包；
- 9.settimout和setinterval第一个参数使用函数而不使用字符串；
- 10.避免页面重排和重绘

#### 前端性能优化
- 减少http请求
- 资源压缩和合并
- dns预请求
- 浏览器缓存
- 异步加载js（jsonp、defer、async）
- 将静态资源放在CDN上
- 预加载和懒加载
- 将css文件放在html头部
- 将js文件放在html底部
- 雪碧图

#### 如何合并两个数组
- 方法一

```
let arr1 = [1,2,3];
let arr2 = [4,5,6];
arr1 = arr1.concat(arr2)
```
- 方法二

```
let arr1 = [1,2,3];
let arr2 = [4,5,6];
Array.prototype.push.apply(arr1,arr2);
```

- 方法三

```
let arr1 = [1,2,3];
let arr2 = [4,5,6];
for(let i=0; i<arr2.length; i++){
    arr1.push(arr2[i])
}

```

#### 获取多少位随机字符串

```
function randomStr(num) {
    let random = Math.random();
    random += '0000000000';
    random = random.slice(0, num);
    return random
}
```

#### 程序的设计模式

#### 说说你遇到的比较难得技术问题，是如何解决的?
















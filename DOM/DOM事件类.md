#### DOM事件的级别

```
DOM0 element.onclick = function(){}
DOM2 element.addEventListener('click',function(){},false)
DOM3 element.addEventListener('keyup',function(){},false)

为什么没有DOM1？
答：因为w3c在制定DOM1标准的时候，没有定义事件相关的东西
```

#### DOM操作（添加、移除、移动、复制、创建和查找节点）
- 创建新节点
    
```
createDocumentFragment() // 创建一个DOM片段
createElement() // 创建一个元素
createTextNode() // 创建一个文本节点
```
- 添加、移除、替换、插入

```
appendChild()
removeChild()
replaceChild()
insertBefore()
```
- 查找节点

```
getElementsByTagName() // 通过标签名查找
getElementsByClassName() // 通过class查找
getElementById() // 通过唯一ID查找
```

#### DOM事件模型

- 捕获
- 冒泡

#### DOM事件流

```
捕获 -> 目标阶段 -> 冒泡
```

- 描述DOM事件捕获的具体流程

```
捕获阶段  window -> document -> html -> body -> 目标元素
冒泡阶段  目标元素 -> body -> html -> document -> window

获取body元素：document.body
获取html元素：document.documentElement
```

#### 事件委托？有什么好处？
> 事件委托：利用冒泡的原理，将原本要发生在子元素上的事件绑定到父元素上。好处：提高性能。

#### Event对象的常见应用

```
event.preventDefault() // 阻止默认事件，例如阻止a标签的默认跳转
event.stopPragation() // 停止冒泡，防止父元素上绑定的事件触发
event.stopImmediateProgagation() // 一个元素上绑定了两个事件，如果只想触发其中一个事件的时候，使用此方法
event.currentTarget // 绑定事件的元素
event.target // 点击的元素
```

#### 自定义事件

```
方法一：

let ev1 = new Event('cat');
dom1.addEventListener('cat', function(e){
    console.log(e)
})
dom1.dispatchEvent(ev1);

方法二：可以传递数据

let eve2 = new CustomEvent("cat", {
  detail: {
    hazcheeseburger: true
  }
});
dom2.addEventListener("cat", function(e) { process(e.detail) });
dom2.dispatchEvent(eve2);
```


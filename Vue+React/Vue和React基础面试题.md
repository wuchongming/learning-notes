
#### 说一下使用jquery和使用框架的区别

    1.数据和视图的分离
    
        解耦（开放封闭原则）
    
    2.以数据驱动视图
    
        框架只改数据，不关心视图；jquery直接修改视图
        
#### 说一下MVVM的理解

    1.MVC
    
    2.MVVM
    
        MVVM不算是一种创新，但其中的ViewModel确实是一种创新
    
    3.关于ViewModel
    
#### MVVM框架三大要素    

    1.响应式：vue如何监听到data的每个属性的变化
    
    2.模板引擎：vue的模板如何被解析，指令如何处理
    
    3.渲染:vue的模板如何被渲染成html，以及渲染过程

#### v-if和v-show的区别
- v-if动态渲或销毁元素，一次性或更新不频繁的场景使用
- v-show显示或隐藏元素

#### 为何v-for中要使用key
- v-for和v-if不可以同时使用，v-for优先级比v-if高
- 不建议key使用跟业务无相关的id和index
- diff算法，就地复用策略，最小化更新Dom，例如向列表中插入数据，如无key，则会更新插入的那条数据后面所有的节点，若有key值，只需更新
插入的那条数据

#### 自定义v-model
- 颜色选择器使用

```
model: {
    
}
```

#### $nextTick
- Vue是异步渲染
- data改变之后，Dom不会立刻渲染
- $nextTick会在在Dom渲染之后触发，以获取最新Dom节点
- 页面渲染时会将data的修改做整合，多次data修改只会修改一次

#### slot
- 作用域插槽 v-slot= 子组件向父组件传递数据
- 具名插槽 v-slot:

#### 异步组件
- 按需加载，异步加载大组件

```
components: {
    FormDemo: () => import('../BaseUse/FormDemo')
}
```

#### keep-alive
- 缓存组件
- 频繁切换，不需要重复渲染

#### minxin
- 多个组件有相同的逻辑，抽离出来
- 缺点：变化来源不明确，不利于阅读
- 多minxin可能会造成命名冲突
- minxin对组件可能出现多对多的情况，复杂度较高
- Vue3的Composite Api旨在解决minxin不完美的问题

#### 描述Vue组件生命周期（有父子组件的情况）
- 挂载阶段 

```
created:父组件要先于子组件实例化
mounted:子组件要先于父组件渲染完成
```

- 更新阶段

```
beforeUpdate:父组件要先于子组件更新
updated:子组件要先于父组件更新完成
```

- 销毁阶段

#### Vue组件如何通信
- 父子组件 props、$emit
- 组件之间没有无关系或嵌套很深 自定义事件
- vuex

#### 描述组件渲染和更新的过程
#### 双向数据绑定v-model的实现原理
#### v-html 会有xss风险，v-html内容会覆盖子组件
#### computed和watch区别
- computed有缓存，computed所依赖的data值不变则computed值不会重新计算
- watch监听引用类型值，需要深度监听，并且oldVal和val指向同一个引用值
#### vue事件
- event是原生的
- event被挂载到当前元素上
       

#### vue有哪些导航钩子
> 导航钩子即路由的生命那个周期

    1. 全局的钩子函数
    beforeEach 路由切换时开始调用
    afterEach  路由切换离开时开始调用
    
    2.局部到单个路由（单个路由里配置）
    beforeEnter
    
    3.组件的钩子函数（组件内配置）
    beforeRouterEnter
    beforeRouterUpdate
    beforeRouterLeave
    
#### vue路由懒加载
> 即延迟加载、按需加载，因为大型单页面应用项目中所有的页面都引用一个js，首次加载会非常慢

#### Vue原理
- 组件化和MVVM模型

```
1.很久之前就有了组件化 asp、jsp,传统组件，只是静态渲染，更新依赖于操作Dom

2.数据驱动视图 vue-用MVVM react-用setState
MVVM的核心概念就是数据驱动视图
```

- 响应式

```
1.组件data的数据一旦变化，就会立刻触发视图的更新
2.核心api Object.defineProperty
3.Object.defineProperty有一些缺点，对嵌套很深的对象进行监听，需要递归到底，一次性计算量大；无法监听新增属性和删除属性（所以有Vue.set、Vue.delete），所以vue3使用Proxy；不支持原生监听数组
4.如何监听数组，重写数组原型上的push、pop等方法，在方法中执行视图更新
5.proxy兼容性不好，且无法polyfill
6.proxy的使用 
Reflect.get(target, key, receiver) 
Reflect.set(target, key, val, receiver) 
deleteProperty(target, key)
```

- vdom和diff

```
1.什么是vdom
    1.virtual dom - 虚拟dom
    2.用JS模拟DOM结构，DOM操作非常昂贵
    3.DOM变化的对比，放在JS中来完成（图灵完备语言）
    4.提高页面重绘的性能
    
2. vdom如何应用？核心api是什么
    1.h函数,返回vnode对象
    2.patch(container, vnode) 第一次渲染
    3.patch(vnode, newVnode) 数据修改后再次渲染
    
3. vdom为何使用diff算法
    1.DOM操作非常昂贵，因此应该尽量减少DOM操作
    2.找出本次DOM必须要更新的node来更新，其它的不更新
    3.这个找出的过程，就需要diff算法
    4.时间复杂度O（n）
    5.只比较同一层；
    6.tag不相同，直接删掉重建，不再深度比较
    7.tag和key相同，则认为是相同节点，不再深度比较
    
4. diff算法的实现
    1.patch(container, vnode) 第一次渲染
    2.patch(vnode, newVnode) 数据修改后再次渲染
    
```

- 模板编译

```
    1.模板是什么
        
        本质：字符串
        
        有逻辑，如 v-if、v-for指令
        
        与html格式很像，但是区别很大
        
        模板最终要转换为html来显示
        
        模板最终必须转换成js代码，因为：有逻辑（v-if）,必须用js才能实现；转换成html页面，必须用js才能实现。因此，模板最终转换成js函数（render函数）
    
    2.vue template complier将模板编译成render函数
    
    3.执行render函数生成vdom
    
    4.基于vnode再执行patch和diff
    
    5.使用 vue-loader,会在开发环境下编译模板
    
```

- 组件渲染更新过程

```
    1.模板编译
    
        解析模板为render函数（或在开发环境通过vue-loader已经编译完成）
        
    2.响应式
    
        Object.defineProperty将data数据代理到vm中，监听data属性getter、setter

    3.执行render函数，生成vnode，执行patch(container,vnode)渲染
    
    4.模板更新
        
        改变data数据，通过set执行updateComponent(rerender)
        
    5.重新执行render函数，生成newVnode
    
    6.执行patch(oldVnde,vnode)渲染
```

- 前端路由


#### React组件如何通信
#### JSX的本质
#### Context是什么，如何应用
#### shouldComponentUpdate的用途
#### 描述redux单向数据流
#### setState是同步还是异步
 
#### redux中间件原理
    改装dispatch,是action与store之间沟通的桥梁，如果action是个函数，可将action转换成对象
    
#### 你会把数据统一放在redux中管理，还是把共享数据放在redux中管理
    1.从快速定位问题角度看，建议把所有数据放在redux中统一管理，只需要在store中定位问题，不需要去state、props中去检查代码。
    2.从项目的可维护性角度看，随着项目的日益庞大，组件不断扩展，父子组件、兄弟组件和跨界组件之间的通信将变得越发困难和混乱。
    3.redux可存储5G的数据，不用担心内存占用问题
    4.redux与immutable库结合使用，可将页面性能达到最优
    
#### componentWillReceiveProps（已废弃）的调用时机
    props改变的时候被调用，父组件向子组件第一次传递数据的时候不会被调用
    
#### react性能优化最佳实践
    React.pureComponent与immutable.js库结合使用,pureComponent自带了shouldComponentUpdate钩子函数的props前比较，如果props值没有改变，则不会触发组件的更新;
    
#### webpack中，是借助loader完成JSX代码的转换，还是babel
    1.React没有类似vue-loader的转换器将JSX代码进行转换;
    2.而是借助babel-preset-react进行转换的;
    
#### 调用setState后发生了什么
    调和函数，rerender组件
- 一般写法

``` 
// 特殊场景：连续点击按钮，值会出现跳跃性，因为React会将多个setState组合
this.setState({
    count: ++ this.state.count
})

```

- 官方建议的写法，不会出现坑
    
```
this.setState((prevState) => {
    count: ++ prevState.count
})
```

#### setState是异步的，你遇到过什么坑
    在setState后面获取dom的值或者state里的值不是最新的，需要在回调函数里获取
    
#### ref的作用是什么？什么场景下会使用
    1.图片放大镜功能，需要获取图片的宽高
    
#### ref函数是什么
    
```
// 推荐写法
// 好处：便于React在组件销毁、重新渲染的时候清空refs引用的东西，防止内存泄露
Class Test extends Component {
    componentDidMount() {
        // 可以直接获取div对应的元素
        console.log(this.elem)
    }
    
    render() {
        return <div ref={div => {this.elem = div}}></div>
    }
}
```

#### 高阶组件本质是什么
    1.React设计模式：组合大于继承
    2.通过接收一个组件，返回包装后的新组件
    3.本质是一个函数
    4.问题：嵌套层次太多，会出现高阶组件地狱；解决办法：使用Hook

#### 受控组件和非受控组件之间的区别
    受控组件优于非受控组件，因为React是个数据驱动视图的框架
    
```
// 受控组件
// inputValue值不改变，input输入框的值就不会改变
<input value={this.state.inputValue} />

// 非受控组件
// 通过ref获取dom值
<input ref='inputValue' />
```

#### 函数组件和Hooks

#### this指向问题一般怎么解决
    1.箭头函数，作用域链(向父级作用域找this)
    2.bind,在constructor中处理
    
#### 函数组件如何做性能优化
    
```
function Test(props){
    return <div>hello world</div>
}
// React.memo()封装，自带shouldComponentUdate功能，并且没有普通组件的生命周期
    
```

#### 在那个生命周期里发送Ajax请求
    1.componentDidMount钩子里去发
    2.componentWillMount在React新版本被废弃了
    3.SSR项目中，componentWillMount用作服务器端数据的获取，不能被占用
    
#### SSR原理是什么
    服务器端渲染，因为虚拟DOM可以在Node环境中执行
    
#### redux-saga的设计思想是什么？什么是sdeEffects

#### jquery、react和vue是否有可能共存在一个项目中
    可以共存，分别挂载到不同的dom上即可。
    
#### 模块是什么？组件是什么？类是什么？类被编译成什么？
    模块是webpack引入的一个个文件
    组件指的是页面的一部分
    类本质是个构造函数
    类被编译成构造函数
    
#### 你是如何跟着社区成长的
    面试是想了解你是如何学习新技术的，以及对新技术的了解
    比如用twitter关注React官方团队，第一时间收到最新消息
    
#### 如何避免ajax数据重新获取
    用redux进行状态管理
    
#### react-router4的核心思想是什么？和3有什么区别
    react-router4将路由变成了组件，通过<Link /> <Route />
    等组件的方式进行页面跳转，不需要再放在一个路由文件进行配置,变得非常的灵活。
    
#### reselect是做什么的
    类似vue中computed功能（所依赖的数据没有发生变化，则computed的数据也不会发生变化）
    
#### react-router的基本原理？hashHistory、browerHistory
    hashHistory前端自身就可以实现
    browerHistory依赖后端服务器配置才可以使用
    
#### 什么情况下使用异步组件
    即懒加载，参考Reloadable库

#### React是如何防范xss攻击的
- dangerouslySetInnerHTML函数不会对标签进行过滤，慎用

```
dangerouslySetInnerHTML = {{_html:'<script>alert(1)</script>'}}
```

#### getDerivedStateFromProps新钩子
    父组件传递给子组件的props发生变化的时候就会执行getDerivedStateFromProps钩子函数，替代即将被废弃的componentWillReceiveProps钩子函数
    
#### immutable.js和redux最佳实践
    

#### event
- event是syntheticEvent合成事件，模拟出来的Dom事件
- event.nativeEvent是原生事件对象
- 所有的事件都委托到document上挂载
- 和Dom事件不一样，也和Vue事件不一样

#### 受控组件和非受控组件之间的区别
受控组件优于非受控组件，因为React是个数据驱动视图的框架

```
// 受控组件 类似于v-model
// inputValue值不改变，input输入框的值就不会改变
<input value={this.state.inputValue} />

// 非受控组件
// 通过ref获取dom值
<input ref='inputValue' />
```

#### 组件通信
- 父子通信：props传递属性、函数
- 无关系或者嵌套深：Provider、Consumer
- Redux

#### 组件的生命周期
- 挂载时

```
constructor
render
更新Dom和refs
componentDidMount
```

- 更新时

```
New props setState forceUpdate
shouldComponentUpdate
render
更新Dom和refs
componentDidUpdate
```

- 销毁时

```
componentWillUnmount
```
父子组件生命周期和Vue一样

#### setState
- 不可变值
不能直接修改state的值

- 可能是异步更新

```
// 在setTimeout中setState是同步的
setTimeout(() => {
    this.setState({
        count: this.state.count + 1
    })
    console.log(this.state.count)
}, 0)

// 自定义的DOM事件,setState是同步的
bodyClickHandler() {
    this.setState({
        count: this.state.count + 1
    })
    console.log(this.state.count)
}
componentDidMount() {
    document.body.addEventListener('click', this.bodyClickHandler)
}

```

- 可能会被合并

```
传入函数不会被合并
```

#### Portals（传送门）
- 组件默认按照既定层次嵌套渲染
- 如何让组件渲染到父组件之外

```
ReactDOM.createPortal(
    <div className="modal">{this.props/children}</div>,
    document.body
)

.modal {
    position: fixed
}
```
- 使用场景

```
1.overflow：hiddren等BFC场景，将子组件逃离父组件
2.父组件z-index太小
3.fixed需要放在body第一层
```

#### 异步组件
使用场景：组件体积较大，路由中需要懒加载异步组件
- React.lazy
- React.Suspense

```
const ContextDemo = React.lazy(() => import('./ContextDemo'))

return(
    <React.Suspense fallback={<div>loading...</div}>
        <ContextDemo />
    </React.Suspense
)
```

#### 性能优化
- shouldComponentUpdate

```
SCU默认返回true
为何React框架自己不处理SCU,而让使用者去定制
因为React默认：父组件更新，子组件也无条件更新（即使子组件内容没有改变）

// 如果开发者用使用不规范写法，直接改变了state值
shouldComponentUpdate则会返回false（即使深度比较）,就会出现bug
所以react不直接处理shouldComponentUpdate

this.state.list.push({
    id: `id-${Date.now()}`,
    title
})
this.setState({
    list: this.state.list
})
```


- pureComponent（纯组件）和React.memo

```
pureComponent在shouldComponentUpdate中实现浅比较，因为深度比较耗费性能，结合state不可变值使用
memo-函数组件中的pureComponent
```

- 不可变值 immutable.js

```
彻底拥抱不可变值
基于共享数据（非深拷贝），速度较快
不要学习成本，按需使用
```
#### 公共逻辑的抽离
- mixin 已被React弃用
- 高阶组件（HOC-High Order Conponet）

```
类似于工厂函数，接受一个组件作为参数，返回加工后的新组件
react-redux的connect就是一个高阶组件
```

- render props

```
将render函数当成props传递
```
#### redux
- 单向数据流

```
dispath(action)
reducer-newState
subscribe触发更新
```

- react-redux

```
连接redux
Provider
connect
```

- 异步action

```
异步操作action,需要引用redux-thunk等中间件
```

- 中间件 redux-thunk redux-saga

```
改造dispatch
```

#### 为何要合成事件机制
- 跨平台兼容性
- 挂载到document上，减少内存消耗，避免频繁绑定
- 方便事件的统一管理

#### 组件更新两个阶段
- reconciliation阶段-执行diff算法
- commit阶段，将diff结果渲染Dom

#### fiber
- JS是单线程，和DOM渲染公用一个线程
- 当组件足够复杂，组件更新时计算和渲染压力很大
- 同时再有Dom操作需求（动画、鼠标拖拽等），将卡顿
解决方案
- 将reconciliation阶段进行任务拆分（commit无法拆分）
- DOM需要渲染时暂停，空闲时恢复
- window.requestIdleCallback API可以知道哪些DOM需要渲染，浏览器若不支持此API，fiber方案也无法使用

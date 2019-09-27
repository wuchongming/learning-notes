#### 什么是vdom
    1.virtual dom - 虚拟dom
    2.用JS模拟DOM结构，DOM操作非常昂贵
    3.DOM变化的对比，放在JS中来完成（图灵完备语言）
    4.提高页面重绘的性能
    
#### vdom如何应用？核心api是什么
    1.h函数
    2.patch(container, vnode) 第一次渲染
    3.patch(vnode, newVnode) 数据修改后再次渲染
    
#### vdom为何使用diff算法
    1.DOM操作非常昂贵，因此应该尽量减少DOM操作
    2.找出本次DOM必须要更新的node来更新，其它的不更新
    3.这个找出的过程，就需要diff算法
    4.key值相同，节点直接复用，不用重新创建
    
#### diff算法的实现
    1.patch(container, vnode) 第一次渲染
    2.patch(vnode, newVnode) 数据修改后再次渲染
    
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
    
#### vue中如何实现响应式

    1.什么是响应式
    
    2.Object.defineProperty
    
    3.模拟，将data的属性代理到vm上（也是应用Object.defineProperty）
    
#### vue中如何解析模板

    1.模板是什么
        
        本质：字符串
        
        有逻辑，如 v-if、v-for指令
        
        与html格式很像，但是区别很大
        
        模板最终要转换为html来显示
        
        模板最终必须转换成js代码，因为：有逻辑（v-if）,必须用js才能实现；转换成html页面，必须用js才能实现。因此，模板最终转换成js函数（render函数）
    
    2.render函数
    
    3.render函数与vdom
    
### vue的完整流程
    1.模板解析
    
        首次页面渲染,创建vdom,打包时执行render函数
    
    2.响应式
    
        Object.defineProperty
    
    3.data数据代理到vm中
    
    4.模板渲染
        
        改变data数据，通过set执行updateComponent(rerender)
        
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
    

    
    


#### 诞生背景

随着移动互联网的普及，用户对手机越来越依赖，他们需要浏览网页时也达到App的体验效果，于是SPA应运而生。

#### 什么是SPA？

答：single page application 单页面应用，所有的功能都是在一个页面完成的，传统的PC端页面是通过a链接进行跳转的。单页的体验类似于native app(原生app，底部有导航栏，页面上很多内容被复用)的体验。

#### 如何实现SPA

- 锚点(hash) window.onhashchange，当 一个窗口的 hash （URL 中 # 后面的部分）改变时就会触发 hashchange 事件，就可以动态加载内容。
- h5(history)
- ajax可以，但不能记录浏览历史
- iframe框架集，例如mint-ui官网里的手，其实就是用iframe嵌套了一个网页。(但是SEO不友好，操作不方便，可能要被废除)

#### react-router是什么
答：是第三方为react开发单页应用而开发的一个库。

#### react-router的使用
[官方文档：reacttraining.com/react-router](https://reacttraining.com/react-router/web/guides/quick-start)

##### BrowserRouter、HashRouter、Route、Link

```
import {
  BrowserRouter as Router,
  Switch,
  Route,
  Link
} from "react-router-dom";
```
-  react-router提供了两个路由的容器：BrowserRouter、HashRouter，所有的路由操作都必须定义在该组件下面
-  HashRouter是用锚点实现SPA
-  BrowserRouter是用h5-history实现的SPA
-  上线后使用BrowserRouter，这种pathinfo模式的地址更加利于SEO
-  对于搜索引擎来说，任何hash都不是一个新的URL，搜索引起就不会将其收录

-  Route：路线的意思，该组件用来定义路径和显示组件的对应关系

- Link：实际就是a链接，实现声明式跳转（区别于函数式跳转）


##### children func
路由切换中，children属性都会执行，如果路径不匹配，route属性match就会返回null;通过它可以封装Link组件，实现一些样式激活、动画效果等。

```
import React from "react";
import ReactDOM from "react-dom";
import {
  BrowserRouter as Router,
  Link,
  Route
} from "react-router-dom";

function ListItemLink({ to, ...rest }) {
  return (
    <Route
      path={to}
      children={({ match }) => (
        <li className={match ? "active" : ""}>
          <Link to={to} {...rest} />
        </li>
      )}
    />
  );
}

ReactDOM.render(
  <Router>
    <ul>
      <ListItemLink to="/somewhere" />
      <ListItemLink to="/somewhere-else" />
    </ul>
  </Router>,
  node
);

// This could also be useful for animations:
<Route
  children={({ match, ...rest }) => (
    {/* Animate will always render, so you can use lifecycles
        to animate its child in and out */}
    <Animate>
      {match && <Something {...rest}/>}
    </Animate>
  )}
/>
```

##### render func

路径匹配的时候就会执行render（函数式组件）,其接受的routeProps 包含hsitory(函数式跳转用)、match(路由传参用)、location等信息。

```
import React from "react";
import ReactDOM from "react-dom";
import { BrowserRouter as Router, Route } from "react-router-dom";

// convenient inline rendering
ReactDOM.render(
  <Router>
    <Route path="/home" render={() => <div>Home</div>} />
  </Router>,
  node
);

// wrapping/composing
// You can spread routeProps to make them available to your rendered Component
function FadingRoute({ component: Component, ...rest }) {
  return (
    <Route
      {...rest}
      render={routeProps => (
        <FadeIn>
          <Component {...routeProps} />
        </FadeIn>
      )}
    />
  );
}

ReactDOM.render(
  <Router>
    <FadingRoute path="/cool" component={Something} />
  </Router>,
  node
);
```

##### 使用hash(hashchange)原生的方式去实现一个SPA

1. 当地址栏hash改变的时候，会自动触发

```
window.hashchange = () => {
    console.log(location.hash)
    // 根据拿到的hash值，去加载对应的页面内容
    const hash = location.hash.sunstr(2) // 截掉前面的/#
    const html
    if (hash === 'home') {
        // 网络请求，加载home页面内容
        html = 'home页面内容'
    }
    
    document.querySelector('#container').InnerHTML = html
}
```

2. 或在body上绑定事件

```
<body onhashchange="funcRef();">
```


3. 若body上还绑定了别的事件，为了不覆盖掉已绑定的事件，可以使用函数 "addEventListener"。

```
window.addEventListener("hashchange", funcRef, false);
```

##### 嵌套路由和路由参数

##### 编程式导航

##### exact: bool(精准匹配)
- react-router在匹配路由的时候是从上到下完全的匹配，例如/home,就会渲染出/和/home两个路径下的页面内容。
- 如果要精准匹配，就需要加上exact属性。

##### Switch
- react-router在匹配路由的时候,匹配到就停止，不再往下进行匹配
- 包在Route列表外层

```
import { Route, Switch } from "react-router";

let routes = (
  <Switch>
    <Route exact path="/">
      <Home />
    </Route>
    <Route path="/about">
      <About />
    </Route>
    <Route path="/:user">
      <User />
    </Route>
    <Route>
      <NoMatch />
    </Route>
  </Switch>
);
```

##### Redirect


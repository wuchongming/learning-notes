#### Render方法
##### React.render('hello', document.getElementById('root'))
将'hello'字符串渲染到root容器中

#### 安装jquery
用jquery操作dom元素

#### 安装babel
将jsx语法通过babel-plugin-transform插件转换成虚拟dom

```
<div name="JSX">
   hello react JSX<button>child</button>
</div>

babel转换后：

React.createElement(
  "div",
  { name: "JSX" },
  "hello react JSX",
  React.createElement("button", {}, "child")
);

yarn add babel-core babel-preset-env babel-plugin-transform-react-jsx --save-dev
```


#### 为了方便查找到某个元素，需要给每个元素打上唯一标记

```
  const markup = `<span data-reactid="${React.nextRootIndex}">${element}</span>`;
  // 直接将markup塞到container中
  $(container).html(markup);
```


#### element可能为字符串、Jsx语法（需转成虚拟dom）、对象、类


```
  // 创建一个工厂函数，来生成对应的react元素
  // 实例化
  const createReactUnitInstance = createReactUnit(element);
  const markup = createReactUnitInstance.getMarkUp(React.nextRootIndex);
  // 直接将markup塞到container中
  $(container).html(markup);
```


##### 将公共方法抽离出来

```
class Unit {
  constructor(element) {
    this.currentElement = element;
  }
}
```

##### 文本渲染

```
class ReactTextUnit extends Unit {
  getMarkUp(rootId) {
    this._rootId = rootId;
    return `<span data-reactid="${rootId}">${this.currentElement}</span>`;
  }
}
```

##### JSX渲染，通过React.createElement方法解析

```
// element为JSX，会通过babel转义
const element = React.createElement(
  "div",
  { name: "JSX" },
  "hello react JSX",
  React.createElement("button", {}, "child")
);

React.render(element, document.getElementById("root"));

class ReactNativeUnit extends Unit {
  getMarkUp(rootId) {
    this._rootId = rootId;
    console.log(this.currentElement);
    const { type, props } = this.currentElement;
    let tagStart = `<${type} data-reactid="${rootId}"`;
    const tagEnd = `</${type}>`;
    let contentStr;
    for (let propName in props) {
      // 若属性是事件
      if (/on[A-Z]/.test(propName)) {
        // 找到绑定事件的元素
        // 不能给字符串绑定事件，可以把事件委托到父级元素
        const eventType = propName.slice(2).toLocaleLowerCase();
        $(document).on(eventType, `[data-reactid="${rootId}"]`, props[propName]);
      } else if (propName === "children") {
        contentStr = props[propName]
          .map((child, idx) => {
            let childInstance = createReactUnit(child);
            return childInstance.getMarkUp(`${rootId}.${idx}`);
          })
          .join("");
      } else {
        tagStart += ` ${propName}=${props[propName]}`;
      }
    }
    return tagStart + ">" + contentStr + tagEnd;
  }
}
```

##### 组件渲染，通过React.Component方法解析

```
// element为Class
class SubCounter {
  componentWillMount() {
    console.log("child component will mount");
  }
  componentDidMount() {
    console.log("child component did mount");
  }
  render() {
    return <span>SubCounter</span>;
  }
}

class Counter extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      number: 1,
    };
  }

  componentWillMount() {
    console.log("parent component will mount");
  }

  componentDidMount() {
    console.log("parent component did mount");
  }

  render() {
    return <SubCounter />;
  }
}

// bable转换为
const element = React.createElement(Counter, {
  name: "component",
});

React.render(element, document.getElementById("root"));

// component单元
class ReactCompositUnit extends Unit {
  getMarkUp(rootId) {
    this._rootId = rootId;
    const { type: Component, props } = this.currentElement;
    // type是个类
    const componentInstance = new Component(props);

    // 执行组件内钩子函数
    // 调用实例上的componentWillMount方法
    // 递归调用时，会先渲染父组件，调用父组件的componentWillMount方法
    componentInstance.componentWillMount &&
      componentInstance.componentWillMount();

    // 调用render,拿到结果
    const reactComponentRenderer = componentInstance.render();
    // 递归调用返回的结果
    const reactCompositUnitInstance = createReactUnit(reactComponentRenderer);
    const markUp = reactCompositUnitInstance.getMarkUp(rootId);
    // 订阅mounted事件,页面挂载完成后执行
    // 需要先执行子组件componentDidMount方法，再执行父组件componentDidMount方法
    $(document).on("mounted", () => {
      componentInstance.componentDidMount &&
        componentInstance.componentDidMount();
    });
    return markUp;
  }
}

// 调用componentDidMount钩子，需要在页面渲染完成后发布mounted方法
/*render 渲染函数
 *@params element 渲染的元素
 *@params container 渲染到哪个容器当中
 */
function render(element, container) {
  // 创建一个工厂函数，来生成对应的react元素
  // 实例化
  const createReactUnitInstance = createReactUnit(element);
  // 为了方便查找到某个元素，需要给每个元素打上唯一标记
  const markup = createReactUnitInstance.getMarkUp(React.nextRootIndex);
  // 直接将markup塞到container中
  $(container).html(markup);
  // 触发挂载完成的方法
  $(document).trigger('mounted')
}
```






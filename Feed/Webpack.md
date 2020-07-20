#### webpack基本配置
##### 拆分配置和merge

```
webpack.common.js
    entry,
    module: {
        rules: [
            {
                test: /\.css$/,
                loader: [
                        'style-loader',
                        'css-loader',
                        'postcss-loader'
                ]
            },
            {
                test: /\.less$/,
                loader: [
                       'style-loader',
                        'css-loader',
                        'less-loader',
                        'postcss-loader'
                ]
            },
        ], // 定义一些loader
    },
    plugins: []

// 用webpack-merge合并webpack.common.js
webpack.dev.js
    mode,
    module: {
        rules: [], // 定义一些loader
    },
    plugins: [
        new webpack.DefinePlugin({
            // window.ENV = 'development',
            ENV: JSON.stringfy('development')
        })
    ],
    devServer: {}
    
webpack.prod.js
    mode,
    output,
    module: {
        rules: [], // 定义一些loader
    },
    plugins: [
        new CleanWebpackPlugin(), // 会默认清空output.path文件夹，
        new webpack.DefinePlugin({
            // window.ENV = 'production',
            ENV: JSON.stringfy('production')
        })
    ],

```
##### 启动本地服务

##### 处理ES6
配置.babelrc文件

##### 处理样式
放在webpack.common.js文件
postcss.confg.js（加前缀，浏览器兼容）

##### 处理图片
webpack.prod.js使用url-loader,小于5kb的图片用base64产出，否则依然延用file-loader

#### 高级配置
##### 多入口

```
entry: {
    index: path.join(srcPath, 'index.js'),
    other: path.join(srcPath, 'other.js')
},
output: {
    filename: '[name][contentHash:8].js'
},
plugins: [
    new HtmlWebpackPlugin({
        template: path.join(srcPath, 'index.html'),
        filename: 'index.html',
        // chunks表示页面引用哪个chunk
        chunks: ['index'] // 只引用index.js
    }),
    new HtmlWebpackPlugin({
        template: path.join(srcPath, 'other.html'),
        filename: 'other.html',
        // chunks表示页面引用哪个chunk
        chunks: ['other'] // 只引用other.js
    }),
]

```
#### 抽离CSS

```
webpack.prod.js

module: {
        rules: [
            {
                test: /\.css$/,
                loader: [
                        MiniCssExtractPlugin.loader,
                        'css-loader',
                        'postcss-loader'
                ]
            },
            {
                test: /\.less$/,
                loader: [
                        MiniCssExtractPlugin.loader,
                        'css-loader',
                        'less-loader',
                        'postcss-loader'
                ]
            },
        ], // 定义一些loader
    },
plugins: [
    // 抽离css文件
    new MiniCssExtractPlugin({
        filename: 'css/main.[contentHash:8].css'
    })
],
optimization: {
    // 压缩css
    minimizer: [new TerserJSPlugin({}), new OptimizeCssAssertsPlugin()]
}
    
```
##### 抽离公共代码

```
webpack.prod.js

optimization: {
    // 压缩css
    minimizer: [new TerserJSPlugin({}), new OptimizeCssAssertsPlugin()],
    
    // 切割代码块
    splitChunks: {
        // 'initial':入口chunk,异步导入的文件不处理
        // 'async': 异步chunk,只对异步导入的文件处理
        // 'all': 全部
        chunks: 'all',
        
        cacheGroups: {
            // 第三方模块
            vendor: {
                name: 'vendor', // chunk名
            },
            
            // 公共模块
            common: {
                name: 'common', // chunk名
            }
        }
    }
}
```
##### 懒加载

```
// 引入动态数据 - 懒加载
setTimeout(() => {
    import('./dynamic-data.js').then(res => {
        console.log(res)
    })
}, 1500)
```

##### 处理JSX
配置.babelrc

##### 处理Vue
给vue文件配置vue-loader

#### 优化打包效率

#### 优化产出代码

#### 构建流程概述

#### babel
编译es6语法

#### 前端代码为何要构建和打包

#### module、chunk、bundle有何区别
- module各个文件，webpack中一切皆模块
- chuck 多模块合并成的 entry import() splitChunk
- bundle 最终的输出文件

#### webpack性能优化
##### 优化babel-loader

```
{
    test: '/\.js$/',
    use: ['babel-loader?cacheDirectory'], //开启缓存
    include: path.resolve(__dirname, 'src'), //明确范围
}
```

##### IgnorePlugin
忽略不不要的文件，比如忽略moment库多语言版本文件

##### noParse
##### happyPack多进程打包
- 开启多进程打包
- 提高构件速度，特别是多核CPU

##### ParallelUglifyPlugin多进程压缩JS

##### 自动刷新
若配置了devServer，默认开启自动刷新
整个网页全部刷新，速度较慢，状态丢失

##### 热更新
新代码生效，网页不刷新，状态不丢失

```
webpack.dev.js

entry: {
    index: [
        'webpack-dev-server/client?http://localhost:8080',
        'webpack/hot/dev-server',
        path.join(srcPath, 'index.js')
    ]
},
plugins: [
    new HotModuleReplacementPlugin()
],
devServer: {
    hot: true
}
```


##### DllPlugin动态链接库插件

#### webpack性能优化，产出代码
##### 小图片base64编码
##### bundle加hash,命中缓存
##### 大文件懒加载 import()
##### 提取公共代码
##### IgnorePlugin
##### 使用CDN加速
```
output: {
    publicPath: 'http://cdn.xxx.com' // 修改所有静态文件url前缀
}
```
##### 使用production
- 默认自动压缩代码 mode: 'production'
- Vue、React等会自动删除调试代码（如开发环境的warning）
- 启动tree-sharking(ES6 module才生效)

##### ES6 module和CommonJs的区别

```
let apiList = require('../config/api.js')
if (isDev) {
    // commonJs可以动态引入，执行时引用
    apiList = require('../config/api_dev.js')
}

import apiList from '../config/api.js'
if (isDev) {
    // ES6 module编译时报错，只能静态引用
    import apiList from '../config/api_dev.js'
}
```
##### 开启Scope hosting（作用域提升）
- 代码体积更小
- 创建函数作用域更少，减少跨作用域访问

```
webpack会将每个模块包裹在函数的闭包中，闭包越多，占据内存越多，会影响浏览器性能，开启Scope hosting就是将多个模块放到单一的函数闭包中
```

- 代码可读性更好

```
resolve: {
    // 针对npm中第三方模块优先采用jsnext:main中指向es6语法的文件
    mainFields: ['jsnext:main', 'brower', 'main']
},
plugins: [
    new ModuleConcatenationPlugin()
]
```

#### babel

##### babel-polyfill
- 是core-js和regenerator的集合，
- babel7.4后被弃用，推荐直接使用core-js和regenerator
- 按需引用

```
{
    "preset": [
        [
            "@babel/preset-env",
            {
                "useBuildIn": "usage", // 按需引用
                "core-js": 3
            }
        ]
    ]
}
```

#### babel-runtime
若开发第三方库，使用方不会出现副作用，比如不会造成全局作用域（promise、incudes）的污染


#### 前端为何要打包和构建
- 体积更小（压缩合并，tree-sharking）,加载速度更快
- 编译高级语言和语法(TS,es6,模块化，scss)
- 兼容性和错误提示（polyfill、postcss、eslint）
- 统一高效的开发环境
- 统一的构建流程和产出标准
- 集成公司构建规范（提测、上线）

#### loader和plugin的区别
- loader-模块转换器
- plugin-扩展插件

#### babel和webpack的区别
- babel-JS新语法编译器
- webpack-打包构建工具，是多个loader、plugin的集合

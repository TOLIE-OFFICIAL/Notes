# webpack入门

webpack是一种静态模块打包器，它从入口文件开始，根据各个文件之间的依赖关系构建内部依赖图，再根据这个依赖树生成一个chunk(代码块)。之后再对这个chunk进行各项处理，比如less=>CSS，这个处理的过程就叫打包，打包完成最后形成一个bundle。



## webpack核心概念和devServer

### 1、Entry

入口(Entry)指明webpack以那个文件为起点开始打包，分析构建内部依赖图。

### 2、Output

输出(Output)指明webpack打包后的资源bundle输出到哪里去，以及如何命名。

```js
entry: './src/js/index.js',
output: {
    //输出文件的文件名和路径，即根目录下面的build/js/built.js
    filename: 'js/built.js',
    path: resolve(__dirname, 'build')
   }
```

### 3、Loaders

Loader让webpack能够去处理非JS文件（webpack自身只理解JS）。

`Loaders`是`webpack`提供的最激动人心的功能之一了。通过使用不同的`loader`，`webpack`有能力调用外部的脚本或工具，实现对不同格式的文件的处理，比如说分析转换less为css，或者把下一代的JS文件（ES6，ES7)转换为现代浏览器兼容的JS文件，对React的开发而言，合适的Loaders可以把React的中用到的JSX文件转换为JS文件。

Loaders需要单独安装并且需要在`webpack.config.js`中的`modules`关键字下进行配置，Loaders的配置包括以下几方面：

>**test**：一个用以匹配loaders所处理文件的拓展名的正则表达式（`必须`）
>
>**loader**：loader的名称（`必须`）
>
>**include/exclude**:手动添加必须处理的文件（文件夹）或屏蔽不需要处理的文件（文件夹）（可选）；
>
>**query**：为loaders提供额外的设置选项（可选）

**注意**： 由于`webpack3.*/webpack2.*`已经内置可处理JSON文件，这里无需再添加`webpack1.*`需要的`json-loader`。



### 4、Plugins

插件(Plugins)可以让webpack执行范围更广的任务，插件范围包括从打包优化和压缩，一直到重新定义环境中的变量等等。



### 5、Mode

模式(Mode)指明webpack使用相应模式的设计。

1. 开发环境打包: webpack ./src/index.js -o ./build/built.js --mode=development
   * webpack会以./src/index.js 为入口文件开始打包，打包后输出到./build/built.js，整体打包环境，是开发环境

2. 生产环境打包: webpack ./src/index.js -o ./build/built.js --mode=production
   * webpack会以./src/index.js 为入口文件开始打包，打包后输出到./build/built.js，整体打包环境，是生产环境

| 选项        | 描述                                                         | 特点                       |
| ----------- | ------------------------------------------------------------ | -------------------------- |
| development | 会将 process.env.NODE_ENV 的值设为 development。启用 NamedChunksPlugin 和 NamedModulesPlugin。 | 能让带妹妹在本地运行       |
| production  | 会将 process.env.NODE_ENV 的值设为 production。启用 FlagDependencyUsagePlugin, FlagIncludedChunksPlugin, ModuleConcatenationPlugin, NoEmitOnErrorsPlugin, OccurrenceOrderPlugin, SideEffectsFlagPlugin 和 UglifyJsPlugin(会压缩JS代码). | 能让代码优化上线运行的环境 |

> *记住，只设置* `NODE_ENV`*，则不会自动设置* `mode`*。*



## 开发环境的基本配置

### 初始化项目

新建文件夹webpack-demo1，进入文件夹打开终端，运行

```powershell
npm init
```

#### 为什么初始化项目

在node开发中使用npm init会生成一个pakeage.json文件，这个文件主要是用来记录这个项目的详细信息的，它会将我们在项目开发中所要用到的包，以及项目的详细信息等记录在这个项目中。方便在以后的版本迭代和项目移植的时候会更加的方便。也是防止在后期的项目维护中误删除了一个包导致的项目不能够正常运行。使用npm init初始化项目还有一个好处就是在进行项目传递的时候不需要将项目依赖包一起发送给对方，对方在接受到你的项目之后再执行npm install就可以将项目依赖全部下载到项目里。

进入到项目所在的目录之后我们就可以直接执行npm init,执行了npm init之后,会让我们填写一些配置信息，如果还不知道怎么填写的话可以一路回车。

>package name: 你的项目名字叫啥
>version: 版本号
>description: 对项目的描述
>entry point: 项目的入口文件（一般你要用那个js文件作为node服务，就填写那个文件）
>test command: 项目启动的时候要用什么命令来执行脚本文件（默认为node app.js）
>git repository: 如果你要将项目上传到git中的话，那么就需要填写git的仓库地址（这里就不写地址了）
>keywirds：项目关键字（我也不知道有啥用，所以我就不写了）
>author: 作者的名字（也就是你叫啥名字）
>license: 发行项目需要的证书

### 安装webpack

```powershell
# 先全局安装，全局安装会覆盖之前的版本而不是重复下载
npm i  webpack webpack-cli -g
# 再本地安装将依赖安装为开发依赖
npm i  webpack webpack-cli -D

```

webpack-cli 提供了许多命令来使 webpack 的工作变得更简单，cli即命令行接口（Command Line Interface）

### Loader使用

#### Loader下载

```powershell
#本地安装
npm i css-loader style-loader less-loader less -D
```

#### Loader配置

```js
//webpack.config.js
   module: {
        //loader的详细配置
        //不同文件需要使用不同的loader处理
        rules: [
            //处理css资源
            {
                //test指明匹配哪些文件，一般是用正则表达式表示
                test: /\.css$/,
                //使用哪些loader进行处理，执行顺序为从右到左，从下到上依次执行
                use: [
                    'style-loader',//创建style标签，后将JS中的样式资源插入进去，添加到header中生效
                    'css-loader'//将css文件变成commonjs模块加载到JS中，里面内容是样式字符串
                ]
            },
            //处理less资源
            {
                test: /\.less$/,
                use: [
                    'style-loader',
                    'css-loader',
                    //需要下载less-loader和less
                    'less-loader'//将less文件编译为css文件，less=>css
                ]
            },

            //处理图片资源，但是默认处理不了html中的img标签图片资源
            {
                test: /\.(jpg|png|gif)$/,
                //使用多个Loader使用use，单个Loader使用loader
                loader: 'url-loader',//这里需要下载两个loader，url-loader和file-loader
                options: {
                    publicPath: '/dist/',
                    //图片大小小于8kb，就会对其进行base64编码处理
                    //base64的优点：减少请求数量，减轻服务器压力
                    //base64的缺点：图片体积更大，文件处理速度更慢，所以一般只对小图片进行处理
                    limit: 8 * 1024

                    //问题：url-loader默认使用ES6模块化解析，而html-loader引入img是用commonjs
                    //所以解析时会出问题
                    //解决：关闭url-loader的ES6解析，使用commonjs的解析
                    esModule: false,

                    //图片文件重命名,
                    //[hash:10]取图片的hash前十位
                    //[ext]取文件原先的扩展名
                    name: '[hash:10].[ext]',
                    //指定符合正则的文件输出目录
                    outputPath: 'imgs'
                }
            },

            //处理html文件
            {
                test: /\.html$/,
                //处理html中的img（负责引入img，从而能被url-loader进行打包处理,这里的引入是commonjs的引入
                loader: 'html-loader',
            },
             //处理其它资源
            {
                //exclude排除哪些格式的文件
                exclude: /\.(html|css|js|jpg|png|gif)$/,
                loader: 'file-loader',
                options:{
                     outputPath: 'media'
                }
            }
        ],
    }
```

### Plugins使用

#### plugins下载

```powershell
npm i html-webpack-plugin -D
```

#### plugins引入和使用

```js
const HtmlWebpackPlugin = require('html-webpack-plugin');

//plugins插件的配置
plugins: [
    //详细的plugins插件配置
    //html-webpack-plugin配置
    //功能：默认会创建一个空的html文件（没有dom内容），自动引入打包输出后的所有资源（资源可以是CSS/js等）
    new HtmlWebpackPlugin({
        //复制"./src/index.html"路径下的html文件，使用HtmlWebpackPlugin的默认功能，即自动引入打包输出后的所有资源（资源可以使CSS/js等）
        template: "./src/index.html"
    })
]
```

### devServer使用

用来辅助自动化开发，拥有自动编译，自动刷新浏览器等功能。

特点是只会在内存中编译打包，不会有任何的输出。

同样需要再webpack的配置文件中配置

```js
//启动devServer的指令为npx webpack-dev-server
devServer: {
    //项目构建后的路径
    contentBase: resolve(__dirname, 'build'),
    //启用gzip压缩
    compress: true,
    //服务器的端口号
    // port:3000
    //自动打开浏览器窗口
    open: true,
    //打包时显示进度条
    progress:true
}
```



### 配置开发环境

```js
const { resolve } = require('path');
const HtmlWebpackPlugin = require('html-webpack-plugin');

module.exports = {
    entry: './src/js/index.js',
    output: {
        filename: 'js/built.js',
        path: resolve(__dirname, 'build')
    },
    module: {
        rules: [
            {
                test: /\.css$/,
                use: [
                    'style-loader',
                    'css-loader'
                ]
            },
            //处理html文件中的图片
            {
                test: /\.html$/,
                loader: 'html-loader'
            },
            //只能处理样式文件中的图片
            {
                test: /\.(png|jpg|gif)/,
                loader: 'url-loader',
                options: {
                    //对小于8kb的图片进行base64处理
                    limit: 8 * 1024,
                    //文件重命名，[ext]指的是原文件的后缀名
                    name: '[hash:10].[ext]',
                    esModule: false,
                    outputPath: 'imgs'
                }
            }
        ]
    },
    //创建空的html文件，并引入依赖
    plugins: [
        //复制此路径下的html模板，再引入依赖
        new HtmlWebpackPlugin({
            template: './src/index.html'
        })
    ],
    mode: 'development',
    devServer: {
        //项目构建后的路径
        contentBase: resolve(__dirname, 'build'),
        port: 8080,
        //启用gzip压缩
        compress: true,
        //自动打开新的浏览器窗口
        open: true
    }
}
```



## 生产环境的基本配置

### CSS处理

#### 提取CSS成单独文件

css与js分开，同时不再通过style标签引入样式`而是link标签`

优点：不再会出现闪屏现象，同时减小了bundle.js的文件大小，优化了性能。

##### 安装plugin

```powershell
#本地安装
npm i mini-css-extract-plugin -D
```

##### plugins引入和使用

```js
const MiniCssExtractPlugin = require('mini-css-extract-plugin');

module: {
        rules: [
            {
                test: /\.css$/,
                use: [
                    // 'style-loader',//创建一个style标签，并将样式写进去

                    //用这个loader取代style-loader，作用是提取js中的css成为单独文件
                    MiniCssExtractPlugin.loader,
                    'css-loader'//将css=>js
                ]
            }
        ]
 },
     
plugins: [
        new HtmlWebpackPlugin({
            //复制此路径下面的html，再引入打包后的所有资源
            template: "./src/index.html"
        }),
        new MiniCssExtractPlugin({
            //指明单独提取出来的css文件名称和存放路径
            filename: 'css/built.css'
        })
    ]
```



#### 兼容性处理

css的兼容性处理，会使用到`postcss库`，webpack使用postcss库要使用postcss-loader和postcss-preset-env插件。

此插件先帮助postcss找到browserslist的配置内容，再根据配置内容的要求加载css的兼容性样式

```js
//这里使用的包版本
//"postcss-loader": "^4.3.0",
//"postcss-preset-env": "^6.7.1",

//postcss.config.js
module.exports = {
    plugins: [
        require('autoprefixer')({
            overrideBrowserslist: ["last 2 version", ">1%", "iOS 7"]
        })
    ]
}
```

postcss-loader的在webpack.config.js中的配置

```js
 module: {
        rules: [
            {
                test: /\.css$/,
                use: [
                    // 'style-loader',//创建一个style标签，并将样式写进去

                    //用这个loader取代style-loader，作用是提取js中的css成为单独文件
                    MiniCssExtractPlugin.loader,
                    'css-loader'//将css=>js
                    
                    //使用loader的默认配置
                    //"postcss-loader"
                    
                    //修改loader的配置
                    {
                        loader: 'postcss-loader',

                    }
                    }
                ]
            }
        ]
 },
```

#### 压缩处理

使用optimize-css-assets-webpack-plugin插件进行压缩

##### 安装Plugin

```powershell
#本地安装
npm i optimize-css-assets-webpack-plugin -D
```

##### plugins引入和使用

```js
const OptimizeCssAssetsPlugin = require('optimize-css-assets-webpack-plugin');

plugins: [
        new HtmlWebpackPlugin({
            //复制此路径下面的html，再引入打包后的所有资源
            template: "./src/index.html"
        }),
        new MiniCssExtractPlugin({
            //指明单独提取出来的css文件名称和存放路径
            filename: 'css/built.css'
        }),
        new OptimizeCssAssetsPlugin()
    ]
```



### JS处理

#### 语法检查-eslint

[airbnb的JavaScript指南](https://github.com/lin-123/javascript)

> 注意：语法检查要`只检查开发者写的代码`，不要检查第三方库的js语法

在webpack中使用最少需要两个，eslint-loader和eslint。这里使用`Airbnb`的库，需要安装eslint-config-airbnb-base、eslint和eslint-plugin-import。

* 使用eslint-loader，要注意一定要排除node_modules的第三方文件；

```js
 {
    test: /\.js$/,
    exclude: /node_modules/,
    loader: 'eslint-loader',
    options: {
        //启用自动修复
        ix: true
    }
}
```



* 在package.json中配置eslint的检查规则，引入Airbnb的库；

```json
//package.json
"eslinkConfig": {
    "extends":"airbnb-base"
  }
```



#### 兼容性处理-bable

##### 什么是bable

[Babel](https://babeljs.io) 是一个 [transpiler](https://en.wikipedia.org/wiki/Source-to-source_compiler)。它将现代的 JavaScript 代码转化为以前的标准形式。

实际上，Babel 包含了两部分：

1. transpiler 

   ​		用于重写代码的 transpiler 程序。开发者在自己的电脑上运行它。它以之前的语言标准对代码进行重写。然后将代码传到面向用户的网站。像 [webpack](http://webpack.github.io/) 这样的现代项目构建系统，提供了在每次代码改变时自动运行 transpiler 的方法，因此很容易集成在开发过程中。

2. polyfill

   ​		新的语言特性可能包括新的内置函数和语法构造。 transpiler 会重写代码，将语法结构转换为旧的结构。但是对于新的内置函数，需要我们去实现。JavaScript 是一个高度动态化的语言。脚本可以添加/修改任何函数，从而使它们的行为符合现代标准。

   更新/添加新函数的脚本称为 “polyfill”。它“填补”了缺口，并添加了缺少的实现。

   两个有意思的 polyfills 是：

   - [core js](https://link.juejin.cn?target=https%3A%2F%2Fgithub.com%2Fzloirock%2Fcore-js) 支持很多，允许只包含需要的功能。
   - [polyfill.io](http://polyfill.io) 根据功能和用户的浏览器，为脚本提供 polyfill 的服务。

所以，如果我们要使用现代语言功能，transpiler 和 polyfill 是必要的。



这里使用到的包是babel-loader@8.0.6、@babel/preset-env@7.8.4、@babel/core@7.8.4

##### 1、@babel/preset-env

* 使用babel-loader，要注意一定要排除node_modules的第三方文件；

```js
 {
     test: /\.js$/,
         exclude: /node_modules/,
             loader: 'babel-loader',
             options: {
                 //预设指示babel做怎么样的兼容性处理
                 presets: ['@babel/preset-env']
         }
}
```

* 这里主要是@babel/preset-env帮助我们实现的兼容性处理，需要注意的是这个包只能帮助我们转换一些基本语法，比如promise就不能转化。要实现全版本的兼容性处理，就要使用其他的包比如@babel/polyfill

##### 2、@babel/polyfill

* @babel/polyfill需要在JS文件中引入

```js
//@babel/polyfill是比较暴力的兼容包，他会将所有的可能有兼容问题的内容编译到js文件中
//在只需要解决部分兼容型问题的时候，会导致项目增大很多
import '@babel/polyfill'
```

**问题**：@babel/polyfill会将所有的可能有兼容问题的内容编译到js文件中，在只需要解决部分兼容型问题的时候，会导致项目增大很多

##### 3、core-js

core-js可以实现按需编译需要的内容，实现按需加载，可以有效避免文件过于庞大。

**注意**：不能和@babel/polyfill一起使用

```js
 {
                test: /\.js$/,
                exclude: /node_modules/,
                loader: 'babel-loader',
                options: {
                    //预设指示babel做怎么样的兼容性处理
                    presets: [
                        [
                            '@babel/preset-env',
                            {
                                //按需加载
                                useBuiltIns: 'usage',
                                //指定corejs的版本
                                corejs: {
                                    version: '3'
                                },
                                //指定兼容哪些个版本的浏览器
                                targets: {
                                    //chrome60及60以上的版本
                                    chrome: '60',
                                    firefox: '60'
                                }
                            }
                        ]
                    ]
                }
            },
```



#### 压缩处理

生产模式下会自动压缩JS代码，所以只需要调整mode项就可实现js压缩。



### HTML处理

`html不需要进行兼容性处理`，也不能进行兼容性处理，html标签认识就认识，不认识就不认识。

#### 压缩处理

使用html-webpack-plugin就可实现html压缩

```js
new HtmlWebpackPlugin({
            //复制此路径下面的html，再引入打包后的所有资源
            template: "./src/index.html",
            minify: {
                //移除换行
                collapseWhitespace: true,
                //移除注释
                removeComments: true
            }
        })
```



### 配置生产环境

```js
const { resolve } = require('path');
const HtmlWebpackPlugin = require('html-webpack-plugin');
const MiniCssExtractPlugin = require('mini-css-extract-plugin');
const OptimizeCssAssetsPlugin = require('optimize-css-assets-webpack-plugin');

const commonCssLoader=[
    // 'style-loader',//创建一个style标签，并将样式写进去
    //用这个loader取代style-loader，作用是提取js中的css成为单独文件
    MiniCssExtractPlugin.loader,
    'css-loader',//将css=>js

    //使用loader的默认配置
    //"postcss-loader"

    //修改loader的配置
    {
        loader: 'postcss-loader',
    }
];
module.exports = {
    entry: './src/js/index.js',
    output: {
        filename: 'js/built.js',
        path: resolve(__dirname, 'build')
    },
    module: {
        rules: [
            {
                test: /\.css$/,
                use: [...commonCssLoader]
            },
            //处理图片资源，但是无法处理html中的img标签
            {
                test: /\.(png|jpg|gif)$/,
                loader: 'url-loader',
                options: {
                    name: '[hash:10].[ext]',
                    esModule: false,
                    outputPath: 'imgs'
                }
            },
            //处理html中的img标签
            {
                test: /\.html$/,
                loader: 'html-loader',
                options: {
                    // 图片大小小于8kb，就会对其进行base64编码处理
                    limit: 8 * 1024
                }
            },
            //处理其它资源
            {
                exclude: /\.(html|css|js|jpg|png|gif)$/,
                loader: 'file-loader',
                options: {
                    name: '[hash:10].[ext]',
                    outputPath: 'media'
                }
            },
            //还需要自己设置检查规则
            //package.json中的eslintConfig中进行设置，使用airbnb规则
            {
                test: /\.js$/,
                exclude: /node_modules/,
                //优先执行，避免因为babel-loader执行在前造成一些问题
                enforce:'pre',
                loader: 'eslint-loader',
                options: {
                    //启用自动修复
                    fix: true
                }
            },
            {
                test: /\.js$/,
                exclude: /node_modules/,
                loader: 'babel-loader',
                options: {
                    //预设指示babel做怎么样的兼容性处理
                    presets: [
                        [
                            '@babel/preset-env',
                            {
                                //按需加载
                                useBuiltIns: 'usage',
                                //指定corejs的版本
                                corejs: {
                                    version: '3'
                                },
                                //指定兼容哪些个版本的浏览器
                                targets: {
                                    chrome: '60',
                                    firefox: '60'
                                }
                            }
                        ]
                    ]
                }
            }
        ]
    },
    plugins: [
        new HtmlWebpackPlugin({
            //复制此路径下面的html，再引入打包后的所有资源
            template: "./src/index.html",
            minify: {
                //移除换行
                collapseWhitespace: true,
                //移除注释
                removeComments: true
            }
        }),
        new MiniCssExtractPlugin({
            //指明单独提取出来的css文件名称和存放路径
            filename: 'css/built.css'
        }),
        new OptimizeCssAssetsPlugin()
    ],
    mode: 'production'
}
```



## 性能优化

### 开发环境性能优化

#### 优化打包构建速度

##### HMR功能

HMR，即Hot Module Replacement，模块热替换/热模块替换

**[实现原理](https://cloud.tencent.com/developer/article/1647565?from=article.detail.1621751)**：当代码文件修改并保存之后，webapck通过watch监听到文件发生变化，根据变化的内容生成两个补丁文件：说明变化内容的manifest（文件格式是hash.hot-update.json，包含了hash和chund Id用来说明变化的内容）和chunk js（hash.hot-update.js）模块。

后将结果存储在内存文件系统中，通过websocket通信机制将重新打包的模块发送到浏览器端，浏览器端hmr runtime 根据 manifest的 hash 和 chunkId 使用ajax拉取最新的更新模块替换旧的模块，浏览器不需要刷新页面就可以实现应用的更新。

![HMR](http://pic.tolie.biz/images/202203121710610.png)

> 作用：实现一个模块发生变化，只打包这个发生变化的模块，而不是重新打包所有模块，可以极大的提升构建速度

**注意**：HMR 不适用于生产环境，这意味着它应当只在开发环境使用。



```js
//启动devServer的指令为npx webpack-dev-server
devServer: {
    //项目构建后的路径
    contentBase: resolve(__dirname, 'build'),
    //启用gzip压缩
    compress: true,
    //服务器的端口号
    // port:3000
    //自动打开浏览器窗口
    open: true,
	//开启HMR功能
    //修改webpack配置，记得重启devServer功能
    hot: true
}
```



`DevServer开启HMR功能之后，样式文件就直接可以实现HMR`，即更改样式文件不会导致真个项目重新打包渲染，这是因为style-loader已经内部实现样式文件的热重载。但是JS和HTML文件需要进一步设置才可以实现热重载。

| 文件类型 | HMR实现                                              | 解决方法/原因                                                |
| :------- | ---------------------------------------------------- | ------------------------------------------------------------ |
| 样式文件 | 直接可以实现HMR功能                                  | style- loader已经内部实现                                    |
| js文件   | 默认不能使用HMR功能                                  | 修改js代码，添加允许实现HMR的代码<br />**注意**：HMR功能对JS文件的处理，`只能处理非入口文件的其他JS模块`。 |
| html文件 | 默认不能使用HMR功能，同时会`导致html 文件不能热更新` | HTML文件只有一个没必要使用HMR功能。<br />只需要`将html文件路径加入entry项中`，即可解决开启HMR导致html不能实现热更新。 |

```js
//webpack.config.js
//开启HMR同时解决html不能实现热更新问题
entry: ['./src/js/index.js','./src/index.html']
```

```js
//index.js
//实现js文件的HMR
//如果module.hot为true，就说明webpack-dev-server开启了HMR
if (module.hot) {
    //监听第一个参数路径下的js文件，一旦此文件发生变化，其他文件默认不会重新打包构建，
    //同时会执行第二个参数中的回调函数
    module.hot.accept('./print.js', function () {
        print();
    })
    //如果需要监听其他模块，只需要复制上面的accept方法
}
```



##### source-map

source-map是一种提供源代码到构建后代码映射技术（如果构建后代码出错了，通过映射可以追踪源代码错误的位置）

> **语法**
>
> &#91;inline-| hidden- | |eval- ]&#91; nosources-][cheap- &#91;module- ]source-map

| 种类                      | 生成文件种类 | 运行效果                                                     |
| :------------------------ | :----------- | ------------------------------------------------------------ |
| source-map                | 外部         | 正确获取错误代码准确信息和源代码的错误位置；                 |
| inline-source-map         | 内联         | 只生成一个内联source -map；<br />正确获取错误代码准确信息和源代码的错误位置； |
| hidden-source-map         | 外部         | 正确获取错误代码准确信息，但无法追踪到源代码的错误位置；     |
| eval - source -map        | 内联         | 每一个文件都生成对应的source - map，都在eval。正确获取错误代码准确信息和源代码的错误位置； |
| nosources - source -map   | 外部         | 正确获取错误代码准确信息，但没有任何源代码信息；             |
| cheap- source-map         | 外部         | 正确获取错误代码准确信息，但无法准确定位到错误的具体位置，只能确定到行； |
| cheap- module- source-map | 外部         | 正确获取错误代码准确信息，但无法准确定位到错误的具体位置，只能确定到行； |

**说明**：内联的方式构建速度更快

​			module类的source-map会将loader的source-map加入

* 开发环境要求：速度快，调试更友好

  * 速度快 ( eval > inline > cheap > .... )
    1. eval-cheap-souce -map
    2. eval- source-map

  * 调试更友好
    1. souce - map
    2. cheap- module- souce-map
    3. cheap- souce -map

  * `推荐`

    eval-source-map / eval-cheap-module-souce-map（官方脚手架使用的是 eval-source-map ）

* 生产环境要求：源代码要不要隐藏？调试要不要更友好？代码体积大小

  * 内联会让代码体积变大，所以在生产环境不用内联

  * 代码需要隐藏

    1. nosources -source-map全部隐藏
    2. hidden-source-map只隐藏源代码，会提示构建后代码错误信息

  * `推荐`

    source-map / cheap-module-souce-map



##### oneOf

一个项目可能存在很多loader，一个文件就需要匹配一下所有loader，看看是否符合要求。但很多文件不需要多次命中不同的loader，`使用oneOf包裹rules下的项`，就会`让文件只匹配这些loader中的一个`，匹配完成就不再尝试其他的loader了。

> **注意**：不能有两个配置处理同一种类型的文件，比如不能将eslint-loader和babel-loaderloader都包裹在oneOf内。

```js
module: {
        rules: [
            //还需要自己设置检查规则
            //package.json中的eslintConfig中进行设置，使用airbnb规则
            {
                test: /\.js$/,
                exclude: /node_modules/,
                loader: 'eslint-loader',
                //优先执行
                enforce: 'pre',
                options: {
                    //启用自动修复
                    fix: true
                }
            },
            {
                oneOf: [
                    {
                        test: /\.css$/,
                        use: [
                            'style-loader',
                            'css-loader',//将css=>js
                            {
                                loader: 'postcss-loader',
                            }
                        ]
                    },                 
                    //处理html中的img标签
                    {
                        test: /\.html$/,
                        loader: 'html-loader',
                        options: {
                            // 图片大小小于8kb，就会对其进行base64编码处理
                            limit: 8 * 1024
                        }
                    },
                    {
                        test: /\.js$/,
                        exclude: /node_modules/,
                        loader: 'babel-loader',
                        options: {
                            //预设指示babel做怎么样的兼容性处理
                            presets: [
                                [
                                    '@babel/preset-env',
                                    {
                                        //按需加载
                                        useBuiltIns: 'usage',
                                        //指定corejs的版本
                                        corejs: {
                                            version: '3'
                                        },
                                        //指定兼容哪些个版本的浏览器
                                        targets: {
                                            chrome: '60',
                                            firefox: '60'
                                        }
                                    }
                                ]
                            ]
                        }
                    }
                ]
            }
        ]
    }
```









优化代码调试功能





### 生产环境性能优化

#### 优化打包构建速度

##### 缓存

###### 1、babel缓存

在生产模式下，不建议使用HMR功能。为了优化打包速度，就需要使用`缓存`。以JS代码为例，一个项目可能有很多很多的JS模块，没必要每次修改其中个别文件的代码，就重新打包整个项目。使用缓存就可以在二次乃至之后的打包编译过程中读取之前的缓存，提高构建速度。

> 功能:jack_o_lantern:：提高第二次打包构建的速度。

###### 开启bable-loader缓存

```js
{
    test: /\.js$/,
        exclude: /node_modules/,
            loader: 'babel-loader',
                options: {
                    //预设指示babel做怎么样的兼容性处理
                    presets: [
                        [
                            '@babel/preset-env',
                            {
                                //按需加载
                                useBuiltIns: 'usage',
                                //指定corejs的版本
                                corejs: {
                                    version: '3'
                                },
                                //指定兼容哪些个版本的浏览器
                                targets: {
                                    chrome: '60',
                                    firefox: '60'
                                }
                            }
                        ]
                    ]，
                    //开启bable缓存
                    //在之后的构建中就会读取之前的缓存
                    cacheDirectory:true
                }
}
```



###### 2、文件资源缓存

通过每次生成不同名称的打包文件实现页面更新（利用打包每次生成的hash值保证文件命名的不同）

`问题一`：因为js和css文件都是用一个hash值，不论修改了几个文件，即使只有一个也会重新打包，导致所有的缓存失效。

​	`解决`：利用chunkhash根据chunk生成的hash值，如果打包来源于一个chunk，那么hash就一样。反之就不同。



`问题二`：利用chunkhash还是会导致js和css都被重新打包。

​	`原因`：是因为css是在js中被引入的，所以他们一定同属一个chunk。

​	`解决`：使用contenthash，contenthash是根据文件内容生成的，不同文件的contenthash一定是不同的。

> 功能:jack_o_lantern:：让代码上线后更好的去使用缓存，减少请求，提高速度。

```js
output: {
    filename: 'js/built.[contenthash:10].js',
    path: resolve(__dirname, 'build')
},
    
plugins: [
    new MiniCssExtractPlugin({
        //指明单独提取出来的css文件名称和存放路径
        filename: 'css/built.[contenthash:10].css'
    }),
]
```



###### 三种不同hash的区别

1. hash

   每次webpack打包都会生成唯一的hash。

2. chunkhash

   根据chunk生成的hash值，如果打包来源于一个chunk，那么hash就一样，反之就不同。

3. contenthash

   根据文件内容生成的hash值，不同文件的contenthash一定是不同的。同一文件不同内容打包后的contenthash也是不同的。



#### 优化代码运行的性能

##### tree shaking

> 目的：去除应用程序中的无用代码，让代码体积更小
>
> 前提：1. 必须使用ES6模块化编程；2. 开启production模式

因webapck版本问题 或者 在package.json中关闭sideEffect，可能会导致一些问题

**问题**：可能会导致css / @babel/polyfill 都被tree shaking

```json
"sideEffect":false
```

**解决**：修改sideEffect项的值，将不需要tree shaking的文件放在其中

```json
//以阻止css、less被tree shaking为例
"sideEffect":["*.css","*.less]
```



##### code split

> 目的：将打包后的bundle文件，分解成多个不同的文件，实现按需加载。

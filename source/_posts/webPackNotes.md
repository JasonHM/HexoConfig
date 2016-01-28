title: webpack笔记
tags: 
    - webpack
---

[getting started](http://webpack.github.io/docs/tutorials/getting-started/)

##笔记:

install: `npm install webpack -g`

一个简单的配置文件`webpack.config.js`:

```json

module.exports = {
    entry: "./entry.js",
    output: {
        path: __dirname,
        filename: "bundle.js"
    },
    module: {
        loaders: [
            { test: /\.css$/, loader: "style!css" }
        ]
    }
};
```

entry: 入口

output: 出口配置,filename: 生成的目标文件

loaders: 加载器,`{ test: /\.css$/, loader: "style!css" }`用于处理样式文件

开发模式下的监听文件变化:

```
webpack --watch
```

启动一个server在[8080端口](http://localhost:8080/webpack-dev-server):

```
npm install webpack-dev-server -g
webpack-dev-server --progress --colors
```

##个人理解

引用图片:

![行为](http://webpack.github.io/assets/what-is-webpack.png)

很好的web项目打包工具(另外的一个工具[browserify](https://github.com/substack/node-browserify)),处理文件依赖,调试工具



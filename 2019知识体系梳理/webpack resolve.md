今天在搭建ts-react脚手架的过程中，利用ts-loader处理ts/tsx文件。
webpack.config.js文件
```js
module: {
  rules: [
    { test: /\.(ts|tsx)?$/, use: ['ts-loader] }
  ]
}
```
tsconfig.json
```js
{
  "jsx": "react" //直接编译为react的代码 <div><div/> => React.createElement('div', null, [])
  "target": "es5"
}
```
处理流程为：当遇到ts文件或者tsx文件，交给ts-loader处理，ts-loader会按照配置的`tsconfig.json`文件进行编译直接编译为es5的代码，可在浏览器端直接运行。

#### 遇到问题
在代码中引用其他模块的代码的时候报错，can't find module. 我百思不得其解，终于发现是我没有配置resolve中的extension属性。
```js
resolve: {
  extensions: [".tsx", ".ts", ".js"]
}
```
#### 分析原因
1. 对webapck的理解程度不够，没有注意到webpack中的模块解析方案和resolve的配置
2. 看起来做一个webpack的脚手架很简单，但是只有实际去做了才发现有很多坑需要自己踩过才知道


#### resolve总结
webpack在启动后会从配置的入口模块出发找出所有依赖的模块，`resolve`配置`webpack`如何寻找模块所对应的文件。`webpack`内置`js`模块语法解析功能，默认会采用模块化标准约定的规则去寻找，但我们也可以根据自己的需要修改默认的规则。

##### 常用配置：
1. alias: 通过别名来将原导入路径映射成一个新的路径，这个平时开发中经常用到，比如：
   ```js
    resolve: {
      alias: {
        components: './src/components'
      }
    }
   ```
2. mainFields: 有些第三方模块会针对不同的环境提供多份代码，webpack可以根据mainFields的配置去决定优先采用哪份代码，默认：`mainFields: ['browser', 'main']`
3. extensions: 日常开发中的导入语句一般都不会带后缀名，webpack会自动带上后缀名去尝试访问文件是否存储，默认是：`extensions: ['js', 'json']`。我在配置`typescript`项目时没有配置这一项就出现了找不到模块的错误，就是这个原因导致的。正确的typescript项目的配置为：`extensions: ['ts','tsx','js', 'json']`
4. module: 配置webpack去哪些目录下寻找第三方模块，默认只会去node_modules下去寻找，我们可以自定义寻找的路径，比如大量的导入模块都在`./src/components`下，可以配置为`modules: ['./src/components', 'node_modules']`,这样就可以`import 'button'`直接导入模块。

   
   

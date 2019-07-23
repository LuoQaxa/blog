
[参考](https://juejin.im/post/5c834bfa5188257e8f616946#heading-2)
## babel的作用
babel是一个JavaScript编译器，简单的说就是把js中的高版本的新语法转化为浏览器环境下能够执行的代码。
而编译器的原理是什么可以参考[超级微型编译器](https://github.com/jamiebuilds/the-super-tiny-compiler)

## babel的运行原理
不管是命令行还是集成在打包工具中的babel，运行原理都是一致的。
@babel/core集成了@babel/parser, @babel/traverser, @babel/generator。分别对应了编译的三大阶段：
1. 解析：包括词法分析和语法分析，最终生成AST（抽象语法树。
2. 转换：对AST进行操作，生成新的AST
3. 代码生成

## babel的使用
平常的开发中，几乎上我们都会使用webpack进行打包项目，利用babel-loader来处理使用es6编写的js文件，对babel-loader的配置放在.babelrc中配置。在这个配置文件中分为两大项：presets和plugins。
presets其实就是预设的一组babel的插件集合，现在推荐使用的是@babel/preset-env,默认相当于babel-preset-latest,preset-env的好处在于更加灵活和更加定制化，可针对浏览器进行配置。

### 常见的babel相关工具
1. @babel/preset-env: 提供了更精细化的配置，以提升编译速度，减少代码冗余
   - 配置项：需要支持的平台和平台的版本，如果指定了精确的版本或者范围就可以编译为确定版本不用编译为默认的所有版本的兼容版本，减少代码冗余
2. babel-polyfill
  babel默认只转换新的js语法，而不转换新的API，例如 iterator generator set map等全局对象，以及一些定义在全局对象上的方法，如果想在旧的浏览器上用这些方法，就必须使用babel-polyfill，为当前环境提供一个垫片
3. babel-transform-runtime: babel转译后的代码要实现源代码同样的功能需要借助一些帮助函数，一些帮助函数可能会重复出现在一些模块中，导致编译后的代码体积变大，babel为了解决这个问题提供了单独的runtime供编译模块复用工具函数


相关知识点：
[ast](https://segmentfault.com/a/1190000016231512)
[babel插件](https://juejin.im/post/5a9315e46fb9a0633a711f25)
[babel-preset-env使用指南](https://www.cnblogs.com/chyingp/p/understanding-babel-preset-env.html)
[babel的polyfill和runtime的区别](babel的polyfill和runtime的区别)

按需加载UI库是减少项目大小的有效方法，在typescript项目中如何让antd按需加载是本文所要讲的。

#### 按需加载的原理
在项目中使用antd的方式为
`import { Button } from 'antd'`
这样的引用方式会将antd下的所有模块引入，可以通过以下的写法来按需加载组件：
```js
  import Button from 'antd/es/button';
  import 'antd/es/button/style'; // 或者 antd/es/button/style/css 加载 css 文件
```
但是每次引入组件的时候如果都采取这样的方式显然很不方便，所以antd官方提供了一个babel插件[babel-plugin-import](https://github.com/ant-design/babel-plugin-import)这个插件的作用是在编译你的代码的时候将
`import { Button } from 'antd';`编译为`import { Button } from 'antd';`从而让你不用手动按需引入，提高开发的体验。

#### babel配置
```js
{
  "presets": [
    [
      "env",
      {
        "modules": false
      }
    ],
    // "react",
    "es2015"
  ],
  "plugins": [
    ["import", {
      "libraryName": "antd",
      // "style": "css"
    }],
    ["transform-runtime", {
      "helpers": false,
      "polyfill": false,
      "regenerator": true,
      "moduleName": "babel-runtime"
    }],
  ]
}
```
在`plugins`项中添加`"import"`,并且配置它的`option`为
```js
{
  "libraryName": "antd",
  // "style": "css"
}
```

#### ts项目中的配置
首先要弄清楚ts项目编译的流程，webpack在遇到`.ts`,`.tsx`类型的文件时会先交给`ts-loader`，`ts-loader`根据`tsconfig.json`配置编译我们需要版本的js，然后再将js教给`babel-loader`处理，`babel-loader`会根据项目中的`babelrc`配置来编译js。其中需要注意的是：
1. ts编译输出为`es2015`，也就是支持import的js版本
2. moduleResolution值为`node`

#### 坑
我采用`webpack-bundle-analyzer`来分析项目的打包情况
1. css按需加载的问题
由于组件的css按需加载之后antd的样式文件会晚与项目本身的reset.css，这就是会造成reset.css样式被覆盖的问题，项目中就有`p`标签的margin属性被antd的样式所覆盖，导致样式错乱。想了许久没有想到好的方案：发现好多人有同样的问题，在(issuse)[https://github.com/ant-design/ant-design/issues/4331].
看了之后依然没有啥好的方法，求指点。

2. @ant-design/icons包被全部导入
我发现虽然我只引入了 message, spin, form, input, 但是由于message组件中引入了icon所以，虽然我没有直接使用icon组件还是引入了。并且是所有的icon都被引入。究其原因是在源码中引入icon的方式是`import * as allIcons from '@ant-design/icons/lib/dist';`,所以导致只要有用到的icon组件或者有组件间接引用了icon组件就会出现所有icon资源都被加载的问题。
[解决方式参考](https://www.zhihu.com/question/308898834),原理就是在打包项目的时候将引入icon的地址重定向到自定义的icon文件。

#### 最终效果
添加了按需加载之后从之前的开发环境下index.js（9.21mb）减少到(4.04mb),效果还是很明显的。


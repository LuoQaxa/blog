在研究源码为ts的开源库中，我会通过一个简单的例子做调试进行源码分析，在vscode中如何做到不去编译ts进可以直接调试呢？

1. 开启`tsconfig.json`中的`sourceMap`, 并且需要注意的是为了能够直接使用`import和export`语法，`module`属性需要设置为`commonjs`
2. 配置.vscode/launch.json文件
```json
{
  "name": "Debug Current TS File",
  "type": "node",
  "request": "launch",
  "args": [
    "${relativeFile}"
  ],
  "runtimeArgs": [
    "--nolazy",
    "-r",
    "ts-node/register"
  ],
  "sourceMaps": true,
  "cwd": "${workspaceRoot}",
  "protocol": "inspector",
  "console": "integratedTerminal",
  "internalConsoleOptions": "neverOpen"
}
```
3. 设置断点或者debugger进行调试

[参考](https://segmentfault.com/a/1190000010605261)
[ts-debug-example](https://github.com/MinionsDave/ts-debug-example)
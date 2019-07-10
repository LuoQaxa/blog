#### axios在项目中的封装
axios：基于promise的请求库，实际上就是将xhr请求从之前回调的形式改为了promise的方式。它是现在前端项目请求首选库，本文先从封装讲起，然后阅读分析源码，彻底掌握axios请求库。
#### axios封装目的
1. 设置baseUrl, 并且兼容一个项目中可能会存在多个baseUrl的情况
2. 设置timeout
3. 设置validateStatus，决定当前请求是成功或者是失败
4. 利用axios的一大特性interceptor，做请求拦截和响应拦截

下面是封装代码
```typescript
import axios from 'axios'
import { AxiosRequestConfig, AxiosInstance } from 'axios'
const _config = window.__CONFIG__ //项目不同环境的配置文件
axios.defaults.withCredentials = true
axios.defaults.timeout = 10000
axios.defaults.validateStatus = function (status) {
  return status >= 200 && status < 599 // default
}

// 由于一个项目可能有多个baseURL，所以用一个类来再次封装axios
class Http {
  private instance: AxiosInstance
  constructor(baseURL?: string) {
    this.instance = axios.create({ baseURL })
    this.addRequestInterceptors()
    this.addResponseInterceptors()
  }
  // 请求头部添加token
  addRequestInterceptors() {
    this.instance.interceptors.request.use(config => {
      config.headers.Authorization = localStorage ? 'Bearer ' + localStorage.getItem('token') |''
      return config
    }, error => {
      return Promise.reject(error)
    })
  }
  // 响应拦截，可以对请求失败做统一的处理
  addResponseInterceptors() {
    this.instance.interceptors.request.use(res => {
      res.status <= 300 ? Promise.resolve(res) : Promise.reject(res)
    }, error => {
      // TODO: why error has response attr
      const { response } = error
      this.errorHandle(response.status, response.data.message)
    })
  }
  errorHandle(status, msg) {
    switch(status) {
      case 401:
        console.log('没有权限')
        break;
      default:
        console.log(msg)
    }
  }
  public get(url, configs?:Object) {
    return this.instance({
      method: 'get',
      url: url,
      ...configs,
    })
  }
  public post(url, data?, configs?:Object) {
    return this.instance({
      method: 'post',
      url: url,
      data: data,
      ...configs,
    })
  }
  public put(url, data?, configs?:Object) {
    return this.instance({
      method: 'put',
      url: url,
      data: data,
      ...configs,
    })
  }
  public patch(url, data?, configs?:Object) {
    return this.instance({
      method: 'patch',
      url: url,
      data: data,
      ...configs,
    })
  }
  public delete(url, configs?:Object) {
    return this.instance({
      method: 'delete',
      url: url,
      ...configs,
    })
  }
}

const API = new Http(_config.api.host)
export default API
```
#### 封装遇到的问题
1. 为什么axios默认导出实例，为什么没有导出Axios类?
从axios的源码来找答案导出代码如下：
```js

const axios = createInstance(defaults)

axios.Axios = Axios

export default axios
```
默认导出的这个`axios`实例是通过一个`createInstance`函数来创建的，传入了默认的配置`defaults`，在`createInstance`函数中首先创建了`Axios`类的实例，使得这个实例拥有了`defaults`的配置。这也就是为什么导出一个实例而非导出类的原因，这个实例能够拥有默认配置，直接就可以方便的通过这个实例发起请求。


2. 为什么设置了实例的静态属性后就能够在不同的实例间共享属性？
```js
const API1 = new Http('first')
const API2 = new Http('second)
console.log(API1.instance.defaults) //true
console.log(API2.instance.defaults) //true
```
可以发现这个两个实例都拥有相同的设置的defaults属性。而我们知道一个类的实例属性不能共享，这个共享的原因在于：1. axios.defaults属性和defaults对象有着相同的对象引用，2. 在`Http`类中调用了`this.instance = axios.create({})`,而`create`方法中合并了defaults对象和传入的config对象，使得每一个实例都用到了defaults对象。
```js
axios.create = function create(config) {
  return createInstance(mergeConfig(defaults, config))
}
```
3. 拦截器可以保证顺序执行，它的原理是什么？
axios实例上有一个`interceptors`属性它的有两个属性分别为`request`和`response`用于存储各自的拦截器，拦截器为`InterceptorManager`实例，实例拥有`use, forEach, eject`方法和`interceptors`数组属性，`use`方法用于注册拦截器：
```js
// use
use(resolved, rejected) {
  this.interceptors.push({
    resolved,
    rejected
  })
  return this.interceptors.length - 1
}
```
知道了如何注册拦截器，再来看看请求的时候是如何做到顺序执行：请求拦截->请求—>响应拦截
从Axios类的request函数：
```js
const chain = [{
  resolved: dispatchRequest  //实际发送请求的函数
  rejected: undefined
}]

this.interceptors.request.forEach(interceptor => {
  // request 拦截器先添加的后执行
  chain.unshift(interceptor)
})

this.interceptors.response.forEach(interceptor => {
  // response 拦截器先添加的先执行
  chain.push(interceptor)
})

// 这时候的chain就是一个按照我们希望顺序的执行数组，数组都每一项都是为{ resolved: fn, reject: fn | undefined }格式

// 创建一个初始化的promise，将现有的config传入
let promise = Promise.resolve(config)


// 不断的取出chain中的项执行
while(chain.length) {
  const { resolve, rejected } = chain.shift()
  promise = promise.then(resolve, rejected)
}

return promise
```
主要在于利用了promise来保证了不管同步还是异步的步骤都能够按照chain数组的顺序来执行。

#### axios源码拾遗
axios实例可以直接调用发起请求，这个是为什么？
```js
axios({
  url: 'xxx',
  method: 'get'
})
```
原因在于
```js
function createInstance(config: AxiosRequestConfig): AxiosStatic {
  const context = new Axios(config)
  const instance = Axios.prototype.request.bind(context)

  extend(instance, context)

  return instance as AxiosStatic
}
```
首先创建了一个实例context，然后将context作为上下文创建bind了request方法（真正发起请求的方法）并返回的新的函数赋值给了instance，然后调用`extend(instance, context)`让instance函数拥有了context其他属性和方法，并返回instance。这样就让一个类的实例就可以作为request方法直接调用了，很巧妙。

#### 封装遗留的问题
1. 请求超时如何统一处理。
2. 如何处理取消请求，比如如何在axios里面防止表单快速点击重复提交。

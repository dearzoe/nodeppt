title: 分享
speaker: 文哲
url: https://huwenzhe.com
transition: move
theme: dark
highlightStyle: monokai_sublime
date: 2018年07月18日  
files: /js/demo.js,/css/demo.css

[slide]

![蓝鸟](/img/blue.png)
## bluebird

[slide]

#  &nbsp; {:&.flexbox.vleft}
## bluebird是一个第三方的Promise规范实现库
- 完全兼容原生Promise对象
- 原生对象功能更强大。

[slide]

#  &nbsp; {:&.flexbox.vleft}
## Promise对象
Promise对象已在es6中做为JavaScript的标准内置对象提供，这个对象根据Promise A+规范实现，相对比较简单。除从Object对象中继承对象属性/方法外，它还有以下Promise自身的属性/方法。

[slide]

#  &nbsp; {:&.flexbox.vleft}
### Promise中的类方法(静态方法[不需要实例化])
- Promise.all(promiseArray) - 将多个Promise实例包装成一个新实例，多个实例会同时执行成功或失败
- Promise.race(promiseArray) - 将多个Promise实例包装成一个新实例，实例中的任何一个实例执行成功或失败将返回
- Promise.resolve(obj) - 将对象包装成resolve状态的Promise实例
- Promise.reject(obj) - 将对象包装成reject状态的Promise实例

[slide]

#  &nbsp; {:&.flexbox.vleft}
### Promise中的实例方法(创建Promise实例后才能使用的方法[被添加到Promise.prototype]){:&.flexbox.vleft}
- promise.then(onFulfilled, onRejected) - 执行成功(或/与)失败的处理
- promise.catch(onRejected) - 执行失败的处理

[slide]

3

[slide]

4
title: 分享
speaker: 文哲
url: https://huwenzhe.com
transition: move
theme: moon
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
            - 比原生对象功能更强大。

[slide]

#  &nbsp; {:&.flexbox.vleft}
## Promise对象
Promise对象已在**es6**中做为**JavaScript**的标准内置对象提供，这个对象根据**Promise A+**规范实现，相对比较简单。除从Object对象中继承对象属性/方法外，它还有以下Promise自身的属性/方法。

[slide]

#  &nbsp; {:&.flexbox.vleft}
### Promise中的类方法(静态方法[不需要实例化])
- **Promise.all(promiseArray)** - 将多个Promise实例包装成一个新实例，多个实例会同时执行成功或失败
- **Promise.race(promiseArray)** - 将多个Promise实例包装成一个新实例，实例中的任何一个实例执行成功或失败将返回
- **Promise.resolve(obj)** - 将对象包装成resolve状态的Promise实例
- **Promise.reject(obj)** - 将对象包装成reject状态的Promise实例

[slide]

#  &nbsp; {:&.flexbox.vleft}
### Promise中的实例方法(创建Promise实例后才能使用的方法[被添加到Promise.prototype])
- **promise.then(onFulfilled, onRejected)** - 执行成功(或/与)失败的处理
- **promise.catch(onRejected)** - 执行失败的处理

[slide]

#  &nbsp; {:&.flexbox.vleft}
### bluebird模块
bluebird是一个第三方的Promise实现，我们可通过npm命令来安装：
```javascript
npm install bluebird
```
模块安装后，可以就可以通过require获取对模块的引用：
```javascript
const Promise = require('bluebird');        
const promise = new Promise((resolve, reject) => {
  const value = Math.random();
  if (value > 0.5) {
    resolve(value);
  } else {
    reject(`Invalid value ${value}`);
  }
});    
promise.then(console.log).catch(console.error);
```

[slide]


## 1.不同点（核心）

![蓝鸟](/img/b1.jpg)

[slide]

#  &nbsp; {:&.flexbox.vleft}

###### [.spread](http://fanyi.baidu.com/?aldtype=85#en/zh/spread)
&nbsp;
```javascript
Promise.resolve([1, 2, 3])
 .spread((v1, v2, v3) => console.log(v1 + v2 + v3));
//6
```

[slide]


## 2.不同点（同步检查）

![蓝鸟](/img/b2.jpg)

[slide]

#  &nbsp; {:&.flexbox.vleft}

###### [.isFulfilled](http://fanyi.baidu.com/?aldtype=85#en/zh/Fulfilled)
&nbsp;
```javascript
const p = new Promise(rs => setTimeout(rs, 1000));

console.log(p.isFulfilled())
setTimeout(()=>{console.log(p.isFulfilled())},2000)
//false
//true
```

[slide]


## 3.不同点（集合操作）

![蓝鸟](/img/b3.jpg)

[slide]

#  &nbsp; {:&.flexbox.vleft}

###### [.some](http://fanyi.baidu.com/?aldtype=85#en/zh/some)
&nbsp;
```javascript
const p1 = new Promise(rs => setTimeout(rs, 1000));
const p2 = new Promise(rs => setTimeout(rs, 3000));
Promise.some([p1,p2], 1)
    .then(()=>{
        console.log('Result')
    })
//Result （3s）  
//不填写第二参数：Unhandled rejection TypeError: expecting a positive integer    
```

[slide]


## 4.不同点（资源管理器）

![蓝鸟](/img/b4.jpg)

[slide]


## 5.不同点（包装器）

![蓝鸟](/img/b5.jpg)

[slide]

#  &nbsp; {:&.flexbox.vleft}

###### [.promisify](http://fanyi.baidu.com/?aldtype=85#en/zh/promisify)
&nbsp;
```javascript
var readFile = Promise.promisify(require("fs").readFile);

readFile("myfile.js", "utf8")
    .then(function(contents) {
        return eval(contents);
    })
    .then(function(result) {
        console.log("The result of evaluating myfile.js", result);
    });
```

[slide]


## 6.不同点（定时器）

![蓝鸟](/img/b6.jpg)

[slide]

#  &nbsp; {:&.flexbox.vleft}

###### [.delay / .timeout](http://fanyi.baidu.com/?aldtype=85#en/zh/delay%0Atimeout)
&nbsp;
```javascript
// 一秒后，输出 hello
Promise.delay(1000, 'hello').then(console.log);  
```

```javascript
//0.5s超时
Promise.delay(1000, 'hello')
    .timeout(500, 'timed out')
    .then(console.log)          
    .catch(console.error);//TimeoutError: timed out
```

[slide]


## 7.不同点（工具方法）

![蓝鸟](/img/b7.jpg)

[slide]

#  &nbsp; {:&.flexbox.vleft}

###### [.call](http://fanyi.baidu.com/?aldtype=85#en/zh/call)
&nbsp;
```javascript
var Promise = require("bluebird");
var fs = Promise.promisifyAll(require("fs"));
var path = require("path");
var thisPath = process.argv[2] || ".";
var now = Date.now();

fs.readdirAsync(thisPath)
    .map(function(fileName) {
        return fs.statAsync(path.join(thisPath, fileName));
    })
    .call("some", function(stat) {
        return (now - new Date(stat.mtime)) < 10000;
    })
    .then(function(someFilesHaveBeenModifiedLessThanTenSecondsAgo) {
        console.log(someFilesHaveBeenModifiedLessThanTenSecondsAgo);
    });
```

[slide]

end



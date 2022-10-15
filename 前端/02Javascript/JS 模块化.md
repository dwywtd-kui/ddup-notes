## 什么是模块化
**将一个大程序拆分成互相依赖的小文件，再用简单的方法拼装起来。**其他语言都有这项功能，比如 Ruby 的require、Python 的import。
块的内部数据与实现是私有的, 只是向外部暴露一些接口(方法)与外部其它模块通信。
## 为什么要模块化
因为在实际的开发过程中，经常会遇到变量、函数、对象等名字的冲突，这样就容易造成冲突，还会造成全局变量被污染；
同时，程序复杂时需要写很多代码，而且还要引入很多类库，这样稍微不注意就容易造成文件依赖混乱；
为了解决上面的的问题，我们才开始使用模块化的js，所以说模块化的作用就是：

- 避免全局变量被污染
- 便于代码编写和维护
## 模块化的发展进程
### 1、普通写法（全局函数和变量）
其实只要是不同的函数或变量放一起就是简单的模块，这样弊端很明显，就是**名称容易冲突，变量容易被污染**；

- module1.js
```javascript
//数据
let data = 'atguigu.com'

//操作数据的函数
function foo() {
  console.log(`foo() ${data}`)
}
function bar() {
  console.log(`bar() ${data}`)
}
```

- module2.js
```javascript
let data2 = 'other data'

function foo() {  //与另一个模块中的函数冲突了
  console.log(`foo() ${data2}`)
}
```

- test.html
```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8">
    <title>Title</title>

    <script type="text/javascript" src="module1.js"></script>
    <script type="text/javascript" src="module2.js"></script>
    <script type="text/javascript">
      let data = "修改后的数据";
      foo();
      bar();
    </script>
  </head>
  <body>
    TEST
  </body>
</html>
```
###  2、对象封装
就是将整个模块放在一个对象里面，外部访问时直接调用对象的属性或者方法就行：

- module1.js
```javascript
let myModule = {
  data: 'atguigu.com',
  foo() {
    console.log(`foo() ${this.data}`)
  },
  bar() {
    console.log(`bar() ${this.data}`)
  }
}
```

- module2.js
```javascript
let myModule2 = {
  data: 'atguigu.com2222',
  foo() {
    console.log(`foo() ${this.data}`)
  },
  bar() {
    console.log(`bar() ${this.data}`)
  }
}
```
 

- test.html
```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8">
    <title>Title</title>

    <script type="text/javascript" src="module1.js"></script>
    <script type="text/javascript" src="module2.js"></script>
    <script type="text/javascript">
        myModule.foo()
        myModule.bar()
      
        myModule2.foo()
        myModule2.bar()
      
        myModule.data = 'other data' //能直接修改模块内部的数据
        myModule.foo()
      </script>
  </head>
  <body>
    TEST
  </body>
</html>
```

这种方法虽然**解决了变量冲突问题**，但本质上是对象，容易被外部随意修改，不安全。
### 3、匿名函数方式

- module3.js
```javascript
(function (window) {
  //数据
  let data = 'atguigu.com'

  //操作数据的函数
  function foo() { //用于暴露有函数
    console.log(`foo() ${data}`)
  }

  function bar() {//用于暴露有函数
    console.log(`bar() ${data}`)
    otherFun() //内部调用
  }

  function otherFun() { //内部私有的函数
    console.log('otherFun()')
  }

  //暴露行为
  window.myModule = {foo, bar}
})(window)
```
```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8">
    <title>Title</title>

    <script type="text/javascript" src="module3.js"></script>
    <script type="text/javascript">
      myModule.foo()
      myModule.bar()
      //myModule.otherFun()  //myModule.otherFun is not a function
      console.log(myModule.data) //undefined 不能访问模块内部数据
      myModule.data = 'xxxx' //不是修改的模块内部的data
      myModule.foo() //没有改变
    
    </script>
  </head>
  <body>
    TEST
  </body>
</html>
```
这样就实现了变量不被随意修改的问题。匿名函数方式基本上解决了函数污染及变量随意被修改问题。
问题：问题: 如果当前这个模块依赖另一个模块怎么办?
4、匿名函数方式增强
引入jquery到项目中 

- module4.js
```javascript
(function (window, $) {
  //数据
  let data = 'atguigu.com'

  //操作数据的函数
  function foo() { //用于暴露有函数
    console.log(`foo() ${data}`)
    $('body').css('background', 'red')
  }

  function bar() {//用于暴露有函数
    console.log(`bar() ${data}`)
    otherFun() //内部调用
  }

  function otherFun() { //内部私有的函数
    console.log('otherFun()')
  }

  //暴露行为
  window.myModule = {foo, bar}
  
})(window, jQuery)
```
```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8">
    <title>Title</title>

    <script type="text/javascript" src="jquery-1.10.1.js"></script>
    <script type="text/javascript" src="module4.js"></script>
    <script type="text/javascript">
      myModule.foo()
    </script>
  </head>
  <body>
    TEST
  </body>
</html>
```
这就是现在模块实现的基石。
### 5、引入多个script标签后出现的问题
当一个页面要引用很多js文件时，需要加载多个请求，出现以下问题：

- 请求过多（依赖的模块过多，请求就会过多）；
- 依赖模糊（不知道模块的具体依赖关系，导致加载顺序出错）；
- 难以维护（以上两个原因就会造成这个结果）。
```html
//index.html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8">
    <title>Title</title>
    <script type="text/javascript" src="module1.js"></script>
    <script type="text/javascript" src="module2.js"></script>
    <script type="text/javascript" src="module3.js"></script>
    <script type="text/javascript" src="module4.js"></script>

  </head>
  <body>
    <div>Test</div>
  </body>
</html>
```
这些问题可以通过现代模块化编码和项目构建来解决。
### 6、模块化方案
根据匿名函数自调用的方式，同时为了增强代码依赖性，现在大部分JavaScript运行环境都有自己的模块化规范；
可以分为：Commonjs、AMD、CMD、ES6 module四大类。
## 如何实现模块化
### CommonJS
地址：[http://wiki.commonjs.org/wiki/Modules/1.1](http://wiki.commonjs.org/wiki/Modules/1.1)

Node.js 就是基于commonJS模块规范，每一个文件就是一个模块；有自己的作用域；在服务器端，模块的加载是同步的；在浏览器端，模块需提前编译打包处理
特点：

- 所有代码都运行在模块作用域，不会污染全局作用域；
- 模块可以多次加载，但是只会在第一次加载时运行一次，然后运行结果就被缓存了，以后再加载，就直接读取缓存结果。要想让模块再次运行，必须清除缓存。
- 模块加载的顺序，按照其在代码中出现的顺序。

CommonJS模块的加载机制是，输入的是被输出的值的拷贝。也就是说，一旦输出一个值，模块内部的变化就影响不到这个值
语法：
    暴露模块：`module.exports = value` 或者 `exports.xxx = value`
    引入模块：`require('xxx')` 如果是第三方模块，xxx为模块名；如果是自定义模块，xxx为模块文件路径

CommonJS规范规定，每个模块内部，module变量代表当前模块。这个变量是一个对象，它的exports属性（即module.exports）是对外的接口。加载某个模块，其实是加载该模块的module.exports属性。

require命令用于加载模块文件。require命令的基本功能是，读入并执行一个JavaScript文件，然后返回该模块的exports对象。如果没有发现指定模块，会报错。
#### 服务端实现 Node.js

1. 下载安装node.js
2. 创建项目结构
> |-modules
> |-module1.js
> |-module2.js
> |-module3.js
> |-app.js
> |-package.json
>   {
>     "name": "commonJS-node",
>     "version": "1.0.0"
>   }


3. 下载第三方模块
> npm install uniq --save

4. 模块化编码
- module1.js
```javascript
module.exports = {
  foo() {
    console.log('moudle1 foo()')
  }
}
```

- module2.js
```javascript
module.exports = function () {
  console.log('module2()')
}
```

- module3.js
```javascript
exports.foo = function () {
  console.log('module3 foo()')
}

exports.bar = function () {
  console.log('module3 bar()')
}
```

- app.js
```javascript
/**
  1. 定义暴露模块:
    module.exports = value;
    exports.xxx = value;
  2. 引入模块:
    var module = require(模块名或模块路径);
 */
"use strict";
//引用模块
let module1 = require('./modules/module1')
let module2 = require('./modules/module2')
let module3 = require('./modules/module3')

let uniq = require('uniq')
let fs = require('fs')

//使用模块
module1.foo()
module2()
module3.foo()
module3.bar()

console.log(uniq([1, 3, 1, 4, 3]))

fs.readFile('app.js', function (error, data) {
  console.log(data.toString())
})
```

5. 通过node运行app.js
> node app.js

#### 浏览器端实现 Browserify
> [http://browserify.org/](http://browserify.org/)
> 也称为CommonJS的浏览器端的打包工具

1. 创建项目结构
```
|-js
  |-dist //打包生成文件的目录
  |-src //源码所在的目录
    |-module1.js
    |-module2.js
    |-module3.js
    |-app.js //应用主源文件
|-index.html
|-package.json
  {
    "name": "browserify-test",
    "version": "1.0.0"
  }
```

2. 下载browserify
- 全局: npm install browserify -g
- 局部: npm install browserify --save-dev

3. 定义模块代码
- module1.js
```javascript
module.exports = {
  foo() {
    console.log('moudle1 foo()')
  }
}
```
 

- module2.js
```javascript
module.exports = function () {
  console.log('module2()')
}
```
 

- module3.js
```javascript
exports.foo = function () {
  console.log('module3 foo()')
}

exports.bar = function () {
  console.log('module3 bar()')
}
```
 

- app.js (应用的主js)
```javascript
//引用模块
let module1 = require('./module1')
let module2 = require('./module2')
let module3 = require('./module3')

let uniq = require('uniq')

//使用模块
module1.foo()
module2()
module3.foo()
module3.bar()

console.log(uniq([1, 3, 1, 4, 3]))
```
 

4. 使用browserify 打包处理js
> browserify js/src/app.js -o js/dist/bundle.js


5. 浏览器页面使用引入
```html
<script type="text/javascript" src="js/dist/bundle.js"></script>
```
 
### AMD
### CMD
### ES6
在 ES6 之前，社区制定了一些模块加载方案，最主要的有 CommonJS 和 AMD 两种。前者用于服务器，后者用于浏览器。ES6 在语言标准的层面上，实现了模块功能，而且实现得相当简单，完全可以取代 CommonJS 和 AMD 规范，成为浏览器和服务器通用的模块解决方案。
#### ES6-Babel-Browserify使用教程

1. 定义package.json文件
```json
{
  "name" : "es6-babel-browserify",
  "version" : "1.0.0"
}
```

2. 安装babel-cli, babel-preset-es2015和browserify

> npm install babel-cli browserify -g 
> npm install babel-preset-es2015 --save-dev


3. 定义.babelrc文件
```json
{
  "presets": ["es2015"]
}
```

4. 编码

- js/src/module1.js
```javascript
export function foo() {
  console.log('module1 foo()');
}
export let bar = function () {
  console.log('module1 bar()');
}
export const DATA_ARR = [1, 3, 5, 1]
```
 

- js/src/module2.js
```javascript
let data = 'module2 data'

function fun1() {
  console.log('module2 fun1() ' + data);
}

function fun2() {
  console.log('module2 fun2() ' + data);
}

export {fun1, fun2}
```
 

- js/src/module3.js
```javascript
export default {
  name: 'Tom',
  setName: function (name) {
    this.name = name
  }
}
```
 

- js/src/app.js
```javascript
import {foo, bar} from './module1'
import {DATA_ARR} from './module1'
import {fun1, fun2} from './module2'
import person from './module3'

import $ from 'jquery'

$('body').css('background', 'red')

foo()
bar()
console.log(DATA_ARR);
fun1()
fun2()

person.setName('JACK')
console.log(person.name);
```

5. 编译
> 1. 使用Babel将ES6编译为ES5代码(但包含CommonJS语法)  `babel js/src -d js/lib`
> 2. 使用Browserify编译 `browserify js/lib/app.js -o js/lib/bundle.js`


6. 页面中引入测试
```html
<script type="text/javascript" src="js/lib/bundle.js"></script>
```

7. 引入第三方模块(jQuery)
> （1）下载jQuery模块: 
> npm install jquery@1 --save
> （2）在app.js中引入并使用


```javascript
import $ from 'jquery'
$('body').css('background', 'red')
```
参考阅读：

1. [https://www.jb51.net/article/211103.htm](https://www.jb51.net/article/211103.htm)
2. [https://wangdoc.com/es6/module.html](https://wangdoc.com/es6/module.html)
3. [https://www.jb51.net/article/233074.htm](https://www.jb51.net/article/233074.htm)

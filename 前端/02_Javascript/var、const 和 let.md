## 使用var声明变量
在 JavaScript 中通常使用 var 关键词来声明变量：
`var carname;`
变量声明之后，该变量是空的（它没有值），未赋值声明的变量，其值实际上是 `undefined`。如需向变量赋值，请使用等号：
`carname="Volvo";`
不过，也可以在声明变量时对其赋值：
`var carname="Volvo";`
也可以在一条语句中声明很多变量。该语句以 var 开头，并使用逗号分隔变量即可：
`var lastname="Doe", age=30, job="carpenter";`
但一条语句中声明的多个变量不可以同时赋同一个值:
`var x,y,z=1;` x,y 为 `undefined`， z 为 1。
如果重新声明 JavaScript 变量，该变量的值不会丢失：
`var carname="Volvo";`
`var carname;`
两条语句执行后，变量 carname 的值依然是 "Volvo"
## JavaSript 作用域
作用域是可访问变量的集合。
### 局部作用域和局部变量
变量在函数内声明，变量为局部变量，具有局部作用域。局部变量只能在函数内部访问。
```javascript
// 此处不能调用 carName 变量
function myFunction() {
    var carName = "Volvo";
    // 函数内可调用 carName 变量
}
```
因为局部变量只作用于函数内，所以不同的函数可以使用相同名称的变量。局部变量在函数开始执行时创建，函数执行完后局部变量会自动销毁。
另外函数参数只在函数内起作用，是局部变量。
### 全局作用域和全局变量
变量在函数外定义，即为全局变量，具有全局作用域。 全局变量正在网页中所有脚本和函数均可使用。
```javascript
var carName = " Volvo";
 
// 此处可调用 carName 变量
function myFunction() {
    // 函数内可调用 carName 变量
}
```
如果变量在函数内没有声明（没有使用 var 关键字），该变量为全局变量。
```javascript
// 此处可调用 carName 变量
 
function myFunction() {
    carName = "Volvo";
    // 此处可调用 carName 变量
}
```
### 小结
JavaScript 变量生命周期在它声明时初始化。局部变量在函数执行完毕后销毁。全局变量在页面关闭后销毁。
变量在函数内声明，变量为局部变量。变量在函数外定义，即为全局变量。
函数参数只在函数内起作用，是局部变量。

## const 和 let
ES2015(ES6) 新增加了两个重要的 JavaScript 关键字: let 和 const。

- let 声明的变量只在 let 命令所在的代码块内有效。
- const 声明一个只读的常量，一旦声明，常量的值就不能改变。

在 ES6 之前，JavaScript 只有两种作用域变量类别： 全局变量与函数内的局部变量。
```javascript
var carNameA = "A";
 
// 这里可以使用 carNameA 变量
// 这里不可以使用 carNameB 变量
 
function myFunction() {
    var carNameB = "B";
    // 这里可以使用 carNameB 变量
    // 这里也可以使用 carNameA 变量
}

// 这里可以使用 carNameA 变量
// 这里不可以使用 carNameB 变量
```
在函数外声明的变量作用域是全局的，在函数内声明的变量作用域是局部的。
### JavaScript 代码块级作用域
使用 var 关键字声明的变量不具备块级作用域的特性，它在 {} 外依然能被访问到。
```javascript
{ 
    var x = 2; 
}
// 这里可以使用 x 变量
```

在 ES6 之前，是没有块级作用域的概念的。ES6 可以使用 let 关键字来实现块级作用域。let 声明的变量只在 let 命令所在的代码块 {} 内有效，在 {} 之外不能访问。
```javascript
{ 
    let x = 2;
}
// 这里不能使用 x 变量
```

使用 var 关键字重新声明变量可能会带来问题。在块中重新声明变量也会重新声明块外的变量：
```javascript
var x = 10;
// 这里输出 x 为 10
{ 
    var x = 2;
    // 这里输出 x 为 2
}
// 这里输出 x 为 2
```
let 关键字就可以解决这个问题，因为它只在 let 命令所在的代码块 {} 内有效。
```javascript
var x = 10;
// 这里输出 x 为 10
{ 
    let x = 2;
    // 这里输出 x 为 2
}
// 这里输出 x 为 10
```
这种现象在for循环中特别明显：
```javascript
var i = 5;
for (var i = 0; i < 10; i++) {
    // 一些代码...
}
// 这里输出 i 为 10。因为：使用了 var 关键字，它声明的变量是全局的，包括循环体内与循环体外。

let j = 5;
for (let j = 0; j < 10; j++) {
    // 一些代码...
}
// 这里输出 j 为 5。因为：使用 let 关键字， 它声明的变量作用域只在循环体内，循环体外的变量不受影响。
```

### HTML 代码中使用全局变量
在 JavaScript 中, 全局作用域是针对 JavaScript 环境。在 HTML 中, 全局作用域是针对 window 对象。使用 var 关键字声明的全局作用域变量属于 window 对象：
```javascript
var carName = "Volvo";
// 可以使用 window.carName 访问变量
```
使用 let 关键字声明的全局作用域变量不属于 window 对象:
```javascript
let carName = "Volvo";
// 不能使用 window.carName 访问变量
```
### 重置变量
使用 var 关键字声明的变量在任何地方都可以修改：
```javascript
var x = 2;
// x 为 2
var x = 3;
// 现在 x 为 3
```
在相同的作用域或块级作用域中，不能使用 let 关键字来重置 var 关键字声明的变量:
```javascript
var x = 2;       // 合法
let x = 3;       // 不合法

{
    var x = 4;   // 合法
    let x = 5   // 不合法
}
```
在相同的作用域或块级作用域中，不能使用 let 关键字来重置 let 关键字声明的变量:
```javascript
let x = 2;       // 合法
let x = 3;       // 不合法

{
    let x = 4;   // 合法
    let x = 5;   // 不合法
}
```
在相同的作用域或块级作用域中，不能使用 var 关键字来重置 let 关键字声明的变量:
```javascript
let x = 2;       // 合法
var x = 3;       // 不合法

{
    let x = 4;   // 合法
    var x = 5;   // 不合法
}
```
let 关键字在不同作用域，或不同块级作用域中是可以重新声明赋值的:
```javascript
let x = 2;       // 合法

{
    let x = 3;   // 合法
}

{
    let x = 4;   // 合法
}
```

### 变量提升
JavaScript 中，var 关键字定义的变量可以在使用后声明，也就是变量可以先使用再声明（JavaScript 变量提升）。
```javascript
// 在这里可以使用 carName 变量

var carName;
```
let 关键字定义的变量则不可以在使用后声明，也就是变量需要先声明再使用。
```javascript
// 在这里不可以使用 carName 变量

let carName;
```
## const 关键字
const 用于声明一个或多个常量，声明时必须进行初始化，且初始化后值不可再修改:
```javascript
const PI = 3.141592653589793;
PI = 3.14;      // 报错
PI = PI + 10;   // 报错
```

const定义常量与使用let 定义的变量相似：

- 二者都是块级作用域
- 都不能和它所在作用域内的其他变量或函数拥有相同的名称

两者还有以下两点区别：

- const声明的常量必须初始化，而let声明的变量不用
- const 定义常量的值不能通过再赋值修改，也不能再次声明。而 let 定义的变量值可以修改。

## 综合比较 var、let 与 const
使用var关键字声明的全局作用域变量属于window对象。
使用let和const关键字声明的全局作用域变量不属于window对象。

使用var关键字声明的变量在任何地方都可以修改。
在相同的作用域或块级作用域中，不能使用let关键字来重置var关键字声明的变量。
在相同的作用域或块级作用域中，不能使用let关键字来重置let关键字声明的变量。
在相同的作用域或块级作用域中，不能使用const关键字来重置var和let关键字声明的变量。
在相同的作用域或块级作用域中，不能使用const关键字来重置const关键字声明的变量

let 和 const 关键字在不同作用域，或不用块级作用域中是可以重新声明赋值的_（因为块级作用域，已经不是之前那个变量了）_。

var关键字定义的变量可以先使用后声明。
let和const关键字定义的变量需要先声明再使用。

const关键字定义的常量，声明时必须进行初始化，且初始化后不可再修改。
## 参考

1. JavaScript 变量：[https://www.runoob.com/js/js-variables.html](https://www.runoob.com/js/js-variables.html)
2. JavaScript 作用域：[https://www.runoob.com/js/js-scope.html](https://www.runoob.com/js/js-scope.html)
3. JavaScript let 和 const：[https://www.runoob.com/js/js-let-const.html](https://www.runoob.com/js/js-let-const.html)




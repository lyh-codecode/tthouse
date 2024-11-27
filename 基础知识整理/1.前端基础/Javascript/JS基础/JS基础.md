# JS基础

## 1.JS是什么/预编译

脚本编程语言，允许我们在网页上实现复杂功能

执行代码前会先预编译，预编译结束代码才执行，函数提升，声明提升，赋值不提升

##### 预编译步骤

1.创建AO对象 

2.找形参和变量声明，变量和形参名作为AO对象的属性名，值为undefined

3.实参值和形参统一

4.在函数体里面找函数声明，值赋予函数体



## 2.1 JS输出

1.js显示方案
window.alert() 写入警告框
document.write() 写入HTML输出
innerHTML 写入HTML元素
console.log() 写入控制台
	

2.使用innerHTML

1.访问html元素可以使用 document.getElementById(id) 获取元素

2.获取元素之后对元素进行操作/赋值
	
3.使用document.write()
括号内容直接输出到页面
在 HTML 文档完全加载后使用 document.write() 将删除所有已有的 HTML 
	
4.使用 console.log()







## 2.2JS语句

### 一些概念

1.JavaScript 语句由以下构成：

​    值、运算符、表达式、关键词和注释

​    JavaScript 会忽略多个空格。

2.代码块{    }

​    用花括号定义一同执行的语句 

   3.关键字    debugger    停止执行 JavaScript，并调用调试函数

function    声明函数 

return      退出函数

var         声明变量



### 语法

1.定义变量
定义变量的时候有const，let，var

遵循原则：
先用const，等到变量要修改时改为let
var可以先用后声明（提升变量），但是提升声明不赋值
少用var



2. =     赋值

  ==	  判断是否相等

  ===	  等值等类型

  !==   不等值或不等型

  其他的感觉和C基本上没有区别

  法大部分来说感觉和C大差不差		





3.数据类型

数值，字符串，数组，对象，布尔等
js是弱数据类型语言，要通过一些操作才能确定数据类型

例如 var x; undefined
x = 7; 现在是数值
x = "bill"; 现在是字符串

注意：null和undefined等值不等型

null表示一个空对象引用。需要明确表示变量为空时，通常会将其赋值为 null
undefined表示一个变量声明但未初始化，或者访问对象不存在的属性
避免将变量显式赋值为 undefined，推荐用 null 表示空值或者用更明确的逻辑来处理变量的状态

数值和字符串相加会变字符串

一些数字可能是字符串，为了确保数字为数值可以在数字前面加个 +



用typeof运算符确定js变量的数据类型
用typeof运算符确定js变量的数据类型



	1.typeof "bill" ==> 返回string
	2.typeof 运算符对数组返回 "object"，因为在 JavaScript 中数组属于对象	

4.箭头函数

​	让表达式更加简洁，替代原来需要匿名函数的地方

```JS
const fn = ( x ) => {

			函数体

	}

```



​		



## 2.3函数/对象

### 2.3.1函数

#### 1.函数是特定代码块，被调用时执行

例如

```javascript
function myFunction(p1, p2) {
    return p1 * p2;              // 该函数返回 p1 和 p2 的乘积
}
```



#### 2.为什么使用函数

​	2.1代码复用，可以一次定义多次调用

​	2.2模块化，更易理解和维护

​	2.3提高可读性，条理清晰，更易维护和修改



#### 3.函数传参和返回值

​	3.1封装函数时设置形参，调用时传实参

​	3.2 返回值 return 数据

​		函数执行完毕了之后，把任务结果返回给我们

​		用变量接住return值



#### 4.作用域

​	函数内部定义的变量为局部变量，函数外面就不能使用，var除外

​	全局变量可以全局使用

​		作用据是为了提高逻辑的局部性，减少名字冲突

​	

​	一个小坑：函数内部变量没有声明，直接赋值，当作全局变量看（不推荐）



#### 5.匿名函数

```js
//具名函数
function fn(){
}
fn()



//匿名函数
let fn = function() {
    我是表达式
}

fn()
```



#### 6.立即执行函数

```js
(函数)()
(function(){
    我是表达式
})()
```



#### 7.箭头函数

用于回调函数或者简单函数的定义

使用箭头函数没有对 `this` 的绑定

用了箭头函数，则 `this` 表示函数的拥有者

```js
const func1 = () => {
  // 函数体
};

const func2 = (param) => {
  // 函数体
};

const func4 = () => expression;
```



### 2.3.2对象

#### 1.对象的定义

​	一种数据类型 object

​		  一种无序的数据集合

​		  用来描述某个事物

​	几乎js中所有的事物都是对象（除了原始值，都是对象）

​	**原始值**指的是没有属性或方法的值

​	对象的组成 	属性 + 方法

```js
let 对象名 = {
	属性名：属性值,
	方法名：函数
}
```



#### 2.对象操作

##### 属性

```
访问 对象名.属性 /或者用数组下标形式
修改 对象名.属性 = 新值
增加 对象名.新属性 = 新值
删除 delete 对象.属性
```



##### 方法

​	在对象里面的函数，直接	对象名.方法() 调用



#### 3.对象遍历

​	for in 遍历对象，但是得到的属性值有 ' '

```js
for (let k in obj) {
//k获得属性名,但是是字符串 比如name属性 ==> k = 'name'
	console.log(obj.k) //直接报错
    
	console.log(obj[k])
}	

```



#### 4.内置对象

​	js内部定义的对象，主要使用数学对象

​		document.write()

​		console.log()

**数学对象** Math

​	random 生成0-1之间的随机数

​	ceil 向上取整	

​	floor 向下取整

​	max/min 找最大最小值

​	pow 幂运算 

​	abs 绝对值

```
调用直接这样
	Math.ceil(1.2)
```





#### 5.创建对象

​	用变量 = new 对象名(我是参数)





## 3.事件

#### 1.什么是事件

事件是正在编程的系统中发生的事情，事件发生时系统会产生某种信号，提供一种机制，然后执行一个操作

例如用户选择，单击，悬停在某个元素上

键盘事件，提交表格，视频播放，暂停，结束等



#### 2.触发事件的方法

1.用addEventListener绑定事件对象

```js
const btn = document.querySelector("button");

function random(number) {
  return Math.floor(Math.random() * (number + 1));
}

btn.addEventListener("click", () => {
  const rndCol = `rgb(${random(255)} ${random(255)} ${random(255)})`;
  document.body.style.backgroundColor = rndCol;
});

```

根据事件类型的不同，用户操作可以触发不同事件，页面进行对应操作



2.解绑事件操作

````js
btn.removeEventListener("click", changeBackground);
````





#### 3.事件对象

在事件处理函数的内部，会有event，evt，e等名称指定参数，这些参数称之为事件对象，它会自动传递给事件处理程序以提供额外的功能和信息

```js
const btn = document.querySelector("button");

function random(number) {
  return Math.floor(Math.random() * (number + 1));
}

function bgChange(e) {
  const rndCol = `rgb(${random(255)} ${random(255)} ${random(255)})`;
  e.target.style.backgroundColor = rndCol;
  console.log(e);
}

btn.addEventListener("click", bgChange);

```

例如这个bgChange函数里面包含了事件对象e，设置e.target上的背景颜色

还可以通过事件对象的其他属性去查找事件对象的一些值，比如说查找按了什么键



#### 4.阻止默认行为

比如说在一个提交表单中设置条件检测错误，如果出现错误就在函数对象上调用preventDefault()函数，这样函数就会停止操作，在表单下的段落中显示一条错误信息，告诉用户出现了什么错误

```js
const form = document.querySelector("form");
const fname = document.getElementById("fname");
const lname = document.getElementById("lname");
const para = document.querySelector("p");

form.addEventListener("submit", (e) => {
  if (fname.value === "" || lname.value === "") {
    e.preventDefault();
    para.textContent = "You need to fill in both names!";
  }
});

```



#### 5.事件冒泡

向父元素添加点击事件，我们去点击子元素

事件同样会发生，因为子元素在父元素内部，相当于隐式点击了其父级元素

如果是多层嵌套的，事件会不断向上触发，形成事件冒泡

就是在父元素上绑定事件，点击子元素，每一个子元素都会触发一次父元素绑定的事件，依次向上



调用stopPropagation() 函数防止事件冒泡

```js
const btn = document.querySelector("button");
const box = document.querySelector("div");
const video = document.querySelector("video");

btn.addEventListener("click", () => box.classList.remove("hidden"));

video.addEventListener("click", (event) => {
  event.stopPropagation();
  video.play();
});

box.addEventListener("click", () => box.classList.add("hidden"));

```





#### 6.事件捕捉

和冒泡顺序相反，默认情况下是禁用的，要在addEventListener中传递capture选项

```js
const output = document.querySelector("#output");
function handleClick(e) {
  output.textContent += `You clicked on a ${e.currentTarget.tagName} element\n`;
}

const container = document.querySelector("#container");
const button = document.querySelector("button");

document.body.addEventListener("click", handleClick, { capture: true });
container.addEventListener("click", handleClick, { capture: true });
button.addEventListener("click", handleClick);

```

从父到子执行





#### 7.事件委托

我们可以在多元素的情况下为每一个元素设置事件处理函数，但是我们可以更简单地在父级元素上面设置

依靠冒泡来确保用户触发事件时，执行程序

可以在父级绑定多个函数，想要点击执行的事件都在父元素上，然后调用即可

```js
function random(number) {
  return Math.floor(Math.random() * number);
}

function bgChange() {
  const rndCol = `rgb(${random(255)} ${random(255)} ${random(255)})`;
  return rndCol;
}

const container = document.querySelector("#container");

container.addEventListener("click", (event) => {
  event.target.style.backgroundColor = bgChange();
});

```





## 4.内置构造函数

### 1.Object

1.assign 合并一个多个对象到目标对象

target是目标对象，所有对象的属性将复制到该对象

sources将被复制到目标对象，原本存在的话就直接覆盖

```js
Object.assign(target, ...sources)

const target = { a: 1, b: 2 };
const source1 = { b: 4, c: 5 };
const source2 = { c: 6, d: 7 };

const result = Object.assign(target, source1, source2);
console.log(result); // { a: 1, b: 4, c: 6, d: 7 }
console.log(target); // { a: 1, b: 4, c: 6, d: 7 }

```

2.keys 获取对象中所有key集合，返回一个数组 键名

3.values 获取对象中所有值的集合，返回一个数组 键值

4.entries 键值对

```js
const obj = { a: 1, b: 2, c: 3 };

console.log(Object.keys(obj)); // ['a', 'b', 'c']
console.log(Object.values(obj)); // [1, 2, 3]
console.log(Object.entries(obj)); // [['a', 1], ['b', 2], ['c', 3]]

```



### 2.Array

方法里面不一定用箭头函数，写立即执行函数更好

1.Array.from( ) 将伪数组转成数组

```js
let arrayLike = document.querySelectorAll('.example'); // 类数组对象
let array = Array.from(arrayLike); // 转换为真正的数组
```



2.filter 

筛选，返回通过筛选的元素数组

```js
let numbers = [1, 2, 3, 4, 5];
let evenNumbers = numbers.filter(num => num % 2 === 0);
console.log(evenNumbers); // [2, 4]
```



3.map

创建一个新数组，结果是传入数组的每个元素调用回调函数后返回的值

```js
let numbers = [1, 2, 3];
let doubled = numbers.map(num => num * 2);
console.log(doubled); // [2, 4, 6]
```



4.reduce

```js
let numbers = [1, 2, 3, 4, 5];
let sum = numbers.reduce((acc, current) => acc + current, 0);
console.log(sum); // 15

```



5.find

返回数组中满足条件的第一个元素，否则返回undefined

```js
let array = [5, 12, 8, 130, 44];
let found = array.find(element => element > 10);
console.log(found); // 12
```



6.every

检测是否所有元素都满足条件，满足true，否则false

```js
let array = [1, 30, 39, 29, 10, 13];
let allOver18 = array.every(age => age > 18);
console.log(allOver18); // false

```



### 3.String

**1.split(separator, limit)**:

- 将字符串按照指定的分隔符 `separator` 分割成子字符串，并返回一个包含分割后的子字符串的数组。
- `limit` 参数可选，指定返回的子字符串数量上限。

```js
let str = "Hello,World";
let arr = str.split(","); // ["Hello", "World"]
```



**2.startsWith(searchString, position)**:

- 判断当前字符串是否以指定的字符串 `searchString` 开头。
- 可以通过 `position` 参数指定搜索起始位置，默认为 `0`。

```js
let str = "Hello, world";
console.log(str.startsWith("Hello")); // true
console.log(str.startsWith("world", 7)); // true，从索引 7 开始检查是否以 "world" 开头

```



**3.includes(searchString, position)**:

- 判断当前字符串是否包含指定的字符串 `searchString`。
- 可以通过 `position` 参数指定搜索起始位置，默认为 `0`。

```js
let str = "Hello, world";
console.log(str.includes("world")); // true
console.log(str.includes("Hello", 1)); // false，从索引 1 开始搜索是否包含 "Hello"

```



**4.substring(startIndex, endIndex)**:

- 返回一个从 `startIndex` 到 `endIndex`（不包括 `endIndex`）之间的子字符串。
- 如果省略 `endIndex`，则直到字符串末尾。

```js
let str = "Hello, world";
console.log(str.includes("world")); // true
console.log(str.includes("Hello", 1)); // false，从索引 1 开始搜索是否包含 "Hello"

```



**5.大小写转换**:

- **toUpperCase()**: 将字符串中的所有字符转换为大写，并返回新字符串。
- **toLowerCase()**: 将字符串中的所有字符转换为小写，并返回新字符串。

```js
let str = "Hello, world";
console.log(str.toUpperCase()); // "HELLO, WORLD"
console.log(str.toLowerCase()); // "hello, world"

```



**6.indexOf(searchValue, fromIndex)**:

- 返回字符串中第一次出现 `searchValue` 的位置索引，如果没有找到则返回 `-1`。
- 可以通过 `fromIndex` 参数指定开始搜索的位置，默认为 `0`。

```js
let str = "Hello, world";
console.log(str.indexOf("o")); // 4，第一次出现 "o" 的位置
console.log(str.indexOf("o", 5)); // 8，从索引 5 开始搜索 "o" 的位置

```



### 4.Number

toFixed()设置小数点后位数

```js
let num = 10.23456;

console.log(num.toFixed(2)); // "10.23"
console.log(num.toFixed(4)); // "10.2346"
console.log(num.toFixed(0)); // "10"

```



### 5.Date

```js
let today = new Date();

console.log(today.getFullYear()); // 当前年份，比如 2024
console.log(today.getMonth()); // 当前月份，范围 0-11
console.log(today.getDay()); // 当前星期几，范围 0-6

```








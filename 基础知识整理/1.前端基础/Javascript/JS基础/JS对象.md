# 对象

##1 对象的创建

1.var obj = {

​	属性 ：属性值,

​	函数名： function( ) {

}

}  

​	直接写出来，有对象字面量/对象直接量



2.构造函数

​	2.1 系统自带的 new object(); //Array Number

```js
var obj = new Object();
obj.name = 'abc';
```

​	2.2自定义 命名记得大驼峰式，首字母大写

```js
function Person(){
	this.name = "hahaha";	
}
//里面增加this.name = 'BMW';等
//可以在创建的时候默认赋值

var person1 = new Person();


```



## 2 原型/继承

### 1.原型

对象原型是JS对象相互继承功能的一种机制，JS的每个对象都有一个内置属性，称为原型

例如一个对象名为Person

对象里面有prototype属性可以将Person对象构造私有属性变成一个原型

```js
Person.prototype {
		name : "haha";
    	say: "hehe";
}
var person = new Person();
可以将Person的属性全部继承到person中

```

如果我在person里面查询属性，会先在自身上找，如果没有就会到继承的Person中找

```js
 Object.getPrototypeOf()//用这个函数可以找到对象的原型是谁
```



在person对象中对prototype中的属性赋值仅仅是改变person对象的值，并且是增加该属性到person本身，无法修改私有属性的值

```js
//Person.prototype --原型
//Person.prototype = {}  --祖先
Person.prototype.LastName = "liang";
Person.prototype.say = function() {
	console.log("man");
}

function Person(name,sex,age) {
			this.name = "";
    		this.sex = "";
    		this.age = "";

} //每次创建的时候都会执行一次

//如果是参数一样的东西，可以把它们集成到原型，创建新对象的时候只需要传入部分属性，公用部分只需要执行一次

```



原型的增删改查要在prototype里面修改，constructor属性可以找到创建的对象在哪个对象类构造来的



### 2.原型链

对象的原型有自己的原型

可以构造一条通过prototype连接的链下一级的prototype = 上一级创建出来的对象

这样属性可以一直继承叠加下去

大多数对象的最终都会继承自Object.prototype，Object.prototype的原型是 `null`，所以它位于原型链的末端

```js
		使用create来创建对象
			var obj = {};
			var person = Object.create(obj);
		此时person的原型为obj
```





## 3.面向对象编程

### 1.基础概念和思想

面向对象编程是编程范例，主要是类和实例，封装，继承，多态。

面向对象编程是将系统建模为对象的集合，其中每个对象代表系统的某些特定方面。对象为想要使用它的其他代码提供公共接口，但维护其自己的私有内部状态，系统其它部分不用关注对象内部发生了什么

在构建系统的时候，定义特定功能的类，里面有属性，方法



### 2.继承

比如构造一些类要用到公共的属性或者方法，可以先构造号公共类，在构造新类时直接添加

```js
class Animal {
  constructor(name) {
    this.name = name;
  }
  
  speak() {
    console.log(this.name + ' makes a noise.');
  }
}

class Dog extends Animal {
  constructor(name, breed) {
    super(name); // 调用父类的构造函数，并传入 name 参数
    this.breed = breed; // 初始化子类独有的属性
  }
  
  speak() {
    console.log(this.name + ' barks.');
  }
  
  displayInfo() {
    console.log(this.name + ' is a ' + this.breed);
  }
}

let dog = new Dog('Buddy', 'Golden Retriever');
dog.speak(); // 输出: Buddy barks.
dog.displayInfo(); // 输出: Buddy is a Golden Retriever.

```

super 是调用父类的方法

### 3.封装

一种数据和数据操作绑定的概念，限制直接访问对象内部，开放公共接口

对象为想要使用它们但维护自己的内部状态的其他代码提供了一个接口。对象的内部状态保持私有，这意味着它只能通过对象自己的方法访问，而不能从其他对象访问。保持对象的内部状态私有，并且通常在其公共接口和私有内部状态之间进行明确划分，称为封装。它在该对象和系统的其余部分之间创建了一种防火墙。

```js
// 使用闭包实现封装
function createCounter() {
    let count = 0;  // 私有变量

    return {
        getCount: function() {   // 公共方法
            return count;
        },
        increment: function() {  // 公共方法
            count++;
        },
        reset: function() {      // 公共方法
            count = 0;
        }
    };
}

// 创建一个计数器实例
const counter = createCounter();

// 使用公共方法操作私有变量
console.log(counter.getCount());  // 输出: 0
counter.increment();
console.log(counter.getCount());  // 输出: 1
counter.increment();
console.log(counter.getCount());  // 输出: 2
counter.reset();
console.log(counter.getCount());  // 输出: 0
```

createCounter 函数返回一个对象，对象包含三个方法

count是函数内部声明的变量，外部无法访问

通过 return 让方法变成对象可以在外部访问的公共方法

这种方式利用了 JavaScript 中函数作用域和闭包的特性来实现封装，确保了 `count` 变量的安全性和访问控制，同时提供了一组公共接口供外部使用





# JS的Window对象

## Window对象



### 1.全局作用域

1.window对象是全局对象，表示浏览器中的窗口或标签页

2.所有全局变量和函数实际上都是 window对象的属性和方法



### 2.窗口和框架控制

它提供了访问和控制浏览器窗口和本身以及内容的方法和属性

#### 1.大小和位置调整

```js
1.调整窗口内部的宽高
window.innerWidth
window.innerHeight

2.调整窗口外部的宽高，包括边框和工具栏等
window.outerWidth 
window.outerHeight

3.分别用于设置窗口的大小和按照当前大小调整窗口
window.resizeTo(width, height)
window.resizeBy(widthDelta, heightDelta)
```



#### 2.窗口位置

```
1.窗口在屏幕上的位置
window.screenX
window.screenY

2.移动窗口到指定位置或按照当前位置进行移动
window.moveTo(x, y) 
window.moveBy(xDelta, yDelta)
```



#### 3.打开关闭窗口

```
1.打开一个新的浏览器窗口或标签页
window.open(url, target, features)

2.关闭当前窗口或标签页
window.close()
```



### 3.浏览器信息和导航

#### 1.当前页面url

```
window.location.href ==>获得当前页面的url

window.location.reload() ==>重新加载当前页面

window.location.replace(url) ==>用新的url替换当前页面，不会留下历史记录

```

#### 2.浏览器历史记录

```
window.history ==>表示当前窗口的浏览历史记录

window.history.back()  表示在历史记录中后退
window.history.forward() 表示在历史记录中前进
```



### 4.定时器和事件处理

#### 1.定时器

```
1.延迟多少秒执行函数
window.setTimeout(func, delay)


2.每隔多少秒执行一次函数
window.setInterval(func, interval)

```



#### 2.事件处理

```
添加和移除事件监听器
window.addEventListener(event, func)
window.removeEventListener(event, func)

```



### 5.window对象的一点操作

1.window.document 是当前窗口的文档对象，用来操作dom

2.window.navigator 包含浏览器相关信息的对象，用来查看信息

3.window.console控制台对象，用于在控制台输出信息。





## Window 下的一些对象

#### 1 Window Console 对象

和上面的一样，访问可以用`window.console` 或仅用 `console`

里面常用的方法

```
清空控制台 console.clear()
将信息在控制台打印 console.log()
记录对count()的特定调用次数 console.count()
```

方法太多，用到再去查也可以的



#### 2 Window History 对象

```js
let length = history.length 获取历史列表中的url数量
```

其他的和上面介绍差不多



#### 3 Window Location 对象 / Window Navigator 对象

主要是用来查询url信息，方法再查



#### 4 Window Screen 对象

与屏幕有关的信息



## DOM对象

### 1.DOM 树结构

1.DOM对象是指浏览器将网页文档解析成由一个节点组成的树形结构模型

2.每一个节点都是一个对象

3.常见的节点类型包括

​           3.1.元素节点(html标签)

​           3.2.文本节点（文本内容）

​           3.3.属性节点（元素属性，id，class等）



### 2.DOM对象

1.document对象 表示整个文档，是DOM树的根节点，通过它可以访问和操作文档的所有内容

2.元素对象 表示HTML元素节点，可以通过标签名，类名，id等方式获取元素，进行操作



### 3.DOM操作

#### 1.查询和选择

1.document.getElementById()

快速获取具有唯一 ID 的元素，效率高。返回的是单个元素而非 NodeList，直接操作更方便

只能根据元素的 ID 获取，对于其他选择器无效。返回的是单个元素，如果要选择多个元素需要另外的方法



2.document.querySelector()

支持复杂的 CSS 选择器，选择灵活。返回第一个匹配元素



3.document.querySelectorAll()

返回所有匹配的元素

返回的是静态的 NodeList，对文档变化不敏感



```js
const elementById = document.getElementById('myId'); // 根据 id 查询元素

const elementsByClass = document.getElementsByClassName('myClass'); // 根据类名查询多个元素

const elementsByTag = document.getElementsByTagName('div'); // 根据标签名查询多个元素

const elementByQuery = document.querySelector('.myClass'); // 使用 CSS 选择器查询单个元素

const elementsByQueryAll = document.querySelectorAll('div'); // 使用 CSS 选择器查询多个元素

```



#### 2.修改更新

直接设置修改，内容，样式，结构

```js
const myElement = document.getElementById('myElement');

// 修改文本内容
myElement.textContent = 'New Text';

// 修改样式
myElement.style.color = 'red';

// 修改属性
myElement.setAttribute('title', 'Updated Title');

```

```js
const elementToRemove = document.getElementById('toBeRemoved');
elementToRemove.parentNode.removeChild(elementToRemove);
//删除
```





#### 3.事件监听

用addEventListener绑定事件

```js
const button = document.getElementById('myButton');

button.addEventListener('click', function() {
    alert('Button clicked!');
});

```



#### 4.创建元素

```js
// 创建一个新的 div 元素
const newDiv = document.createElement('div');

// 设置元素的属性
newDiv.className = 'my-class';
newDiv.id = 'new-div';
newDiv.setAttribute('title', 'New Div');

// 添加文本内容
newDiv.textContent = 'Hello, World!';

// 将新元素插入到文档中的某个位置
document.body.appendChild(newDiv); // 添加到 body 元素的末尾

```
































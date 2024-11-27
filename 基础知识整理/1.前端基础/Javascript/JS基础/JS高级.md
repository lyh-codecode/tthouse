# JS高级

### 1.闭包

内部函数被保存到外部，一定会形成闭包。它允许函数访问其词法作用域之外的变量

这个词法环境包含了函数定义时可访问的所有局部变量，以及它定义时所处的外部函数的局部变量。当函数在其词法作用域之外被调用时，它仍然保持对其作用域的引用，因此可以访问这些变量

#### 1.应用

##### 1.实现公有变量

比如说函数累加器

```js
function add() {
	var count = 0;
	function demo() {
	count++;
	console.log(count);
}
	return demo;
}
var counter = add();
counter();//调用一次count +1
```



##### 2.做缓存

外部不可见，但是实际是存在的

```js
function test(){
	var num = 100;
	function a() {
		num++;
		console.log(num);
}
	function b() {
		num--;
		console.log(num);
}
		return [a,b];
}

var arr = test();
arr[0]();//101
arr[1]();//100
```

```js
function eater(){
	var food = "";
	var obj = {
		eat : function (){
		console.log("我吃" + food);
			food = "";
	},
		push : function (myFood) {
            	food = myFood;
		}
		}
		return obj;
}

var eater1 = eater();
eater1.push('banana');
eater1.eat();
```



如果想要套现，要在里面写立即执行函数

比如说一个循环 i = 10 结束，但是里面的函数全部都没有执行，最后如果访问和 i 有关的时候 i 全部为 10

无法实现 0 1 2 3 ... 9 的效果，用立即执行函数就可以当场把0 1 2 等数字返回



##### 3.实现封装，属性私有化/模块化开发，防止污染全局变量

```js
function createCounter() {
  // 私有变量
  let count = 0;

  // 私有函数
  function increment() {
    count++;
    console.log('Count incremented:', count);
  }

  function decrement() {
    count--;
    console.log('Count decremented:', count);
  }

  // 公共接口（返回一个对象，包含可以访问的方法）
  return {
    increment: increment,
    decrement: decrement,
    getCount: function() {
      return count;
    }
  };
}

const counter1 = createCounter();
const counter2 = createCounter();

counter1.increment(); // 输出: Count incremented: 1
counter1.increment(); // 输出: Count incremented: 2
console.log(counter1.getCount()); // 输出: 2

counter2.increment(); // 输出: Count incremented: 1
console.log(counter2.getCount()); // 输出: 1

counter1.decrement(); // 输出: Count decremented: 1
console.log(counter1.getCount()); // 输出: 1

```



#### 2.危害

闭包会导致原有作用域链不释放，导致内存泄漏

```js
function a() {
	var num = 100;
	function b() {
		num++;
		console.log(num);
}
		return b;//b被返回，a才执行结束，b先保存a的AO对象，a再销毁
}
var demo = a(); //在a函数调用结束，a释放里面的所有变量，但是b连接了a创建的AO对象，销毁了b还是可以访问
demo(); //打印101
demo(); //打印102
```





### 2.this

非严格模式下，this始终是对对象的引用。严格模式下，this可以是任何值。

this的指向取决于它如何调用，用this替代被调用的方法对象



#### 绑定规则

##### 1.全局上下文中的this

当作用域是全局时，指向window

##### 2.函数中的this

指向调用该方法的对象

##### 3.构造函数中的this

用new关键字调用构造函数时，this指向新创建的实例对象

##### 4.DOM事件处理函数中的this

指向触发事件的DOM元素

```js
// 全局上下文中的 this
console.log(this); // 在浏览器中指向 window 对象

function myFunction() {
  console.log(this);
}

myFunction(); // 在非严格模式下，指向 window 对象；严格模式下，指向 undefined

// 对象方法中的 this
const obj = {
  name: 'John',
  greet: function() {
    console.log(`Hello, ${this.name}!`);
  }
};

obj.greet(); // 输出 "Hello, John!"

// 构造函数中的 this
function Person(name) {
  this.name = name;
  this.greet = function() {
    console.log(`Hello, my name is ${this.name}`);
  };
}

const person1 = new Person('Alice');
person1.greet(); // 输出 "Hello, my name is Alice"

// 箭头函数中的 this
const obj2 = {
  name: 'Emma',
  greet: function() {
    setTimeout(() => {
      console.log(`Hello, ${this.name}!`);
    }, 1000);
  }
};

obj2.greet(); // 输出 "Hello, Emma!"，箭头函数继承了 obj2.greet 的 this

```



##### 5.改变this指向的方法

1.call 

主要用于改变this指向，同时调用函数

```js
obj = {
	name : "nihao"
	}
function fn(x,y){
	console.log(x + y)	
}

fn.call(obj,1,2)
第一个参数是this
```



2.apply

和call差不多，但是传入的第二个参数必须是数组

可以用来求数组最大值,最小值

```js
const arr = [11,22,55]
const max = Math.max.apply(Math,arr)
//for循环，展开运算符也可以
```



3.bind（重要）

不调用函数，但是能改变函数内部的this指向

```js
function fn() {
	console.log(this)	
}
fn.bind(obj)
//返回值为改过this的新函数，拷贝一份相当于
```

应用：有一个按钮，点击禁用，2s后开启

```js
const btn = document.querySelector('button')
btn.addEventListener('click',function() {
	this.disabled = true
	window.setTimeout(function(){
	this.disabled = false
}.bind(this),2000)
})
```

因为bind(this)的this是在匿名函数外面的，所以和点击那个this是一样的



### 3.类数组

1.利用属性名模拟数组特性，实际上还是个对象 ==>一定要有length

2.可以动态增长length属性

3.要加push方法，splice方法

```js
var obj = {
    "0" : "a",
    "1" : "b",
    name : "asd",
    age : 111,
    length : 3,
    push : Array.prototype.push, //length 是多少就在哪个位置上赋值，比如说length =3，在"2"上覆盖
    splice : Array.prototype.splice,  
}
```





### 4.异常处理

#### 1.throw抛异常

1.throw抛出异常信息，程序终止

2.throw后面跟的是错误提示信息

3.Error对象配合throw使用，设置更详细的报错提醒

```js
if(出现异常) {
	throw new Error('没有参数传入')
}
```



#### 2.try catch 捕获异常

```js
try{
 	//可能出错的代码，出错前的正常执行，出错后直接跳到catch
} catch(error) {
	console.log(error.message)
	//需要中断程序加return
} finally {
	不管对错都执行
}
```





#### 3.debugger

写出来一直摁下一步调试
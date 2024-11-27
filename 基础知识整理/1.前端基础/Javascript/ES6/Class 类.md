# Class类

## 主体

#### 1. 类的声明和定义

```js
//声明
class Example {
    constructor(a) {
        this.a = a;
    }
}

// 匿名类
let Example = class {
    constructor(a) {
        this.a = a;
    }
}
// 命名类
let Example = class Example {
    constructor(a) {
        this.a = a;
    }
}
```

使用 `class` 关键字声明一个类，类名通常以大写字母开头

```js
class Rectangle {
  constructor(width, height) {
    this.width = width;
    this.height = height;
  }//默认返回实例对象this，也可以指定返回对象
    
    
	//在类中定义方法不需要function关键字，直接函数名即可
  // 普通方法
  calculateArea() {
    return this.width * this.height;
  }

  // 静态方法
  static isEqual(a, b) {
    return a.width === b.width && a.height === b.height;
  }

  // Getter
  get area() {
    return this.calculateArea();
  }
}
```

在类中使用 `constructor` 方法来定义构造函数，它在实例化对象时被调用。`this` 关键字在构造函数内部指向创建的新实例。

在实例化的时候传入constructor的参数，用new构建一个实例化即可

```js
class Example {}
 
let exam1 = new Example(); 
```



方法是定义在 prototype 上的

```js
Example.prototype = {
	//方法
}

Object.assign(Example.prototype,{
	//方法	
})
```

#### 2. 构造函数（constructor）

构造函数在创建类的新实例时自动调用，用于初始化对象的状态

````js
let rect = new Rectangle(5, 10);
console.log(rect.calculateArea()); // 输出: 50

````

#### 3. 类方法

类中可以定义各种方法，这些方法会被添加到类的原型上，使得所有实例对象可以共享使用这些方法

这样就不用在创建新实例的时候再写一次

```js
class Animal {
  constructor(name) {
    this.name = name;
  }

  // 类方法
  speak() {
    console.log(`${this.name} makes a noise.`);
  }
}

let dog = new Animal('Dog');
dog.speak(); // 输出: Dog makes a noise.

```

#### 4.静态方法/属性

使用 `static` 关键字可以定义静态方法和静态属性，它们属于类本身而不是类的实例

即直接定义在类内部的属性（ Class.propname ），不需要实例化

实例化之后直接点方法名调用，

```js
class Animal {
  static getType() {
    return 'Animal';
  	}
}

console.log(Animal.getType()); // 输出: Animal
```

#### 5.修饰器

decorator 是一个函数，用来修改类的行为，在代码编译时产生作用



**类修饰器** 接收一个参数，即类的构造函数

方法修饰器接收三个参数：

target(类的原型对象) ，name（修饰的属性名），descriptor（改属性的描述对象）

- 对于普通类，第一个参数是类的构造函数本身。
- 对于静态类，第一个参数是类的构造函数本身。

```
//类修饰

//方法修饰
```

我们可以在一个类的基础上，在内部引入修饰器，增加函数功能

```js
function classDecorator(constructor) {
  // 执行一些操作，例如修改构造函数的原型
}

@classDecorator
class MyClass {
  // 类的定义
}

```

```js
// 定义一个方法修饰器
function methodDecorator(target, propertyKey, descriptor) {
  let originalMethod = descriptor.value;

  descriptor.value = function(...args) {
    console.log(`Calling ${propertyKey} with`, args);
    let result = originalMethod.apply(this, args);
    console.log(`Method ${propertyKey} returned`, result);
    return result;
  };
  return descriptor;
}



// 使用方法修饰器
class Calculator {
  @methodDecorator //我直接内部@你 ==>将修饰器加入add方法中
  add(a, b) {
    return a + b;
  }
}

// 创建 Calculator 的实例
let calc = new Calculator();

// 调用被修饰的方法
let sum = calc.add(10, 20);
console.log("Sum:", sum);

//Calling add with [10, 20]
//Method add returned 30
//Sum: 30

```



#### 6. 类表达式

类可以作为表达式使用，可以作为函数的返回值或者赋值给变量

类表达式可以用于需要动态创建类的情况

```js
let Animal = class {
  constructor(name) {
    this.name = name;
  }

  speak() {
    console.log(`${this.name} makes a noise.`);
  }
};

let dog = new Animal('Dog');
dog.speak(); // 输出: Dog makes a noise.
```



## 封装和继承

#### 1. 继承

使用 `extends` 关键字可以创建一个子类，子类可以继承父类的所有属性和方法

```
class Child extends Father { ... }
```

```js
class Dog extends Animal {
  constructor(name, breed) {
    super(name); // 调用父类的 constructor 方法
    this.breed = breed;
  }

  // 子类可以覆盖父类的方法
  speak() {
    console.log(`${this.name} barks.`);
  }
}

let labrador = new Dog('Buddy', 'Labrador');
labrador.speak(); // 输出: Buddy barks.

```

在子类的构造函数中，使用 `super` 关键字调用父类的构造函数，以便在子类实例化时初始化父类的属性



#### 2. Getter 和 Setter

使用 `get` 和 `set` 关键字可以定义访问器属性，它们允许更加控制地访问类的属性

```js
class Rectangle {
  constructor(width, height) {
    this._width = width;
    this._height = height;
  }

  get area() {
    return this._width * this._height;
  }

  set width(value) {
    if (value > 0) {
      this._width = value;
    }
  }
}

let rect = new Rectangle(5, 10);
console.log(rect.area); // 输出: 50

rect.width = 20;
console.log(rect.area); // 输出: 200
```










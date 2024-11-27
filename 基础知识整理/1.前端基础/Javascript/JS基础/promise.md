## promise

### 1.主要作用

* 利用.then使得代码成链式调用
* .then中的回调函数属于异步任务中的微任务



### 2.Promise状态

* 初始状态 pending

  * 在resolve或者reject之前都处于pending等待状态

  * 可以改变

    ​

* 成功状态 fulfilled

  * 执行了resolve之后，变成fulfilled状态
  * 后续进入.then的回调函数中
  * 回调函数的第一个参数可以获取到值

  ​

* 失败状态 rejected

  * 执行reject之后，变成rejected状态
  * rejected函数传递的参数，可以在.then的第二个参数函数中获得，或者是.catch获取



### 3.Promise的九个方法

#### 1.resolve

* Promise对象的静态方法，用于创建一个成功状态的Promise对象，可以在.then的成功回调中获取resolve的值

```js
const p = Promise.resolve("成功");

p.then((res) => {
    console.log(res);//执行，打印成功
});

const p1 = new Promise((resolve, reject) => {
	resolve("成功");
});
p1.then((res) => {
  console.log(res);
})
```



#### 2.reject

和resolve一样，只是状态不一样

```js
const p = Promise.reject("失败");

p.then(
    (res) => {
        //不执行
    },
    (rej) => {
        console.log(rej);//打印失败
    }
);


//等效
p.catch((rej) => {
    console.log(rej);//打印失败
})
```




































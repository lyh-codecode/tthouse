# async和await

### async

async是异步操作相关的关键字与Promise和Generator有很大关联

语法

```js
async function name() {
	函数体
}
```



### 返回值

async函数返回一个Promise对象，可以使用then方法添加回调函数

async函数中可能会有await表达式，执行时遇到await就会先暂停执行，等到触发的异步操作完成后，再回头执行解析返回值

await关键字仅在 async function中有效，在外面用报错





### await

await操作符用于等待一个 Promise 对象, 它只能在异步函数 async function 内部使用

```
[return_value] = await expression;
expression: 一个 Promise 对象或者任何要等待的值
```

返回 Promise 对象的处理结果。如果等待的不是 Promise 对象，则返回该值本身

如果一个 Promise 被传递给一个 await 操作符，await 将等待 Promise 正常处理完成并返回其处理结果



正常情况下，await 命令后面是一个 Promise 对象，它也可以跟其他值，如字符串，布尔值，数值以及普通函数



await针对所跟不同表达式的处理方式：

- Promise 对象：await 会暂停执行，等待 Promise 对象 resolve，然后恢复 async 函数的执行并返回解析值
- 非 Promise 对象：直接返回对应的值







**总结步骤：**

await在async函数内部等待一个Promise对象，然后暂停async函数的执行

等待Promise对象进行resolve或者reject操作

resolove则await表达式的值就是解决后的值，rejected则抛出错误



```js
async function example() {
  let promise = new Promise((resolve, reject) => {
    setTimeout(() => resolve("done!"), 1000);
  });

  let result = await promise; // 等待 promise 解决
  console.log(result); // "done!"
    //操作
}

example();

```

await相对于传统回调函数或者用.then()的链式调用，代码更加简洁
















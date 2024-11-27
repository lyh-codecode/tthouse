# JavaScript Promise 对象

### 1.Promise 对象

1.代表了未来将要发生的事件，用来传递异步操作的消息

2.可以封装异步操作，避免了层层嵌套的回调函数

3.有统一的接口，更易控制异步操作

4.执行无法取消Promise

5.不设置回调函数Promise内部会抛出错误



### 2.Promise的创建

​	1.通过new来调用Promise的构造器来进行实例化

​	2.Promise 构造函数包含一个参数和一个带有 resolve（解析） 和 reject（拒绝） 两个参数的回调函数，

​	一切正常调用resolve，否则调用拒绝

```js
var promise = new Promise(function(resolve, reject) {
    
    // 异步处理
    // 处理结束后、调用resolve 或 reject
    
});
```



### 3.Promise 实现 Ajax

**1.创建Promise对象**

在ajax函数中创建Promise对象实例，将一个函数作为参数传入，这个函数会在Promise被创建时立即执行

```js
function ajax(url, method, data) {
  return new Promise((resolve, reject) => {
    // 在 Promise 构造函数中执行异步操作
  });
}
请求地址，请求方法，请求数据（看方法要不要选）
```



**2.XMLHttpRequest设置**

在Promise函数内部，创建一个 `XMLHttpRequest` 对象 (`xhr`)，并使用 `xhr.open()` 方法设置请求的方法 (`GET`, `POST` 等) 和 URL

```js
const xhr = new XMLHttpRequest();
xhr.open(method, url);//设置请求方法和请求地址
xhr.setRequestHeader('Content-Type', 'application/json'); // 设置请求头
```



**3.看返回参数调用resolve还是reject,响应处理**

```js
xhr.onload = function() {
  if (xhr.status >= 200 && xhr.status < 300) {
    let responseData = xhr.responseText;
    try {
      responseData = JSON.parse(responseData); // 尝试解析为 JSON
      resolve(responseData); // 解析成功，返回响应数据
    } catch (e) {
      reject('Invalid JSON response'); // JSON 解析失败
    }
  } else {
    reject('Request failed with status ' + xhr.status); // 请求失败
  }
};



//xhr.onload 成功触发
```



**4.错误处理，使用onerror**

使用 `xhr.onerror` 事件处理程序，处理请求过程中的错误。如果出现任何错误，调用 `reject(new Error('Ajax request failed'))`，将错误传递给Promise的 `catch` 方法的回调函数

```js
xhr.onerror = function() {
  reject('Request failed'); // 请求错误
};
```



**5.发送请求send**

最后调用 `xhr.send(data)` 发送请求

data要转成json，用JSON.stringify(data)



**6.调用ajax**

调用的时候可以通过.then()方法处理请求成功的情况，通过.catch()方法处理请求失败或网络错误的情况

```js
ajax(url).then(function success(value){
	document.write(value);
}).catch(function failure(error){
	document.write(error);
});
```



```js
function ajax(url, method, data) {
  return new Promise((resolve, reject) => {
    const xhr = new XMLHttpRequest();
    xhr.open(method, url);
    xhr.setRequestHeader('Content-Type', 'application/json'); // 设置请求头

    xhr.onload = function() {
      if (xhr.status >= 200 && xhr.status < 300) {
        let responseData = xhr.responseText;
        try {
          responseData = JSON.parse(responseData); // 尝试解析为 JSON
        } catch (e) {
          reject('Invalid JSON response');
        }
        resolve(responseData); // 请求成功，返回响应数据
      } else {
        reject('Request failed with status ' + xhr.status); // 请求失败，返回错误信息
      }
    };

    xhr.onerror = function() {
      reject('Request failed'); // 请求错误
    };

    xhr.send(JSON.stringify(data)); // 发送请求并传递数据
  });
}

// 示例用法：
ajax('https://api.example.com/data', 'POST', { key: 'value' })
  .then(response => {
    console.log('Ajax request successful:', response);
    // 处理获取到的数据
  })
  .catch(error => {
    console.error('Ajax request failed:', error);
    // 处理错误情况
  });

```





## #补充一下then和catch

在Promise中，`then` 和 `catch` 是用来处理Promise对象状态变化的方法。它们之间的区别主要在于它们处理的情况和返回值



**1.then方法**：

- `then` 方法用于注册当Promise状态变为 `fulfilled`（已成功）时的回调函数
- `then` 方法可以接收两个参数：第一个是处理成功情况的回调函数，第二个是处理失败情况的回调函数（可选）
- 如果只提供一个参数，则该参数会被当作处理成功情况的回调函数。处理失败情况的回调会被跳过，错误会被传递到链中的下一个 `catch` 方法



**2.catch方法**：

- `catch` 方法是 `then(null, rejection)` 或 `then(undefined, rejection)` 的别名，用于注册当Promise状态变为 `rejected`（已失败）时的回调函数
- `catch` 方法只接收一个参数，即处理失败情况的回调函数。它是为了方便地捕获Promise链中的错误而设计的




### Promise的方法

​	**Promise.resolve 方法，Promise.reject 方法**

1.Promise.resolve 将现有对象转为Promise对象，返回一个以给定值解析后的Promise对象

​	成功状态



2.Promise.reject(reason)时，返回的 Promise 对象会以拒绝的状态（rejected）被创建，并且拒绝原因（reason）将作为该 Promise 对象的拒绝理由

​	失败状态
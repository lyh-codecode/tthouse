# XHR和Fetch



### 1.XMLHttpRequest (XHR)

用于在浏览器中发起网络请求

- 在不重新加载页面的情况下更新网页
- 在页面已加载后从服务器请求数据
- 在页面已加载后从服务器接收数据
- 在后台向服务器发送数据

`XMLHttpRequest` 可以用于获取任何类型的数据，而不仅仅是 XML





#### 使用xhr发起请求的步骤

1.创建一个xhr对象

```js
let xhr = new  XMLHttpRequest();
```



2.配置请求，设置请求类型，url，是否异步等

```js
xhr.open('GET', 'https://api.example.com/data', true);
```



3.设置请求头

```
xhr.setRequestHeader('Content-Type', 'application/json');
```



4.响应处理

绑定成功失败事件



5.请求异步处理

`open` 方法中的 `async` 参数设置为 `true`，则请求是异步的,可以设置异步处理

如果设置为 `false`，则是同步请求，JavaScript 会在请求完成前等待



6.发送请求

```js
xhr.send();
```

对于 GET 请求，可以不传递参数；对于 POST 请求，参数通常通过 `send` 方法发送





```js
let xhr = new XMLHttpRequest(); //创建实例对象
xhr.open('GET', 'https://api.example.com/data', true);//设置请求行

xhr.onload = function() {
  if (xhr.status >= 200 && xhr.status < 300) {
    console.log('Success!', xhr.responseText);
  } else {
    console.error('Request failed with status:', xhr.status);
  }
};//绑定成功响应处理

xhr.onerror = function() {
  console.error('Request failed');
}; //失败

xhr.send();//发送请求

```





### 2.Fetch

fetch() 第一个参数是url，第二个参数是作为配置对象，定制发出的http请求



fetch是基于promise来发送网络请求的，对比xhr的话，很多功能都能实现，但是因为fetch的状态只有成功或者失败，所以不能实现进度条功能（可以用随机数方法实现假进度条）



`fetch()`采用模块化设计，API 分散在多个对象上（Response 对象、Request 对象、Headers 对象）

默认向该网址发出 GET 请求，返回一个 Promise 对象



`await`语句必须放在`try...catch`，这样捕捉可能发生的错误





####请求判断

请求成功后返回一个response对象

`Response.status`属性，得到 HTTP 回应的真实状态码，才能判断请求是否成功





####数据读取

`Response`对象根据服务器返回的不同类型的数据，提供了不同的读取方法

```
response.text()可以用于获取文本数据
response.json()主要用于获取服务器返回的 JSON 数据
response.formData()主要用在 Service Worker 里面，拦截用户提交的表单，修改某些数据以后，再提交给服务器
response.blob()用于获取二进制文件
```



#### 请求类型

1.POST

```js
const response = await fetch(url, {
  method: 'POST',
  headers: {
    "Content-type": "application/x-www-form-urlencoded; charset=UTF-8",
  },
  body: 'foo=bar&lorem=ipsum',
});

const json = await response.json();//主要记得设置一个await来等待promise
```



2.提交JSON数据

将发送请求的`Content-Type`设成`'application/json;charset=utf-8'`，因为默认发送的是纯文本



3.提交表单

获取表单元素的值，并将它们组织成一个对象或者 FormData 对象

其余步骤和POST差不多，注意数据类型



4.文件上传

上传二进制文件时，不用修改标头的`Content-Type`，浏览器会自动设置









#### 使用Fetch发起请求的步骤

1.创建请求对象，指定url，请求类型，请求头，请求体

2.发送请求并处理响应

3.处理异步请求的错误



最基本的用法

```js
fetch(url)
  .then(response => {
    if (!response.ok) {
      throw new Error('Network response was not ok');
    }
    return response.json(); // 将响应体解析为 JSON
  })
  .then(data => {
    console.log('Fetch successful:', data);
    // 处理获取到的数据
  })
  .catch(error => {
    console.error('Fetch error:', error);
    // 处理错误
  });

```



```js
async function fetchData() {
    try {
        const response = await fetch('https://api.example.com/data');
        const data = await response.json();
        console.log(data);
    } catch (error) {
        console.error('Error fetching data:', error);
    }
}
try...catch 是捕捉异常的语法，error是出现错误的原因或者异常对象
```




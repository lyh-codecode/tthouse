# Axios

### 1.定义

​	Axios是一个基于promise网络请求库，作用于node.js和浏览器中。

​	

### 2.特性 （反正很强）

​	在浏览器中发送XMLHttpRequests

​	在node.js中发送http请求

​	支持Promise API

​	拦截请求和响应

​	转换请求和响应数据

​	取消请求

​	超时处理

​	将HTML Form转换成JSON进行请求

​	自动转换JSON数据

​	获取浏览器和node.js的请求进度，提供额外信息（进度，剩余时间）



## Axios的基本使用

### 1.发送Ajax请求

​	创建一些按钮来绑定请求事件

​	例如

```js
 btn.onclick = function( ) {

	axios({
			//请求类型
		method: 'POST',
            //URL
         url:'我是目标地址',
            
  			//设置请求体 
         data = {
        		我是请求体
        }
              }).then(response => {
            console.log(response);
        });
 }
```

如果发送别的请求就按照对应格式修改

例如PUT请求，要有对应id或者其他的关键字连接对应修改位置

GET请求也是这样



### 2.其他方式发送请求

```js
//GET
axios.request({
	 method: 'GET',
	 url: '我要在什么地方获取数据',
}).then(response => {
获取回来之后怎么操作数据
})
```



```js
//POST
axios.post(
    url,
    {
     data
    }).then(respose =>{
成功操作})
```

 

### 3.配置对象的详细说明

#### 详细说明

​	





#### 设置默认配置

对重复配置的统一编写

```
axios.defaults.method = 'GET'
baseURL
params
timeout
```



### 4.创建实例对象

```js
const NiHao = axios.create({
	baseURL: ' ',
    timeout: 2000
});

//这个 NiHao对象和axios对象功能几乎一样了

直接用NiHao 发请求也可以

```

这样子可以把不同的默认地址赋予不同的实例对象，对应发送请求更简便

给谁发送就调用哪个对象



### 5.拦截器

**1.请求拦截器**类似于关卡，满足条件就放行进入下一个，否则取消请求

调用use方法

```js
axios.interceptors.request.use(function(config){

成功操作；
这里可以设置config参数

return config;
},function(error){
失败操作；
return Promise.reject(error);
});
```



**2.响应拦截器** 会对响应做预处理，数据格式化处理，没有问题交给程序处理。失败了就失败处理（响应错误等）

```js
axios.interceptors.request.use(function(config){

成功操作；

return response; //这里可以改response.data(直接处理数据)
},function(error){
失败操作；
return Promise.reject(error);
});
```

可以设置成功返回的部分，例如response.data 只返回响应数据部分



全部成功了，回调函数才能成功运行

但是请求的成功与否主要与网络请求本身是否成功有关（网络连接问题，服务器错误等）



### 6.取消请求

利用配置对象的属性来取消请求

​	定义全部变量let cancel = null;

​	在cancelToken: new axios.CancelToken(function(c){

​		cancel = c; //这里的c其实是一个函数

}).then(response=>{

​	操作了之后，初始化cancel=null；

})

​	判断cancel 是否等于null，调用cancel();

​	不为null就取消上一次请求





## 使用axios发送请求的具体步骤（GET作为实例）

#### 1.导入axios

在js文件中导入axios模块



#### 2.发送GET请求

```js
axios.get('/api/data')
  .then(response => {
    console.log('Response:', response.data);
    // 处理获取的数据
  })
  .catch(error => {
    console.error('Error fetching data:', error);
    // 处理错误
  });

```



#### 3,设置请求配置

第二个参数以对象的方式写

```js
axios.get('/api/data', {
    params: {
      id: 123
    },
    headers: {
      'Authorization': 'Bearer your_access_token'
    }
  })
  .then(response => {
    console.log('Response:', response.data);
  })
  .catch(error => {
    console.error('Error:', error);
  });

```



#### 4.处理响应

原本是用.then处理成功的响应数据，.catch处理请求过程中出现的错误

但是axios是基于Promise对象的，直接用async/await来处理异步代码

```js
async function fetchData() {
  try {
    const response = await axios.get('/api/data');
    console.log('Response:', response.data);
    // 处理返回的数据
  } catch (error) {
    console.error('Error fetching data:', error);
    // 处理错误
  }
}
fetchData();

```



#### 5.设置拦截器和全局配置

设置默认的全部配置，不用重复

拦截器可以添加认证，进行校验

```js
// 设置全局默认配置
axios.defaults.baseURL = 'https://api.example.com';
axios.defaults.headers.common['Authorization'] = 'Bearer your_access_token';

// 添加请求拦截器
axios.interceptors.request.use(config => {
  console.log('Request sent:', config);
  // 可以在此处修改配置、添加认证信息等
  return config;
}, error => {
  console.error('Request error:', error);
  return Promise.reject(error);
});

// 添加响应拦截器
axios.interceptors.response.use(response => {
  console.log('Response received:', response);
  // 可以在此处处理响应数据，如添加额外处理逻辑等
  return response;
}, error => {
  console.error('Response error:', error);
  return Promise.reject(error);
});

```







## AJAX补充

ajax是一种使用现有标准的方法，最大的优点是在不重新加载整个页面的情况下，可以与服务器交换数据并更新部分网页内容

ajax不是一种实体，更像是一种技术和思想

### 1.ajax的应用

1.用JS操作DOM来执行动态效果

2.运用XHTML + CSS 来表达资讯

3.用XML 和 XSLT 操作资料

4.用 xhr 或者 fetch 与网页服务器进行异步资料交换



### 2.ajax工作原理

1.浏览器发送请求

2.服务器处理请求

3.服务器响应返回浏览器

4.JS处理被返回的数据并更新内容



实际上在写ajax的时候，无论如何都要逃不过请求行，请求头这些信息






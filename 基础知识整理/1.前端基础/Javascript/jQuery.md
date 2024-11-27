# jQuery

## 1.jQuery语法

##### 1.概念

jQuery是通过语法选取HTML元素，然后执行一些操作

$ 是最顶级的对象

原生JS获取的就是DOM对象

jQuery方法获取的就是jQuery对象，本质是用$对DOM对象包装，伪数组形式存储



##### 2.基础语法

```
$(selector).action

$(this).hide()--隐藏当前元素
$("p").hide() --隐藏所有 <p> 元素
里面的名字和CSS选择器的一样

```



##### 3.对象转换

1.DOM变jQuery 直接加刀乐符号$

div ==>  $('div')

2.jQuery变DOM，因为是伪数组，下标索引

$('div')[0]

## 2.文档就绪事件

所有的jQuery函数都位于document ready 函数中

是为了防止文档在完全加载之前运行jQuery代码，可能会操作失败

```js
$(document).ready(function(){
 我是jQuery代码
 
});

//简洁版
$(function(){
我是jQuery代码

});
```



## 3.jQuery选择器

基于CSS选择器,方式差不多

```
1.元素选择
$("p") ==>选择页面中所有的p元素

2.id选择
#("#xixi") 

3. class选择
$(".text")

```





## 4.独立文件引入jQuery

先把jQuery写在一个独立的js文件中

直接在 < head > 部分引入jquery.min.js文件,和 自己的js文件





## 5.效果

#### 1.隐藏/显示/toggle切换

```js
$("#hide").click(function(){
  $("p").hide();
});
 
$("#show").click(function(){
  $("p").show();
});


$("button").click(function(){
	$("p").toggle(); 
})
```





#### 2.淡入淡出

```js
fadeIn() 淡入隐藏元素
$(selector).fadeIn(speed,callback); 
第一个参数可以设置规定时长（毫秒），也可以设置slow，fast等
第二个callback是回调函数，完成后执行的函数

fadeOut() 淡出可见元素
同上

fadeToggle() 切换
同上


fadeTo() 允许渐变为给定不透明度
$(selector).fadeTo(speed,opacity,callback);
```



#### 3.滑动

```js
slideDown() 用于向下滑动的元素
$(selector).slideDown(speed,callback);

slideUp() 向上

slideToggle() 切换
$("#flip").click(function(){
  $("#panel").slideToggle();
});
```



#### 4.动画

```
$(selector).animate({params},speed,callback);
```

**1.用于创建自定义动画**

params必须的参数定义动画的CSS属性，其他的都是可选择

params对象形式操作多个属性

**2.驼峰命名**

必须使用 paddingLeft 而不是 padding-left，使用 marginRight 而不是 margin-right，等等

**3.使用相对值**

```js
$("button").click(function(){
  $("div").animate({
    left:'250px',
    height:'+=150px',
    width:'+=150px'
  });
});
//相对原来增加多少用+ / -
```



#### 5.停止动画

```
$(selector).stop(stopAll,goToEnd);
1.可选择stopAll参数是否应该清除动画队列，默认false不清除，即停止当前动画，进行最新一个动画
设置为true则全部停止

2.goToEnd参数规定是否立即完成当前动画，默认false，设置为true的话，触发停止直接跳到动画结尾

```



#### 6.回调函数

```js
1.动画问题

$("button").click(function(){
	$("p").hide("slow",function(){
		alert("段落被隐藏了")；
});
});

如果不用回调函数，下面的alert会在隐藏效果完成前弹出
使用回调函数，则会在动画效果完成之后，执行函数
```



#### 7.链

如果多个动作执行，可以把动作追加到之前的动作上，这样就不用多次查找相同元素

```js
$("#p1").css("color","red").slideUp(2000).slideDown(2000);
```

在一个元素上找它的父节点或子节点也同样，看当前执行动作的对象是谁就可以了







## 6.操作HTML

#### 1.DOM操作

```js
.text() --设置或返回所选元素的文本内容
.html() --设置或返回所愿元素的内容，包括html标签
$("#test").val() --设置或返回表单字段的值 //value 属性的值

<input type="text" id="test" value="菜鸟教程">
    
$("a").attr("href") 获取href值

设置的话直接在空格里面填就好了
$("#btn1").click(function(){
    $("#test1").text("hello wokao"); 
});


```



#### 2.添加元素/删除元素

```
1.子插入（在内部）
append() -在被选中元素的结尾插入内容
prepend() -在被选中元素开头插入内容

2.兄弟插入（）
after() -在选中元素之后插入内容
before() -在被选中元素之前插入内容


3.remove() 全部删除，包括自己
4.empty() 清空子元素，保留自己
```





#### 3.设置CSS样式

```
1.设置
addClass() --向被选择元素增加类/多个类
removeClass() --移除类
toggleClass() --切换

2.css方法
css() -设置或返回样式属性
css("propertyname"); 返回指定属性
css("propertyname","value"); 设置属性
多个直接用对象形式
$("p").css({"background-color":"yellow","font-size":"200%"});
```





#### 4.尺寸处理

```
width() 设置或返回元素宽度
height() 高度

innerWidth() 包括内边距
innerHeight()

outerWidth() 包括内边距和边框
outerHeight()
```



#### 5.位置方法

设置或者获取元素偏移

```
1.offset({left:xx,top:xx}) 相对于文档偏移，与父级无关
 offset().left 获取
 
2.position()  相对于带有定位的父级元素，没有就看文档

3.scrollTop()/scrollLeft() 被卷去的头部距离，左侧距离
```

对于第三个，用一个变量接收指定盒子被卷去头部的多少，制作锚点链接，或者是显示隐藏

## 7.遍历

#### 1.根据相对于其他元素的关系来查找元素

```
1.查找祖先,向上遍历DOM树
parent() 直接父元素，向上一级

parents() 所有祖先元素，一直向上直到html

parentsUntil() 查找给定两个元素之间的所有祖先元素

$("span").parentsUntil("div") ==> 查找span到div之间所有span的祖先元素


2.查找后代
children() 亲儿子

find() 所有后代

3.同级遍历，找兄弟
siblings() 除了自己，全部遍历

next() 返回下一个同胞

nextAll() 自己下面的全部同胞

nextUntil() 两个元素之间的全部同胞

prev() 和上面的原理相同，方向相反
prevAll()
prevUntil()

```

#### 2.遍历过滤

##### 1.最基本的过滤方法

```js
first() 返回被选中元素的首个元素（从上到下第一个）

last() 最后一个

eq() 指定索引
$(document).ready(function(){
  $("p").eq(1);
});
//返回第二个，索引0开始
```

##### 2.其他两个

```js
//返回不匹配标准的所有元素
$(document).ready(function(){
  $("p").not(".url");
});

//返回匹配标准的所有元素，不匹配的删除
$(document).ready(function(){
  $("p").filter(".url");
});
```



#### 3.each

jQuery隐式迭代是对同一元素做相同操作，如果要不同操作要用each

##### 1.each

```js
$("div").each(function(index,domElement) {
	我是操作
})；
```

index返回的是遍历索引，0，1，2，，，

domElement是遍历的元素

##### 2.$.each

```js
$.each(obj,function(index,element){
   操作你
});
```

$.each遍历方法可用于任何遍历对象，主要用于数据处理，数组，对象





## 8.AJAX

具体应用还没看



1.load

URL ：希望加载的URL

data：参数规定与请求一同发送的查询字符串，键值对集合

callback：load完成后的回调函数

```
$(selector).load(URL,data,callback);
```



2.get/post请求

get

```js
$.get(URL,callback);
或
$.get( URL [, data ] [, callback ] [, dataType ] )

$("button").click(function(){
  $.get("demo_test.php",function(data,status){
    alert("数据: " + data + "\n状态: " + status);
  });
});
```

- **URL**：发送请求的 URL字符串。
- **data**：可选的，发送给服务器的字符串或 key/value 键值对。
- **callback**：可选的，请求成功后执行的回调函数。
- **dataType**：可选的，从服务器返回的数据类型。默认：智能猜测（可以是xml, json, script, 或 html）。



post

```js
$.post(URL,callback);
或
$.post( URL [, data ] [, callback ] [, dataType ] )

$("button").click(function(){
    $.post("/try/ajax/demo_test_post.php",
    {
        name:"菜鸟教程",
        url:"http://www.runoob.com"
    },
    function(data,status){
        alert("数据: \n" + data + "\n状态: " + status);
    });
});
```

- **URL**：发送请求的 URL字符串。
- **data**：可选的，发送给服务器的字符串或 key/value 键值对。
- **callback**：可选的，请求成功后执行的回调函数。
- **dataType**：可选的，从服务器返回的数据类型。默认：智能猜测（可以是xml, json, script, 或 html）。


## 9.事件

### 1.on

```js
$(selector).on(event,childSelector,data,function)
```

```js
$(document).ready(function(){
  $("p").on("click",function(){
    alert("段落被点击了。");
  });
});
```



### 2.off

off() 方法通常用于移除通过 on() 方法添加的事件处理程序

```js
$(selector).off(event,selector,function(eventObj),map)
```



### 3.one

用一次就移除

```js
$(selector).one(event,data,function)

$("p").one("click",function(){
  $(this).animate({fontSize:"+=6px"});
	});
```



### 4.trigger/triggerHandler

#### 区别

trigger() 方法触发被选元素上指定的事件以及事件的默认行为（比如表单提交）

trigger() 方法不触发默认行为，只触发指定事件

.trigger() 会操作 jQuery 对象匹配的所有元素，而 .triggerHandler() 只影响第一个匹配元素

由 .triggerHandler() 创建的事件不会在 DOM 树中冒泡；如果目标元素不直接处理它们，则不会发生任何事情



```js
$(selector).triggerHandler(event,param1,param2,...)
$(selector).trigger(event,eventObj,param1,param2,...)
```



### 5.拷贝

#### 1.浅拷贝和深拷贝

区别主要体现在对象上，其他的键值对都是直接赋值

浅拷贝：直接把对象的地址赋值给拷贝对象，修改拷贝对象的值，被拷贝的一方值也会改变

深拷贝：创建一个新的对象，然后把新对象的值赋值给拷贝对象，两者修改不影响对方



#### 2.方法

```js
$.extend(targetObj,obj)
obj==>targetObj 
第一个参数是默认false == 浅拷贝
设置为true == 深拷贝
```





### 6.其他事件方法

#### 1.键盘/鼠标事件

和之前了解的感觉差不多





#### 2.杂项方法

比如$符号的控制权之类的，时间紧迫，用到再学一下

```js
var jq=$.noConflict();
```

noConflict() 方法释放变量 $ 的 jQuery 控制权。

该方法也可用于为 jQuery 变量规定新的自定义名称。

多库共存的时候使用


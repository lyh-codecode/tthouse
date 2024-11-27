# JS事件

## 1.页面加载事件

### 1.load事件

页面所有资源都加载完，包括DOM节点还有CSS样式渲染

给整个window加

```js
window.addEventListener('load',function(){
    操作
})
```



### 2.DOMContentLoaded事件

只需等待DOM节点加载完成，无序等待CSS或者图片加载，速度较快

给document加

```js
document.addEventListener('DOMContentLoaded',function(){
操作
})
```





## 2.页面滚动事件

### 1.scroll事件

滚动时持续触发的事件,常见给window加，给某个固定元素加也是可以的

```js
window.addEventListener('scroll',function(){

const n = document.documentElement.scrollTop
console.log(n)
})

```

#### scrollTop参数

判断卷去的头部有多长(看不到的部分)，可以进行相应的操作

返回的scrollTop是数字，不带单位的





## 3.页面尺寸事件

### 1.窗口尺寸改变触发resize

```js
window.addEventListener('resize',function(){
    
})
```

### 2.宽高获取

#### 1.检测盒子宽度clientWidth/ 高度clientHeight

这个检测不包含边框，padding，滚动条等

```js
const div = document.querySelector('div')
console.log(div.clientWidth)
console.log(div.clientHeight)
```



### 2.offsetWidth / offsetHeight

检测盒子可视宽高，包括设置的padding/border 

如果不可见得到的是0



### 3.获取位置

offsetLeft/Top获取位置，固定的，相对于最近的祖先元素





 












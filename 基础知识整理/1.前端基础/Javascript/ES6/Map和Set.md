# Map和Set

### Map

#### 1.基本概念

`Map` 是一种键值对的集合，其中的键和值可以是任意类型的数据（包括基本类型、对象引用等）

`Map` 中的键是唯一的；每个键对应一个值

`Map` 可以用来存储和操作各种类型的数据，尤其适合需要以键值对形式存储和访问数据的场景

####2.特点

1.存储类型任意，包括基本数据类型和函数，对象等

2.键唯一，后面出现重复键名直接覆盖

3.按照顺序迭代



#### 3.Map创建

key 可以是字符串，对象，函数，NaN

```js
// 创建一个空的 Map
let map = new Map();

// 设置键值对
map.set('key1', 'value1');
map.set(1, 'value2');
map.set({}, 'value3');

// 获取值
console.log(map.get('key1')); // 输出: 'value1'

// 检查键是否存在
console.log(map.has('key1')); // 输出: true

// 删除键值对
map.delete('key1');

// 清空 Map
map.clear();

// 获取 Map 的大小
console.log(map.size);

```

#### 4.Map的迭代

用 for...of 或者forEach() 遍历

```js
//for...of
let myMap = new Map();
myMap.set('key1', 'value1');
myMap.set('key2', 'value2');
myMap.set('key3', 'value3');

// 使用 for...of 遍历 Map
for (let [key, value] of myMap) {
  console.log(key + ' = ' + value);
}



//forEach()
var myMap = new Map();
myMap.set(0, "zero");
myMap.set(1, "one");
// 将会显示两个 logs。 一个是 "0 = zero" 另一个是 "1 = one"
myMap.forEach(function(value, key) {
  console.log(key + " = " + value);
}, myMap)
```









### Set

#### 1.基本概念

是一种集合，存储的值是唯一的，不允许重复

#### 2.特点

元素唯一，顺序迭代，类型不限

#### 3.Set创建

```js
let set = new Set();

//添加元素
set.add('value1');
set.add(1);
set.add({ key: 'value' });

// 检查元素是否存在
console.log(set.has('value1')); // 输出: true

// 删除元素
set.delete('value1');

// 清空 Set
set.clear();

console.log(set.size); //检查大小
```



#### 4.Set遍历

```js
let set = new Set([1, 2, 3, 4]);
for (let item of set) {
    console.log(item);
}




let set = new Set(['apple', 'banana', 'cherry']);
set.forEach(function(value, valueAgain, set) {
    console.log(value);
});
//为了与 Map 的 forEach 方法保持一致，forEach 方法会为每个元素传入相同的值作为第二个参数
//value 和 valueAgain 都将是当前遍历到的元素的值
```



####5.Set 中的特殊值

Set 对象存储的值总是唯一的，所以需要判断两个值是否恒等。有几个特殊值需要特殊对待：

- +0 与 -0 在存储判断唯一性的时候是恒等的，所以不重复；
- undefined 与 undefined 是恒等的，所以不重复；
- NaN 与 NaN 是不恒等的，但是在 Set 中只能存一个，不重复。




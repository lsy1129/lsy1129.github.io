---
title: 2022/7/18-2022/7/23组内分享
categories: 分享
tags: 
  - javascript
  - vue
---

## 2022/07/18分享

### 空值合并操作符（??）

空值合并操作符（??）是一个逻辑操作符，当左侧的操作数为 null 或者 undefined 时，返回其右侧操作数，否则返回左侧操作数。

与逻辑或操作符（||）不同，逻辑或操作符是左边是空字符串或false或0等false值，都会返回后侧的值。

~~~ javascript
const foo = null ?? 'default string';
console.log(foo); 
// output: "default string"

const baz = 0 ?? 42;
console.log(baz); 
// output: 0
~~~

#### 使用空值合并操作符

~~~ javascript
const nullValue = null;
const emptyText = ""; // 空字符串，是一个假值，Boolean("") === false
const someNumber = 42;

const valA = nullValue ?? "valA 的默认值";
const valB = emptyText ?? "valB 的默认值";
const valC = someNumber ?? 0;

console.log(valA); // "valA 的默认值"
console.log(valB); // ""（空字符串虽然是假值，但不是 null 或者 undefined）
console.log(valC); // 42
~~~

#### 为变量赋默认值

~~~javascript
let foo;

//  foo is never assigned any value so it is still undefined
let someDummyText = foo || 'Hello!';
~~~

#### 浏览器兼容性
{% asset_img 1.png %}

## 2022/07/19分享

### 可选链操作符 ( ?. ) 

?.直接在链式调用的时候判断，判断左侧的对象是否为null或undefined，如果是的，就不再往下运算，返回undefined，如果不是，则返回右侧的值。

可以使用?.简化&&和三元运算符

~~~ javascript
let street = user.address && user.address.street;

// 简化
let street = user.address?.street
~~~

#### 浏览器兼容性
{% asset_img 2.png %}

## 2022/07/20分享

### 使用Array.prototype.at()简化arr.length

> at() 方法接收一个整数值并返回该索引的项目，允许正数和负数，表示获取指定位置的成员。
> 参数正数就表示顺数第几个，负整数从数组中的最后一个项目开始倒数。

~~~ javascript
var arr = [1, 2, 3, 4, 5]
// 以前获取最后一位
console.log(arr[arr.length-1]) //5
// 简化后
console.log(arr.at(-1)) // 5
~~~

## 2022/07/21分享

> css 怎样穿透样式？穿透符能穿透修改 vue #app 节点外元素的样式吗？

##### ::v-deep vue3.0 开始，可使用 ::v-deep 替代 /deep/

~~~less
<style lang="less" scoped> 
   ::v-deep .el-input {
       width: 120px;
   }
</style>
~~~

##### /deep/ vue2 中可使用 /deep/ 穿透样式~

~~~less
<style lang="less" scoped> 
   /deep/ .el-input {
       width: 120px;
   }
</style>
~~~

##### >>> 仅对 css 有效，对于 css 预处理语言，例如 scss、less 不生效。

对于 vue 中 div#app 节点外的元素样式，如果 '' 加上了 scoped，那么此时样式穿透符是不能穿透修改 div#app 节点外的元素样式的。
这是因为 scoped 的作用域仅局限在 div#app 容器内部，所以此时只能修改 div#app 容器内的样式。
例如 el 组件的下拉选的弹出层是 div#app 的兄弟元素，body的子元素，在 '' 中使用样式穿透符修改该弹出层的样式是无效的。

## 2022/07/22分享

### JS代码优化技巧（一）

#### 带有多个条件的 if 语句

~~~ javascript
// 优化之前
if (x === 'abc' || x === 'def' || x === 'ghi' || x ==='jkl') {
}
// 优化之后
if (['abc', 'def', 'ghi', 'jkl'].includes(x)) {
}
~~~

## 2022/07/23分享

### JS代码优化技巧（二）

#### switch 简化

> 可以将条件保存在键值对象中，并根据条件来调用它们

~~~javascript
// 优化之前
switch (data) {
  case 1:
    test1();
  break;
  case 2:
    test2();
  break;
  case 3:
    test();
  break;
  // ...
}
// 优化之后
var data = {
  1: test1,
  2: test2,
  3: test
};
data[something] && data[something]();
~~~
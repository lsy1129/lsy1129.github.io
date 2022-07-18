---
layout: post
title: 2022/06/20-2022/06/25组内分享
date: 2022-07-18 09:39:45
categories: 分享
tags:
  - vue
  - vue3
  - javascript
  - typescript
sharedBy: lsy
---

## 2022/06/20分享

### reduce的用法
reduce() 方法对数组中的每个元素执行一个由您提供的reduce函数(升序执行)，将其结果汇总为单个返回值。
#### 语法：
```typescript
/**
prev 必需。累计器累计回调的返回值; 表示上一次调用回调时的返回值，或者初始值 init;
cur 必需。表示当前正在处理的数组元素；
index 可选。表示当前正在处理的数组元素的索引，若提供 init 值，则起始索引为- 0，否则起始索引为1；
arr 可选。表示原数组；
init 可选。表示初始值。
*/
arr.reduce(function(prev,cur,index,arr){
...
}, init);
```
#### 用法：
``` javascript
let myArray = ['a', 'b', 'a', 'b', 'c', 'e', 'e', 'c', 'd', 'd', 'd', 'd'];
let myOrderedArray = myArray.reduce(function (accumulator, currentValue) {
  if (accumulator.indexOf(currentValue) === -1) {
    accumulator.push(currentValue)
  }
  return accumulator;
}, []);
```
这里主要是借助迭代功能实现数组的扩展，判断当前元素是否已经添加到数组中，如果不存在就从尾部添加；
#### 总结：
 reduce() 是数组的归并方法，与 forEach()、map()、filter()等迭代方法一样都会对数组每一项进行遍历，但是reduce() 可同时将前面数组项遍历产生的结果与当前遍历项进行运算，这一点是其他迭代方法无法企及的。

## 2022/06/21分享

### watchEffect属性
watch 的套路是：既要指明监视的属性，也要指明监视的回调
watchEffect 的套路是：不用指明监视哪个属性，监视的回调中用到哪个属性，那就监视哪个属性
watchEffect有点像computed：
* 但computed注重的计算出来的值（回调函数的返回值)，所以必须要写返回值
* 而watchEffect更注重的是过程（回调函数的函数体)，所以不用写返回值

```typescript
import {reactive,watchEffect} from 'vue'

export default {
  name: 'Demo',
  setup() {
    let person = reactive({
      name: "张三",
      age: 18,
      job:{
        j1:{
          salary:20
        }
      }
    })

    watchEffect(()=>{
      const x1 = person.name;
      console.log("watchEffect所指定的回调执行了"+x1);
    })
    return {
      person
    }
  }
}
</script>
```

## 2022/06/22分享

### vue3 在setup访问路由
> setup 里不能访问 this，不能再直接访问 this.$router 或 this.$route。（getCurrentInstance可以替代this但不推荐）
> 推荐：使用useRoute 函数和useRouter函数替代this.$route 和 this.$router

```typescript
<script setup>
import { useRouter, useRoute } from 'vue-router'
    const route = useRoute()
    const router = useRouter()
    
    function pushWithQuery(query) {
      router.push({
        name: 'search',
        query: {
          ...route.query,
        },
      })
    }
  <script/>
```

## 2022/06/23分享

### ref和reactive
#### ref
ref是一个函数，接受一个简单类型或者复杂类型的传入并返回一个响应式且可变的 ref 对象
* 参数: 传入数据 所有数据类型都支持
* 返回值: 实现了响应式的数据
  
*注意：* 在 setup 中使用数据时必须要 .value
```typescript
<script setup lang="ts">
    import { ref } from "vue";
    let count = ref(10)
    setInterval(()=>{
        count.value++;
    }, 1000)
</script>
```
#### reactive
reactive是一个函数，接收一个普通的对象传入，把对象数据转化为响应式对象并返回，用于声明响应式数据的函数
* 参数: 传入数据(必须是引用数据类型)
* 返回值: 实现了响应式的数据
```typescript
<template>
<script setup lang="ts">
    import { ref, reactive } from "vue";
    let users = reactive([
        {
            name: '张三',
            age: 18,
            hobby: ()=>{ console.log('李四') }
        }
    ])
    setInterval(()=>{
        refUsers[0].value.age++;
    },1000)
</script>
```
#### ref响应函数与reactive响应函数的区别
两个函数都是用于声明响应式数据的函数
* ref支持基本数据类型与引用数据类型
* reactive只支持引用数据类型

*注意：* ref 其实就是对 reactive 的一层包装，内部调用 reactive 生成一个响应式的对象, 在外面包一个对象

## 2022/06/24分享

### typescript类型断言
类型断言（Type Assertion）可以用来手动指定一个值的类型。
```typescript
const foo = {};
foo.bar = 123; // Property 'bar' does not exist on type '{}'.
foo.bas = "hello"; // Property 'bas' does not exist on type '{}'.
```
代码发出了错误警告，因为 foo 的类型推断为 {}，即是具有零属性的对象。因此，你不能在它的属性上添加 bar 或 bas，可以通过类型断言来避免此问题
```typescript
interface Foo {
  bar: number;
  bas: string;
}
const foo = {} as Foo;
foo.bar = 123;
foo.bas = 'hello';
```

## 2022/06/25分享

### TypeScript：类访问修饰符public, private, protected
- public：修饰的属性或方法是公有的，可以在任何地方被访问到，默认所有的属性和方法都是 public 的
- private：修饰的属性或方法是私有的，只能在类的内部进行访问
- protected：修饰的属性或方法是受保护的，它和 private 类似，区别是它在子类中也是允许被访问的
```typescript
class Phone{
	constructor(owner : string) 
    {
		this.owner = owner; 
	}
	makeCall(ownerName : string, phoneNumber : string) : void 
    {
		if(ownerName == this.owner) {
			console.log(this.owner, "make call to ", phoneNumber);
		}
		else{
			console.log("Invalid owner, can't make call");
		}
	}
	private owner : string; //定义为private，只能在类的内部进行访问
}
 
let aPhone= new Phone("XiaoMing");    
aPhone.makeCall("XiaoMing", "12345"); //输出：XiaoMing make call to  12345
aPhone.makeCall("XiaoHong", "67890"); //输出：Invalid owner, can't make call
aPhone.owner = "XiaoHong";            
//在类的外部无法对owner进行访问，输出：Property 'owner' is private and only accessible within class 'Phone'.
```

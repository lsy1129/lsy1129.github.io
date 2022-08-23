---
layout: post
title: 2022/08/22-2022/08/26组内分享
date: 2022-08-20 11:26:00
categories: 分享
tags:
  - vue
  - javascript
  - typescript
sharedBy: lsy
---

## 2022/08/22分享

### 对象动态属性

声明对象时，如果属性是动态的，可以这样声明:
``` javascript
const dynamic = 'color';
var item = {
    brand: 'Ford',
    [dynamic]: 'Blue'
}
console.log(item); 
// { brand: "Ford", color: "Blue" }
```

## 2022/08/23分享

### 如何在forEach的循环里使用break

查阅MDN，上面有一个备注：
{% asset_img 1.png %}

#### 在forEach里合法的使用break

```javascript
function breakInForEach(arr) {
	let BreakException = {};
	let res = false;
	try {
	    arr.forEach(item => {
	       if (item === 2) {
	          res = true;
		  throw BreakException;
	        }
	    })
	}
	catch(e) {
	    if (e !== BreakException) throw e
	}
	return res;
}
console.log(foreachBreak([1， 2， 3， 4， 5， 6])); // true
```

#### 也可以使用every 或者 some等
- every: 碰到return false的时候，循环中止，return true 循环继续；
- some: 碰到return ture的时候，循环中止，return false 循环继续;

## 2022/08/24分享

### 检查对象是否为空

检查对象是否为空，实际上并不那么简单，即使对象为空，每次检查对象是否等于 {} 也会返回 false。

``` javascript
const isEmpty = obj => Reflect.ownKeys(obj).length === 0 && obj.constructor === Object;
isEmpty({}) // true
isEmpty({a:"not empty"}) //false
```

## 2022/08/25分享

### TypeScript数字分隔符_

``` typescript
const num:number = 1_2_345.6_78_9
console.log(num) // 12345.6789
```

_可以用来对长数字做任意的分隔，主要设计是为了便于数字的阅读，编译出来的代码是没有下划线的，请放心食用。

## 2022/08/26分享

### TypeScript交叉类型

交叉类型，用&操作符表示，交叉类型就是两个类型必须存在

``` typescript
interface IpersonA{
  name: string,
  age: number
}
interface IpersonB {
  name: string,
  gender: string
}

let person: IpersonA & IpersonB = { 
    name: "师爷",
    age: 18,
    gender: "男"
};
```

person 即是 IpersonA 类型，又是 IpersonB 类型

> **注意：**交叉类型取的多个类型的并集，但是如果key相同但是类型不同，则该key为never类型
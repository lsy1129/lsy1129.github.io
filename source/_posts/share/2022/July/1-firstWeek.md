---
layout: post
title: 2022/07/04-2022/07/08组内分享
date: 2022-07-18 10:25:32
categories: 分享
tags:
  - vue
  - javascript
sharedBy: myy
---

## 2022/07/04分享

导出文件时（responseType：arraybuffer），会存在没有数据或者超出最大导出条数限制，可以借助try...catch...给出后端返回的数据 

{% asset_img 1.png %}

## 2022/07/05分享

### js运行机制：

{% asset_img 2.png %}

输出结果的顺序为：2，4，5，10，8，9，3，6，1，7

## 2022/07/06分享

### 数组交集，并集，差集

{% asset_img 3.png %}

## 2022/07/07分享

### 判断数组是不是每一项都满足：

普通数组:

~~~ javascript
[1, 2, 3].every(item => { return item > 2 })
~~~

数组对象：

~~~ javascript
const arr = [{ age: 3 }, { age: 4 }, { age: 5 }]
arr.every(item => { return item.age > 2 })
~~~

### 判断数组是不是有一项满足：

普通数组:

~~~ javascript
[1, 2, 3].some(item => { return item > 2 })
~~~

数组对象：

~~~ javascript
const arr = [{ age: 3 }, { age: 4 }, { age: 5 }]
arr.some(item => { return item.age < 4 })
~~~

## 2022/07/08分享

### 动态表单的校验

{% asset_img 4.png %}


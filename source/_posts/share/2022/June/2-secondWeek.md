---
layout: post
title: 2022/06/06-2022/06/10组内分享
categories: 分享
date: 2022-07-18 09:07:10
tags:
  - javascript
sharedBy: myy
---

## 2022/06/06分享

vue2中，列表渲染的时候，不建议v-for与v-if一起使用，如若有此需要，需要使用机算属性，过滤一下列表数据

{% asset_img 1.png %}

## 2022/06/07分享

vue中，v-on可以绑定多个事件

{% asset_img 2.png %}

## 2022/06/08分享

### forEach如何跳出循环

利用try catch

{% asset_img 3.png %}

## 2022/06/09分享

### vue开发中巧用template

这样可以少嵌套一层元素

{% asset_img 4.png %}

在template上使用v-for指令，还能解决 v-for 和 v-if 同时使用报出的警告问题

{% asset_img 5.png %}

## 2022/06/10分享

### $on('hook:')的使用

{% asset_img 6.png %}

{% asset_img 7.png %}

创建定时器和销毁定时器的方法不放在一起，不方便维护，容易忘记清除这个定时器，可以用$on('hook:')来监听beforeDestory生命周期来销毁定时器
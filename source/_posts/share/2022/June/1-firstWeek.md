---
layout: post
title: 2022/5/30-2022/06/02组内分享
categories: 分享
date: 2022-07-18 08:12:38
tags:
  - 网关
  - vue
  - javascript
sharedBy: dah
---

## 2022/05/30分享

### iview控制表单项显示与隐藏

最佳方式在FormItem外层增加div 增加v-if

{% asset_img 1.png %}

直接在FormItem上增加v-if，可能会导致验证信息不能及时隐藏

{% asset_img 2.png %}

## 2022/05/31分享

### 异步函数(async await)的正确使用

await后跟promise对象可以返回promise对象resolve和reject的结果

捕获异常直接对await语句加try catch

##### 正确使用

{% asset_img 3.png %}

##### 错误使用

{% asset_img 4.png %}

## 2022/06/01分享

### package.json中包版本号说明

* '2.1.1'   表示安装指定的版本号，也就是安装2.1.1版本。
* '~2.1.1' 表示安装2.1.x的最新版本，安装时不改变大版本号和次要版本号。
* '^2.1.1'  表示安装2.x.x的最新版本，安装时不改变大版本号

现在项目中普遍用到的是第3种

{% asset_img 5.png %}

## 2022/06/02分享

后端微服务架构简单介绍，方便和后端沟通接口问题网关为单独的微服务，所有的业务微服务都挂在网关上，

404排除URL地址拼写错误，一般为业务服务在网关上的挂载问题。

500一般为实际业务服务报错或依赖服务报错。

{% asset_img 6.png %}
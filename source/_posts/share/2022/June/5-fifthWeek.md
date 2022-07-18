---
layout: post
title: 2022/06/27-2022/07/01组内分享
date: 2022-07-18 09:58:15
categories: 分享
tags:
  - Webpack
sharedBy: dah
---

## 2022/06/27分享

### Webpack构建单页面应用读取环境变量

1.docker拉取node、Ngix都有的镜像

{% asset_img 1.png %}

2.使用webpack的definePlugin在打包的时候写入环境变量

{% asset_img 2.png %}

3.代码中读取环境变量

{% asset_img 3.png %}

## 2022/06/28分享

### Webpack提高构建性能

loader应用于最少量的必要模块，减少loader转换和扫描的时间

{% asset_img 4.png %}

## 2022/06/29分享

### Webpack提高构建性能

dll,为更改不频繁的代码生成单独的编译结果。提高编译速度

1.单独编写dll打包配置文件，为固定且较大的包单独生成dll，使用webpack的dllPlugin

{% asset_img 5.png %}

2.生成对应的dll和dll的包的映射文件如下

{% asset_img 6.png %}

3.在打包文件通用manifest映射文件，使用生成的dll,并把dll文件打包到html中

{% asset_img 7.png %}

## 2022/06/30分享

Webpack代码分离，避免打包出过大bundle。

入口分离，SplitChunksPlugin提取分离Chunk中公共部分

{% asset_img 8.png %}

## 2022/07/01分享

webpack动态导入实现代码分离，预加载、预获取提高页面性能

{% asset_img 9.png %}

动态导入的模块，会打包生成独立的 bundle。

预获取prefetch,在当前页面chunk加载完后，利用网络空闲加载可能会被用户加载的内容，应用场景：
页面上点击按钮，弹窗展示另一个组件，预获取弹窗组件

预获取prefetch,在当前页面chunk加载完后，利用网络空闲加载可能会被用户加载的内容，应用场景：
页面上点击按钮，弹窗展示另一个组件，预获取弹窗组件

页面上需要引用很大包，例如图表库。
会在加载当前页面的同时加载独立库，会由两次请求，合并为一次请求


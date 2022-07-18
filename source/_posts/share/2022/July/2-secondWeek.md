---
layout: post
title: 2022/07/11-2022/07/16组内分享
date: 2022-07-18 10:37:01
categories: 分享
tags:
  - vue3
  - javascript
  - typescript
sharedBy: gcg
---

## 2022/07/11分享

vue3：不需要响应式的引用类型数据用shallowRef定义

{% asset_img 1.png %}

## 2022/07/12分享

vue3实现传送门(同ReactDOM.createPortal)：
teleport为vue3新增的内置组件

{% asset_img 2.png %}

常用语实现modal或message类组件的封装；

## 2022/07/13分享

在 3.x 中，自定义组件上的 v-model 相当于传递了 modelValue prop 并接管抛出的 update:modelValue 事件：

~~~ html
<ChildComponent v-model="pageTitle" />
<!-- 简写: -->

<ChildComponent
  :modelValue="pageTitle"
  @update:modelValue="pageTitle = $event"
/>
~~~

若须要更改 model 名称，而不是更改组件内的 model 选项，那么当初咱们能够将一个 argument 传递给 model：

~~~ html
<ChildComponent v-model:title="pageTitle" />
<!-- 简写: -->

<ChildComponent :title="pageTitle" @update:title="pageTitle = $event" />
~~~

## 2022/07/14分享

vue3重定向组件（协同平台公共入口，携token直接登录问题管理平台）：

{% asset_img 3.png %}

## 2022/07/15分享

### less变量的定义及使用：

####  定义

~~~ less
@link-color:  #428bca; // sea blue
@link-color-hover:  darken(@link-color, 10%);
~~~

#### 使用

~~~ less
a,
.link {
  color: @link-color;
}
a:hover {
  color: @link-color-hover;
}
.widget {
  color: #fff;
  background: @link-color;
}
~~~

## 2022/07/16分享

vue3 异步组件&加载过程中的占位组件，内置组件Suspense的使用

~~~ typescript
<template>
  <div>
    <button @click="showButton">展示异步组件</button>
    <template v-if="isShowButton">
      <Suspense>
        <template #default>
          <AsyncButton></AsyncButton>
        </template>
        <template #fallback>
          <div>组件加载中...</div>
        </template>
      </Suspense>
    </template>
  </div>
</template>
<script>
import { defineAsyncComponent } from "vue";
const AsyncButton = defineAsyncComponent(() =>
  import("./components/AsyncButton.vue")
);
export default {
  setup() {
    const isShowButton = ref(false);
    function showButton() {
      isShowButton.value = true;
    }
    return {
      isShowButton,
      showButton,
    };
  },
}
</script>
~~~
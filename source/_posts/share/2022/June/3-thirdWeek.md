---
layout: post
title: 2022/06/13-2022/06/17组内分享
date: 2022-07-18 09:18:27
categories: 分享
tags:
  - vue
  - vue3
  - javascript
  - typescript
sharedBy: gcg
---

## 2022/06/13分享

### 路由组件keep-alive区别

#### vue2

{% asset_img 1.png %}

#### vue3

{% asset_img 2.png %}

(注意组件name定义，以及setup语法糖问题)

## 2022/06/14分享

vue3动态ref使用（常见于v-for生成的表单或其他组件，用于获取组件实例）：
{% asset_img 3.png %}
{% asset_img 4.png %}
{% asset_img 5.png %}

## 2022/06/15分享

### vue3：setup语法糖&setup钩子函数的用法区别及使用场景

##### 语法糖：

~~~ javascript
 <script setup>
    import {ref,reactive,defineProps,defineEmits} from "vue";

    defineProps({
        msg: String,
        num: {
        type:Number,
        default: 0
        }
    });
    const emitList = defineEmits(['handleNodeClick'])
    const handleNodeClick = (e) => {
        emitList('gatewayData', label.value)
    }
</script>
~~~

##### setup钩子：

~~~ javascript
<script>
    import {defineComponent} from "vue";
    export default defineComponent({
    props:{
        num: {
            type:Number,
            default: 0
        }
    },
    emits: ["handleNodeClick"],
    setup(props,context){
        const handleNodeClick = (e) => {
            context.emit('gatewayData', label.value)
        }

        return {
        handleNodeClick
        }
    }
    })
</script>
~~~

### 总结:  

使用setup语法糖，引用组件不需要注册，定义ref&reactive也不需要return，可直接在template使用；

 setup语法糖中，无法定义组件name（可以使用两个script标签，但不推荐），需要keep-alive的组件尽量使用setup钩子写法（对应2022/06/13 keep-alive的分享）;

 ### 易错点：
 
 emit  OR  emits

 ## 2022/06/16分享

 ### vue3+ts

 组件setup接收参数，使用interface为props定义泛型

 {% asset_img 6.png %}

  ## 2022/06/17分享

  ###  vue3 子组件ref变量和defineExpose

  在标准组件写法里，子组件的数据都是默认隐式暴露给父组件的，但在 script-setup 模式下，所有数据只是默认 return 给template 使用，不会暴露到组件外，所以父组件是无法直接通过挂载 ref 变量获取子组件的数据。

  在标准组件写法里，子组件的数据都是默认隐式暴露给父组件的，但在 script-setup 模式下，所有数据只是默认 return 给template 使用，不会暴露到组件外，所以父组件是无法直接通过挂载 ref 变量获取子组件的数据。

  ##### 子组件：

   {% asset_img 7.png %}

  ##### 父组件：

   {% asset_img 8.png %}


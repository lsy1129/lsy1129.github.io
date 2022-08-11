---
layout: post
title: 2022/08/01-2022/08/12组内分享
date: 2022-08-10 8:46:32
categories: 分享
tags:
  - Webpack
  - Vite
sharedBy: gcg
---

## 2022/08/08分享

React组件内存泄漏问题，【Warning: Can't perform a React state update on an unmounted component. This is a no-op, but it indicates a memory leak in your application.】

以最常见的FC组件描述触发场景：

1、页面使用useEffect调用getData()获取并更新页面数据；

2、进入页面后，在接口响应前离开页面（即卸载组件)；

3、由于：接口，接口回调，react的useState都是异步操作，导致组件卸载后，这些异步操作仍然占用内存；

解决方案：

合理使用useEffect的return；通过变量标识当前组件的挂载状态，在接口异步操作中通过该变量判断是否需要进行状态的更新(setState)

~~~ typescript
const [value, setValue] = useState('checking value...');
useEffect(() => {
let isMounted = true;
fetchValue().then(() => {
      if(isMounted ){
      setValue("done!"); // no more error
      } 
    });
   return () => {
    isMounted = false;
    };
}, []);
~~~

## 2022/08/09分享

### React16.X context的使用

16.x 之后的Context使用了Provider和Customer模式,在顶层的Provider中传入value，在子孙级的Consumer中获取该值，并且能够传递函数，用来修改context

1、声明一个全局的 context 定义,context.js

~~~ typescript
import React from 'react'
let { Consumer, Provider } = React.createContext();//创建 context 并暴露Consumer和Provider模式
export {
    Consumer,
    Provider
}
~~~

2、父组件导入

~~~ typescript
// 导入 Provider
import {Provider} from "../../utils/context"

<Provider value={name}>
  <div style={{border:'1px solid red',width:'30%',margin:'50px auto',textAlign:'center'}}>
    <p>父组件定义的值:{name}</p>
    <EightteenChildTwo></EightteenChildTwo>
  </div>
</Provider>
~~~

3、子组件使用

~~~ typescript
// 导入Consumer
import { Consumer } from "../../utils/context"
function Son(props) {
  return (
    //Consumer容器,可以拿到上文传递下来的name属性,并可以展示对应的值
    <Consumer>
      {name => (
        <div
          style={{
            border: "1px solid blue",
            width: "60%",
            margin: "20px auto",
            textAlign: "center"
          }}
        >
        // 在 Consumer 中可以直接通过 name 获取父组件的值
          <p>子组件。获取父组件的值:{name}</p>
        </div>
      )}
    </Consumer>
  );
}
export default Son;
~~~

## 2022/08/10分享

### axios请求取消

{% asset_img 1.png %}

{% asset_img 2.png %}

## 2022/08/11分享

Typtscript内置类型定义、泛型，可直接使用：

{% asset_img 3.png %}

更多内容：[可能是你需要的 React + TypeScript 50 条规范和经验 - 掘金 (juejin.cn)](https://juejin.cn/post/6844903849166110728)

PS：图中第三条Readonly的demo有错误（Todo=> iPeople）
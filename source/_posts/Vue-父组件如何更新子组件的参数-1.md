---
title: Vue - 父组件如何更新子组件的参数?
date: 2020-04-20 08:51:17
tags: 
- Vue
- 组件
---



### 方法1. 父组件更新子组件的prop参数

所有的 prop 都使得其父子 prop 之间形成了一个单向下行绑定：父级 prop 的更新会向下流动到子组件中，但是反过来则不行。这样会防止从子组件意外改变父级组件的状态，从而导致你的应用的数据流向难以理解。

额外的，每次父级组件发生更新时，子组件中所有的 prop 都将会刷新为最新的值。这意味着你不应该在一个子组件内部改变 prop。如果你这样做了，Vue 会在浏览器的控制台中发出警告。如果想在子组件中改变prop，可以参考官方解释[https://cn.vuejs.org/v2/guide/components...]([https://cn.vuejs.org/v2/guide/components-custom-events.html#sync-%E4%BF%AE%E9%A5%B0%E7%AC%A6](https://cn.vuejs.org/v2/guide/components-custom-events.html#sync-修饰符))

### 方法2. 父组件调用子组件的方法

1. 在子组件中定义函数 empty()

![image-20200417173318790](https://tva1.sinaimg.cn/large/007S8ZIlgy1gdzy5c3r3tj30jz0b6dgu.jpg)

1. 在父组件中的使用处添加ref  ref="upload"

![image-20200417173352552](https://tva1.sinaimg.cn/large/007S8ZIlgy1gdzy5cya5zj30gf083mxs.jpg)

1. 在需要的地方调用子组件中的函数 

```js
this.$refs.upload.empty();
```



![image-20200417173511471](https://tva1.sinaimg.cn/large/007S8ZIlgy1gdzy5b8vwbj30bo08y0tb.jpg)
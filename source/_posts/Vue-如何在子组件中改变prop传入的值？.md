---
title: Vue - 如何在子组件中改变prop传入的值？
date: 2020-04-20 09:04:04
tags:
- Vue
- sync
- prop
---



Vue - 如何在子组件中改变prop传入的值？



 我们都知道在vue中，父组件传入子组件的变量是存放在props属性中的，我们在调用变量的时候是跟data里面的变量一样的，都是通过this.变量来调用，但是如果想要在子组件中直接改变props中的属性浏览器会报错

如何解决这个问题呢？官方给出了一个方案(支持Vue2.3.0+)

![image-20200420092057528](https://tva1.sinaimg.cn/large/007S8ZIlgy1gdzyy9pn1yj30u00yqn6k.jpg)



参考：

[https://cn.vuejs.org/v2/guide/components...]([https://cn.vuejs.org/v2/guide/components-custom-events.html#sync-%E4%BF%AE%E9%A5%B0%E7%AC%A6](https://cn.vuejs.org/v2/guide/components-custom-events.html#sync-修饰符))
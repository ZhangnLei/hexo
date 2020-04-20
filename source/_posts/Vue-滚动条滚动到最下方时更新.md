---
title: Vue - 滚动条滚动到最下方时更新
date: 2020-04-18 17:38:13
tags: 
- Vue
---



`代码展示`

```js
watchScroll() {
  this.$nextTick(() => {
    const el = this.$refs["discussInfoBox"];
    const offsetHeight = el.offsetHeight;
    el.onscroll = () => {
      const scrollTop = el.scrollTop;
      const scrollHeight = el.scrollHeight;
      if (offsetHeight + scrollTop - scrollHeight >= -1) {
        // 需要执行的代码
        console.log("get info ");
      }
    };
  });
},
```



`使用步骤`

1. 第三行中的`discussInfoBox`为要监听的div的ID
2. 在第十行编写当滚动条滚动到最下方时需要调用的函数
3. 在需要的地方调用该函数。例如created方法或其他监听事件中



`原理解释`


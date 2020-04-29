---
title: 后端开发 - 发现一个SQL的新技能
date: 2020-04-28 12:40:36
tags: 
- SQL
---



>  不是发明创造，以前没见过这种用法，写下来记录一下。

## 起因

需要写一个添加根据用户`真实姓名`或`用户名`或`工号`模糊查询用户信息的接口

但是公司用了`shardingjdbc`且是较低版本，不支持用 OR关键字，短时间内不可能将组件升级。

## 怎么思路

使用concat() 函数

## 解决方案

```sql
concat( real_name, '*', user_name, '*', work_no ) LIKE concat('%',#{searchParam}, '%' )
```



哈哈，很简单，很神奇。


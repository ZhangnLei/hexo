---
title: LeetCode 350. 两个数组的交集 II
date: 2020-07-13 13:31:15
tags:
- LeetCode
---

[toc]

## 题目

[350. 两个数组的交集 II](https://leetcode-cn.com/problems/intersection-of-two-arrays-ii/)

难度简单326收藏分享切换为英文关注反馈

给定两个数组，编写一个函数来计算它们的交集。

 

**示例 1：**

```
输入：nums1 = [1,2,2,1], nums2 = [2,2]
输出：[2,2]
```

**示例 2:**

```
输入：nums1 = [4,9,5], nums2 = [9,4,9,8,4]
输出：[4,9]
```

 

**说明：**

- 输出结果中每个元素出现的次数，应与元素在两个数组中出现次数的最小值一致。
- 我们可以不考虑输出结果的顺序。

***\*进阶\**：**

- 如果给定的数组已经排好序呢？你将如何优化你的算法？
- 如果 *nums1* 的大小比 *nums2* 小很多，哪种方法更优？
- 如果 *nums2* 的元素存储在磁盘上，磁盘内存是有限的，并且你不能一次加载所有的元素到内存中，你该怎么办？

## 思路

`我的思路：`

维护两个hashMap，元素为key，出现的次数为value；最后遍历比较两个hashMap



`LeetCode官方提供的思路1：`

在我的思路上做了优化，只维护一个hashMap，遍历短的数组，生成hashMap，value增加；遍历第二个数组，取map中找是否存在元素，如存在则value-1，把key添加到结果中。很精妙！



可选优化：value=0时把key删掉，每次getKey前判断map是否有key



`LeetCode官方提供的思路2：`

先排序，然后使用两个指针做对比，两个指针指向的值相同时，记录元素，然后同时后移；两个指针指向的值不同时，数值小的指针往后移，任意一个数组完成后则停止。

## 编码

```java

```



更多详细代码见我的代码仓库

[https://github.com/ZhangnLei/java-base/tree/master/src/main/java/mrzhang/leecode](https://github.com/ZhangnLei/java-base/tree/master/src/main/java/mrzhang/leecode)
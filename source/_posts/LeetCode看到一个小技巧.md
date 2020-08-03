---
title: ' LeetCode看到一个小技巧'
date: 2020-08-03 10:16:09
tags:
---



很有趣，记录一下。

算法题中困难的地方就是面对复杂的情况，找出一个公共的方法

以下是一个题解中的代码片段：
```java
public static void functionName (int[] nums1, int[] nums2){
    int n1 = nums1.lenght;
    int n2 = nums2.lenght;
    if (n1 > n2){
        functionName(nums2, nums1);
    }
    ....
    // 算法代码
}
```
使用递归保证第一个数组的长度是较短的那一个。



巧妙，优雅，有意思。
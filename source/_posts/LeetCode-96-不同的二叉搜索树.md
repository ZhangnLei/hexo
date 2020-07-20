---
title: LeetCode 96. 不同的二叉搜索树
date: 2020-07-15 13:10:38
tags:
- LeetCode
- 二叉搜索树
- 公式法
- 卡特兰数
---

[toc]

## 题目

 [96. 不同的二叉搜索树](https://leetcode-cn.com/problems/unique-binary-search-trees/)

难度中等663收藏分享切换为英文关注反馈

给定一个整数 *n*，求以 1 ... *n* 为节点组成的二叉搜索树有多少种？

**示例:**

```
输入: 3
输出: 5
解释:
给定 n = 3, 一共有 5 种不同结构的二叉搜索树:

   1         3     3      2      1
    \       /     /      / \      \
     3     2     1      1   3      2
    /     /       \                 \
   2     1         2                 3
```

## 思路

设G(n)为n个节点组成二叉搜索树的个数，f(i)为以i为根节点二叉搜索树的个数
则有：G(n) = f(1) + f(2) + ... + f(n);
又因为i的左侧有i-1个节点，右侧有n-i个节点，
则有：f(i) = G(i-1) * G(n-i);
结合上述两式可得：
G(n) = G(0) * G(n-1) + G(1) * G(n-2) + ... + G(n-1) * G(0);

## 编码

```java
class Solution {
    public int numTrees(int n) {
        int[] dp = new int[n+1];
        dp[0] = 1;
        dp[1] = 1;
        
        for(int i = 2; i < n + 1; i++)
            for(int j = 1; j < i + 1; j++) 
                dp[i] += dp[j-1] * dp[i-j];
        
        return dp[n];
    }
}
```



更多详细代码见我的代码仓库

[https://github.com/ZhangnLei/java-base/tree/master/src/main/java/mrzhang/leecode](https://github.com/ZhangnLei/java-base/tree/master/src/main/java/mrzhang/leecode)
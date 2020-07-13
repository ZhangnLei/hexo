---
title: LeetCode 108. 有序数组转换二叉搜索树
date: 2020-07-11 11:48:43
tags:
- LeetCode
- 二叉搜索树
- 递归
---



[toc]

## 题目

#### [108. 将有序数组转换为二叉搜索树](https://leetcode-cn.com/problems/convert-sorted-array-to-binary-search-tree/)

将一个按照升序排列的有序数组，转换为一棵高度平衡二叉搜索树。

本题中，一个高度平衡二叉树是指一个二叉树*每个节点* 的左右两个子树的高度差的绝对值不超过 1。

**示例:**

```
给定有序数组: [-10,-3,0,5,9],

一个可能的答案是：[0,-3,9,-10,null,5]，它可以表示下面这个高度平衡二叉搜索树：

      0
     / \
   -3   9
   /   /
 -10  5
```

## 思路





## 编码

```java
package mrzhang.leecode;

/**
 * @author zhangnianlei
 * @date 2020/7/7
 * 108. 将有序数组转换为二叉搜索树
 */
public class Solution108 {

	
	public static TreeNode sortedArrayToBST(int[] nums) {
		return dfs(nums, 0, nums.length - 1);
	}

	/**
	 * @description 递归的构建一棵二叉搜索树
	 * @author zhangnianlei
	 * @date 2020/7/11
	 * @exception
	 * @param: nums
	 * @param: left
	 * @param: right
	 * @return: mrzhang.leecode.TreeNode
	 * @modifier
	 */
	private static TreeNode dfs(int[] nums, int left, int right) {
		if (left > right) {
			return null;
		}
		int mid = left + (right - left) / 2;
		TreeNode root = new TreeNode(nums[mid]);
		root.left = dfs(nums, left, mid - 1);
		root.right = dfs(nums, mid + 1, right);
		return root;
	}


	/**
	 * @description 编写一个main函数在本地检验
	 * @author zhangnianlei
	 * @date 2020/7/11
	 * @exception
	 * @param: args
	 * @modifier
	 */
	public static void main(String[] args) {
		int[] nums = {-10,-3,0,5,9};
		TreeNode root = sortedArrayToBST(nums);
		TreeNode.prePrint(root);
	}

}
```



更多详细代码见我的代码仓库

[https://github.com/ZhangnLei/java-base/tree/master/src/main/java/mrzhang/leecode](https://github.com/ZhangnLei/java-base/tree/master/src/main/java/mrzhang/leecode)
---
author: "volyx"
title:  "110. Balanced Binary Tree"
date: "2021-03-13"
# description: "Sample article showcasing basic Markdown syntax and formatting for HTML elements."
tags:  ["leetcode", "easy", "binary-tree"]
categories: ["leetcode"]
# series: ["Themes Guide"]
# aliases: ["migrate-from-jekyl"]
# ShowToc: true
# TocOpen: true
# weight: 2
---

[110. Balanced Binary Tree](https://leetcode.com/problems/balanced-binary-tree/)

Given a binary tree, determine if it is height-balanced.

For this problem, a height-balanced binary tree is defined as:

> a binary tree in which the left and right subtrees of every node differ in height by no more than 1.

```txt
Example 1:

Input: root = [3,9,20,null,null,15,7]
Output: true
```

![ex1](/images/2021-03-13-balanced-binary-tree-ex1.jpg)

```txt
Example 2:

Input: root = [1,2,2,3,3,null,null,4,4]
Output: false
```

![ex1](/images/2021-03-13-balanced-binary-tree-ex1.jpg)

```txt
Example 3:

Input: root = []
Output: true
```

Constraints:

- The number of nodes in the tree is in the range [0, 5000].
- -104 <= Node.val <= 104



```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution {
    public TreeNode sortedArrayToBST(int[] nums) {
        if (nums.length == 0) return null;
        return buildBST(nums, 0, nums.length - 1);
    }
    
    TreeNode buildBST(int[] nums, int lo, int hi) {
        if (hi < lo) {
            return null;
        }
        TreeNode node = new TreeNode();
        int mid = lo +  (hi  - lo) / 2;
        node.val = nums[mid];
        node.left = buildBST(nums, lo, mid - 1);
        node.right = buildBST(nums, mid + 1, hi);
        return node;
    }
}
```

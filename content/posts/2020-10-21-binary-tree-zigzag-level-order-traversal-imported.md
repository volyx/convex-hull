---
author: "volyx"
title:  "Binary Tree Zigzag Level Order Traversal"
date: "Wed Oct 21 00:00:00 MSK 2020"
# description: "Sample article showcasing basic Markdown syntax and formatting for HTML elements."
tags:  ["leetcode", "medium"]
categories: ["leetcode"]
# series: ["Themes Guide"]
# aliases: ["migrate-from-jekyl"]
# ShowToc: true
# TocOpen: true
# weight: 2
---

Given a binary tree, return the zigzag level order traversal of its nodes' values. (ie, from left to right, then right to left for the next level and alternate between).

For example:
Given binary tree [3,9,20,null,null,15,7],

```txt
    3
   / \
  9  20
    /  \
   15   7
```

return its zigzag level order traversal as:

```txt
[
  [3],
  [20,9],
  [15,7]
]
```

Solution:

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
    public List<List<Integer>> zigzagLevelOrder(TreeNode root) {
        List<List<Integer>> result = new ArrayList<>();
        dfs(root, result, 0);
        return result;
    }

    void dfs(TreeNode node, List<List<Integer>> result, int level) {

        if (node == null) {
            return;
        }

        checkSize(result, level);

        if (level % 2 == 1) {
           result.get(level).add(0, node.val);
        } else {
            result.get(level).add(node.val);
        }

        dfs(node.left, result, level + 1);
        dfs(node.right, result, level + 1);
    }

    void checkSize(List<List<Integer>> result, int level) {
        // 0 [ [] ]
        // 1 [[][]]
        // 2 [ [][] ]
        if (result.size() <= level) {
            result.add(new ArrayList<>());
        }
    }
}

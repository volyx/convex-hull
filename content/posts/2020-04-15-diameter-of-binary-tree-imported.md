---
author: "volyx"
title:  "Diameter of Binary Tree"
date: "2020-04-15"
# description: "Sample article showcasing basic Markdown syntax and formatting for HTML elements."
tags:  ["leetcode", "easy", "mock"]
categories: ["leetcode"]
# series: ["Themes Guide"]
# aliases: ["migrate-from-jekyl"]
# ShowToc: true
# TocOpen: true
# weight: 2
---

Given a binary tree, you need to compute the length of the diameter of the tree. The diameter of a binary tree is the length of the longest path between any two nodes in a tree. This path may or may not pass through the root.

Example:
Given a binary tree

```txt
          1
         / \
        2   3
       / \
      4   5
```

Return 3, which is the length of the path [4,2,1,3] or [5,2,1,3].

Note: The length of path between two nodes is represented by the number of edges between them. 

```txt
{3,4}     1
         / \
{2,2}   2   3{0,1}
       / \
{0,1} 4   5{0,1}
```


```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {

    Node dfs(TreeNode root) {
        if (root == null) {
            return new Node();
        }
        Node left = dfs(root.left);
        Node right = dfs(root.right);
        // diametr, depth
        int diam = Math.max(Math.max(left.diametr, right.diametr), left.depth + right.depth);

        return new Node(diam, 1 + Math.max(left.depth, right.depth));
    }

    public int diameterOfBinaryTree(TreeNode root) {
      return dfs(root).diametr;
    }

    class Node {
        Node() {}

        Node(int diametr, int depth) {
            this.diametr = diametr;
            this.depth = depth;
        }
        public int diametr;
        public int depth;
    }
}

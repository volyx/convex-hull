---
author: "volyx"
title:  "Lowest Common Ancestor of a Binary Tree"
date: "2020-11-12"
# description: "Sample article showcasing basic Markdown syntax and formatting for HTML elements."
tags:  ["leetcode", "medium"]
categories: ["leetcode"]
# series: ["Themes Guide"]
# aliases: ["migrate-from-jekyl"]
# ShowToc: true
# TocOpen: true
# weight: 2
---

Given a binary tree, find the lowest common ancestor (LCA) of two given nodes in the tree.

According to the definition of LCA on Wikipedia: “The lowest common ancestor is defined between two nodes p and q as the lowest node in T that has both p and q as descendants (where we allow a node to be a descendant of itself).”

 

Example 1:

Input: root = [3,5,1,6,2,0,8,null,null,7,4], p = 5, q = 1
Output: 3
Explanation: The LCA of nodes 5 and 1 is 3.


![ex1](/images/2020-11-12-ex1.png)

Example 2:

Input: root = [3,5,1,6,2,0,8,null,null,7,4], p = 5, q = 4
Output: 5
Explanation: The LCA of nodes 5 and 4 is 5, since a node can be a descendant of itself according to the LCA definition.

![ex2](/images/2020-11-12-ex2.png)

Example 3:

Input: root = [1,2], p = 1, q = 2
Output: 1

Constraints:

- The number of nodes in the tree is in the range [2, 105].
- -109 <= Node.val <= 109
- All Node.val are unique.
- p != q
- p and q will exist in the tree.

Solution:

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
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        
        List<TreeNode> parentNodes1 = new ArrayList();
        List<TreeNode> parentNodes2 = new ArrayList();
        
        search(root, p, parentNodes1);
        search(root, q, parentNodes2);
        
        int n = Math.min(parentNodes1.size(), parentNodes2.size());
        TreeNode lca = root;
        for (int i = 1; i < n; i++) {
            if (parentNodes1.get(i).val == parentNodes2.get(i).val) {
                lca = parentNodes1.get(i);
            } else {
                break;
            }
        }
        return lca;

    }
    
    boolean search(TreeNode current, TreeNode target, List<TreeNode> path) {
        if (current == null) return false;
        
        path.add(current);
             
        if (current.val == target.val) {
            return true;
        }
        
        if (search(current.left, target, path)) {
            return true;
        }
        
        if (search(current.right, target, path)) {
            return true;
        }
        
        path.remove(path.size() - 1);
        
        return false;
    }
}

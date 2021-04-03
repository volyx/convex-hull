---
author: "volyx"
title:  "872. Leaf-Similar Trees"
date: "2021-04-03"
# description: "Sample article showcasing basic Markdown syntax and formatting for HTML elements."
tags:  ["leetcode", "easy", "tree", "dfs"]
categories: ["leetcode"]
# series: ["Themes Guide"]
# aliases: ["migrate-from-jekyl"]
# ShowToc: true
# TocOpen: true
# weight: 2
---

[872. Leaf-Similar Trees](https://leetcode.com/problems/leaf-similar-trees/)

Consider all the leaves of a binary tree, from left to right order, the values of those leaves form a leaf value sequence.

For example, in the given tree above, the leaf value sequence is (6, 7, 4, 9, 8).

Two binary trees are considered leaf-similar if their leaf value sequence is the same.

Return true if and only if the two given trees with head nodes root1 and root2 are leaf-similar.

```txt
Example 1:

Input: root1 = [3,5,1,6,2,9,8,null,null,7,4], root2 = [3,5,1,6,7,4,2,null,null,null,null,null,null,9,8]
Output: true
```

![ex1](/images/2021-04-03-ex1.png)

```txt
Example 2:

Input: root1 = [1], root2 = [1]
Output: true
```

![ex2](/images/2021-04-03-ex2.png)

```txt
Example 3:

Input: root1 = [1], root2 = [2]
Output: false
```

![ex2](/images/2021-04-03-ex2.png)

```txt
Example 4:

Input: root1 = [1,2], root2 = [2,2]
Output: true
```

```txt
Example 5:

Input: root1 = [1,2,3], root2 = [1,3,2]
Output: false
```

![ex5](/images/2021-04-03-ex5.png)

Constraints:

- The number of nodes in each tree will be in the range [1, 200].
- Both of the given trees will have values in the range [0, 200].

## Solution

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
    public boolean leafSimilar(TreeNode root1, TreeNode root2) {
        List<Integer> leaves1 = new ArrayList<>();
        List<Integer> leaves2 = new ArrayList<>();
        
        visit(root1, leaves1);
        visit(root2, leaves2);
        
        if (leaves1.size() != leaves2.size()) return false;
        
        for (int i = 0; i < leaves1.size(); i++) {
            if (!leaves1.get(i).equals(leaves2.get(i))) {
                return false;
            }
        }
        return true;
    }
    
    void visit(TreeNode node, List<Integer> leaves) {
        if (node == null) return;
        
        if (node.left == null && node.right == null) {
            leaves.add(node.val);
        } else {
            visit(node.left, leaves);
            visit(node.right, leaves);
        }
    }
}
```

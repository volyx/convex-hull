---
author: "volyx"
title:  "31. Next Permutation"
date: "2021-06-13"
# description: "Sample article showcasing basic Markdown syntax and formatting for HTML elements."
tags:  ["leetcode", "medium", "backtracking"]
categories: ["leetcode"]
# series: ["Themes Guide"]
# aliases: ["migrate-from-jekyl"]
# ShowToc: true
# TocOpen: true
# weight: 2
---

[31. Next Permutation](https://leetcode.com/problems/next-permutation/)

Implement next permutation, which rearranges numbers into the lexicographically next greater permutation of numbers.

If such an arrangement is not possible, it must rearrange it as the lowest possible order (i.e., sorted in ascending order).

The replacement must be in place and use only constant extra memory.

```txt
Example 1:

Input: nums = [1,2,3]
Output: [1,3,2]

Example 2:

Input: nums = [3,2,1]
Output: [1,2,3]

Example 3:

Input: nums = [1,1,5]
Output: [1,5,1]

Example 4:

Input: nums = [1]
Output: [1]
```

Constraints:

- 1 <= nums.length <= 100
- 0 <= nums[i] <= 100

## Solution

```java
class Solution {
    public void nextPermutation(int[] nums) {
        int i = nums.length - 2;
        // [2,3,1,3,3]
        // i = 2
        while (i >= 0 && nums[i + 1] <= nums[i]) {
            i--;
        }
        
        if (i >= 0) {
            int j = nums.length - 1;
            while (nums[j] <= nums[i]) {
                j--;
            }
            swap(nums, i, j);
        }
        reverse(nums, i + 1);
    }
    
    void swap(int[] nums, int i, int j) {
        int temp = nums[i];
        nums[i] = nums[j];
        nums[j] = temp;
    }
        
    void reverse(int[] nums, int start) {
        int i = start;
        int j = nums.length - 1;
        
        
        while (i < j) {
            // System.out.println("reverse " + i + " " + j);
            swap(nums, i, j);
            i++;
            j--;
        }
    }
}
```

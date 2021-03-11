---
author: "volyx"
title:  "Longest Continuous Increasing Subsequence"
date: "2020-06-23"
# description: "Sample article showcasing basic Markdown syntax and formatting for HTML elements."
tags:  ["leetcode", "easy"]
categories: ["leetcode"]
# series: ["Themes Guide"]
# aliases: ["migrate-from-jekyl"]
# ShowToc: true
# TocOpen: true
# weight: 2
---

Given an unsorted array of integers, find the length of longest continuous increasing subsequence (subarray).

Example 1:
```
Input: [1,3,5,4,7]
Output: 3
Explanation: The longest continuous increasing subsequence is [1,3,5], its length is 3. 
Even though [1,3,5,7] is also an increasing subsequence, it's not a continuous one where 5 and 7 are separated by 4. 
```

Example 2:
```
Input: [2,2,2,2,2]
Output: 1
Explanation: The longest continuous increasing subsequence is [2], its length is 1. 
```

Note: Length of the array will not exceed 10,000. 

Solution:

```java
class Solution {
    public int findLengthOfLCIS(int[] nums) {
            int ans = 0;
        int anchor = 0;
        
        for (int i = 0; i < nums.length; i++) {
            if (i > 0 && nums[i - 1] >= nums[i]) anchor = i;
            
            ans = Math.max(ans, i - anchor + 1);
            System.out.printf("i %d anchor %d %n", i, anchor);
        }
        
        return ans;
        
    }
}


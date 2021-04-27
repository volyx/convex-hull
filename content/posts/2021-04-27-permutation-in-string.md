---
author: "volyx"
title:  "567. Permutation in String"
date: "2021-04-27"
# description: "Sample article showcasing basic Markdown syntax and formatting for HTML elements."
tags:  ["leetcode", "medium", "string"]
categories: ["leetcode"]
# series: ["Themes Guide"]
# aliases: ["migrate-from-jekyl"]
# ShowToc: true
# TocOpen: true
# weight: 2
---

[567. Permutation in String](https://leetcode.com/problems/permutation-in-string/)

Given two strings s1 and s2, write a function to return true if s2 contains the permutation of s1. In other words, one of the first string's permutations is the substring of the second string.

```txt
Example 1:

Input: s1 = "ab" s2 = "eidbaooo"
Output: True
Explanation: s2 contains one permutation of s1 ("ba").
```

```txt
Example 2:

Input:s1= "ab" s2 = "eidboaoo"
Output: False
```

Constraints:

- The input strings only contain lower case letters.
- The length of both given strings is in range [1, 10,000].

## Solution

```java
class Solution {
    public boolean checkInclusion(String s1, String s2) {
        int len1 = s1.length();
        int len2 = s2.length();
        
        int[] count1 = new int[256];
        int[] count2 = new int[256];
        for (int i = 0; i < len1; i++) {
            count1[s1.charAt(i)]++;
        }
        for (int i = 0; i < len2; i++) {
            count2[s2.charAt(i)]++;
            if (i >= len1) {
                count2[s2.charAt(i - len1)]--;
            }
            if (Arrays.equals(count1, count2)) {
                return true;
            }
        }
        return false;
    }
}
```

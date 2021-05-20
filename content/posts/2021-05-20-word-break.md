---
author: "volyx"
title:  "139. Word Break"
date: "2021-05-20"
# description: "Sample article showcasing basic Markdown syntax and formatting for HTML elements."
tags:  ["leetcode", "medium", "linked-list"]
categories: ["leetcode"]
# series: ["Themes Guide"]
# aliases: ["migrate-from-jekyl"]
# ShowToc: true
# TocOpen: true
# weight: 2
---

[139. Word Break](https://leetcode.com/problems/word-break/)

Given a string s and a dictionary of strings wordDict, return true if s can be segmented into a space-separated sequence of one or more dictionary words.

Note that the same word in the dictionary may be reused multiple times in the segmentation.

```txt
Example 1:

Input: s = "leetcode", wordDict = ["leet","code"]
Output: true
Explanation: Return true because "leetcode" can be segmented as "leet code".

Example 2:

Input: s = "applepenapple", wordDict = ["apple","pen"]
Output: true
Explanation: Return true because "applepenapple" can be segmented as "apple pen apple".
Note that you are allowed to reuse a dictionary word.

Example 3:

Input: s = "catsandog", wordDict = ["cats","dog","sand","and","cat"]
Output: false
```

Constraints:

- 1 <= s.length <= 300
- 1 <= wordDict.length <= 1000
- 1 <= wordDict[i].length <= 20
- s and wordDict[i] consist of only lowercase English letters.
- All the strings of wordDict are unique.

## Solution

```java
class Solution {
    public boolean wordBreak2(String s, List<String> wordDict) {
        Map<String, Boolean> memo = new HashMap<>();
        return search(s, wordDict, memo);
    }
    
    private boolean search(String s, 
                           List<String> wordDict, 
                           Map<String, Boolean> memo ) {
        
        if (s.length() == 0) {
            return true;
        }
        for (String key: wordDict) {
            if (s.startsWith(key)) {
                boolean find;
                String substr = s.substring(key.length(), s.length());
                if (memo.containsKey(substr)) {
                    find = memo.get(substr);
                } else {
                    find = search(substr, wordDict, memo);
                }
                memo.put(substr, find);
                if (find) return true;
            }
        }
        return false;
    }
    
    public boolean wordBreak(String s, List<String> wordDict) {
        boolean[] dp = new boolean[s.length() + 1];
        dp[0] = true;
        for (int i = 1; i < s.length() + 1; i++) {
            for (int j = 0; j < i; j++) {
                if (dp[j] && wordDict.indexOf(s.substring(j, i)) >=0 ) {
                    dp[i] = true;
                    break;
                }
            }
        }
        System.out.println(Arrays.toString(dp));
        return dp[s.length()];
    }
}
```

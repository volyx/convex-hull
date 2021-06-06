---
author: "volyx"
title:  "301. Remove Invalid Parentheses"
date: "2021-06-06"
# description: "Sample article showcasing basic Markdown syntax and formatting for HTML elements."
tags:  ["leetcode", "hard", "backtracking"]
categories: ["leetcode"]
# series: ["Themes Guide"]
# aliases: ["migrate-from-jekyl"]
# ShowToc: true
# TocOpen: true
# weight: 2
---

[301. Remove Invalid Parentheses](https://leetcode.com/problems/remove-invalid-parentheses)

Given a string s that contains parentheses and letters, remove the minimum number of invalid parentheses to make the input string valid.

Return all the possible results. You may return the answer in any order.

```txt
Example 1:

Input: s = "()())()"
Output: ["(())()","()()()"]

Example 2:

Input: s = "(a)())()"
Output: ["(a())()","(a)()()"]

Example 3:

Input: s = ")("
Output: [""]
```

Constraints:

- 1 <= s.length <= 25
- s consists of lowercase English letters and parentheses '(' and ')'.
- There will be at most 20 parentheses in s.

## Solution

```java
class Solution {
    public List<String> removeInvalidParentheses(String s) {
        TreeMap<Integer, Set<String>> res = new TreeMap<>();
        
        back(0, s, "", res, 0, 0);
        
        return new ArrayList<>(res.firstEntry().getValue());
    }
    
    void back(int index, String s, String current, 
              Map<Integer, Set<String>> res,
              int open, int closed) {
        
        if (index == s.length()) {
            if (open == closed) {
                int removed = s.length() - current.length();
                Set<String> values = res.getOrDefault(removed, new TreeSet<>());                       values.add(current);  
                res.put(removed, values);
            }
            return;
        }
        
        if (closed > open) return;
        
        char c = s.charAt(index);
        
        if (c == '(' || c == ')') {
            back(index + 1, s, current + c, res,
                 (c == '(') ? open + 1: open, (c == ')') ? closed + 1: closed);
            
            back(index + 1, s, current, res, open, closed);
            
        } else {
            back(index + 1, s, current + c, res, open, closed);
        }   
    }
}
```

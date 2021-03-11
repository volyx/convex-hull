---
author: "volyx"
title:  "Verifying an Alien Dictionary"
date: "2020-06-23"
# description: "Sample article showcasing basic Markdown syntax and formatting for HTML elements."
tags:  ["leetcode", "easy", "2times"]
categories: ["leetcode"]
# series: ["Themes Guide"]
# aliases: ["migrate-from-jekyl"]
# ShowToc: true
# TocOpen: true
# weight: 2
---

In an alien language, surprisingly they also use english lowercase letters, but possibly in a different order. The order of the alphabet is some permutation of lowercase letters.

Given a sequence of words written in the alien language, and the order of the alphabet, return true if and only if the given words are sorted lexicographicaly in this alien language.

Example 1:

```
Input: words = ["hello","leetcode"], order = "hlabcdefgijkmnopqrstuvwxyz"
Output: true
Explanation: As 'h' comes before 'l' in this language, then the sequence is sorted.
```

Example 2:

```
Input: words = ["word","world","row"], order = "worldabcefghijkmnpqstuvxyz"
Output: false
Explanation: As 'd' comes after 'l' in this language, then words[0] > words[1], hence the sequence is unsorted.
```

Example 3:

```
Input: words = ["apple","app"], order = "abcdefghijklmnopqrstuvwxyz"
Output: false
Explanation: The first three characters "app" match, and the second string is shorter (in size.) According to lexicographical rules "apple" > "app", because 'l' > '∅', where '∅' is defined as the blank character which is less than any other character (More info).
```

Solution:

```java
class Solution {
    public boolean isAlienSorted(String[] words, String order) {
        if (words.length == 0) {
            return true;
        }
        if (words.length == 1) {
            return true;
        }

        Map<Character, Integer> alphabet = new HashMap<>();
        for (int i = 0; i < order.length(); i++) {
            alphabet.put(Character.valueOf(order.charAt(i)), i); // 012
        }

        String prev = words[0]; // ac // b

        for (int i = 1; i < words.length; i++) {
            String current = words[i]; // b
            if (!isSorted(prev, current, alphabet)) {
                return false;
            }
            prev = current;
        }
        return true;
    }
    boolean isSorted(String a, String b, Map<Character, Integer> alphabet) {
        for (int i = 0; i < Math.min(a.length(), b.length()); i++) {
            char c1 = a.charAt(i); // a
            char c2 = b.charAt(i); // b

            int index1 = alphabet.get(Character.valueOf(c1)); // 0
            int index2 = alphabet.get(Character.valueOf(c2)); // 1
            // System.out.println(c1 +" " + c2 + " " + index1 + " < " + index2);
            if (index1 < index2) {
                return true;
            } else if (index1 == index2) {
                continue;
            } else {
                return false;
            }
        } // for
        return a.length() <= b.length();
    }

}

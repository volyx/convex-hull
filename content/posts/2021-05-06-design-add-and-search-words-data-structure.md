---
author: "volyx"
title:  "211. Design Add and Search Words Data Structure"
date: "2021-05-06"
# description: "Sample article showcasing basic Markdown syntax and formatting for HTML elements."
tags:  ["leetcode", "medium", "string", "trie"]
categories: ["leetcode"]
# series: ["Themes Guide"]
# aliases: ["migrate-from-jekyl"]
# ShowToc: true
# TocOpen: true
# weight: 2
---

[211. Design Add and Search Words Data Structure](https://leetcode.com/problems/design-add-and-search-words-data-structure/)

Design a data structure that supports adding new words and finding if a string matches any previously added string.

Implement the WordDictionary class:

- WordDictionary() Initializes the object.
- void addWord(word) Adds word to the data structure, it can be matched later.
- bool search(word) Returns true if there is any string in the data structure that - matches word or false otherwise. word may contain dots '.' where dots can be matched with any letter.

```txt
Example:

Input
["WordDictionary","addWord","addWord","addWord","search","search","search","search"]
[[],["bad"],["dad"],["mad"],["pad"],["bad"],[".ad"],["b.."]]
Output
[null,null,null,null,false,true,true,true]

Explanation
WordDictionary wordDictionary = new WordDictionary();
wordDictionary.addWord("bad");
wordDictionary.addWord("dad");
wordDictionary.addWord("mad");
wordDictionary.search("pad"); // return False
wordDictionary.search("bad"); // return True
wordDictionary.search(".ad"); // return True
wordDictionary.search("b.."); // return True
```

Constraints:

- 1 <= word.length <= 500
- word in addWord consists lower-case English letters.
- word in search consist of  '.' or lower-case English letters.
- At most 50000 calls will be made to addWord and search.

## Solution

```java
class WordDictionary {
    static int R = 256;
    Trie trie = new Trie(); 

    /** Initialize your data structure here. */
    public WordDictionary() {
        
    }
    
    public void addWord(String word) {
        Trie node = trie;
        for (char c: word.toCharArray()) {
            Trie curr = node.next[c];
            if (curr == null) {
                curr = new Trie();
            }
            node.next[c] = curr;
            node = curr;
        }
        node.isWord = true;
    }
    
    public boolean search(String word) {
        return patternSearch(word, trie, 0);
    }
    
    boolean patternSearch(String word, Trie node, int index) {
         if (node == null) return false;
         if (index == word.length()) return node.isWord;
         char c = word.charAt(index);             
         if (c == '.') {
             for (Trie t: node.next) {
                 if (patternSearch(word, t, index + 1)) return true;
             }
         } else {
            if (patternSearch(word, node.next[c], index + 1)) return true;
         }        
         return false;
    }
    
    class Trie {
        Trie[] next = new Trie[R];
        boolean isWord;
    }    
}

/**
 * Your WordDictionary object will be instantiated and called as such:
 * WordDictionary obj = new WordDictionary();
 * obj.addWord(word);
 * boolean param_2 = obj.search(word);
 */
```

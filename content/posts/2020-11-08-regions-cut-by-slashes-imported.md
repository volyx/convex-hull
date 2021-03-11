---
author: "volyx"
title:  "Regions Cut By Slashes"
date: "2020-11-08"
# description: "Sample article showcasing basic Markdown syntax and formatting for HTML elements."
tags:  ["leetcode", "medium"]
categories: ["leetcode"]
# series: ["Themes Guide"]
# aliases: ["migrate-from-jekyl"]
# ShowToc: true
# TocOpen: true
# weight: 2
---

![https://leetcode.com/problems/regions-cut-by-slashes/]

n a N x N grid composed of 1 x 1 squares, each 1 x 1 square consists of a /, \, or blank space.  These characters divide the square into contiguous regions.

(Note that backslash characters are escaped, so a \ is represented as "\\".)

Return the number of regions.

Example 1:

```txt
Input:
[
  " /",
  "/ "
]
Output: 2
Explanation: The 2x2 grid is as follows:
```

![ex1](/images/2020-11-08-ex1.png)

Example 2:

```txt
Input:
[
  " /",
  "  "
]
Output: 1
Explanation: The 2x2 grid is as follows:
```

![ex2](/images/2020-11-08-ex2.png)

Example 3:

```txt
Input:
[
  "\\/",
  "/\\"
]
Output: 4
Explanation: (Recall that because \ characters are escaped, "\\/" refers to \/, and "/\\" refers to /\.)
```

The 2x2 grid is as follows:

![ex3](/images/2020-11-08-ex3.png)

Example 4:

```txt
Input:
[
  "/\\",
  "\\/"
]
Output: 5
Explanation: (Recall that because \ characters are escaped, "/\\" refers to /\, and "\\/" refers to \/.)
The 2x2 grid is as follows:
```

![ex4](/images/2020-11-08-ex4.png)

Example 5:

```txt
Input:
[
  "//",
  "/ "
]
Output: 3
Explanation: The 2x2 grid is as follows:
```

![ex5](/images/2020-11-08-ex5.png)

Note:

- 1 <= grid.length == grid[0].length <= 30
- grid[i][j] is either '/', '\', or ' '.

Solution:

```java
class Solution {
    public int regionsBySlashes(String[] input) {
        int N = input.length;
        int[][] matrix = new int[3 * N][3 * N];

        for (int i = 0; i < N; i++) {
            for (int j = 0; j < N; j++) {
                if (input[i].charAt(j) == '/') {
                    fillForwardSlash(matrix, i, j);
                } else if (input[i].charAt(j) == ' ') {

                } else {
                    fillBackwardSlash(matrix, i, j);
                }
            }
        }
        int count = 0;
        for (int i = 0; i < matrix.length; i++) {
            for (int j = 0; j < matrix.length; j++) {
                if (matrix[i][j] == 0) {
                    count++;
                    fill(matrix, i, j);
                }
            }
        }
        return count;
    }

    int[][] dirs = new int[][] {{1,0}, {0, 1}, {-1, 0}, {0, -1}};

    void fill(int[][] matrix, int i, int j) {
        if (i < 0 || i == matrix.length || j < 0 || j == matrix.length || matrix[i][j] == 1) return;

        matrix[i][j] = 1;

        for(var dir : dirs) {
            fill(matrix, i + dir[0], j + dir[1]);
        }
    }

    void fillForwardSlash(int[][] m, int row, int col) {
        m[3 * row + 2][3 * col] = 1;
        m[3 * row + 1][3 * col + 1] = 1;
        m[3 * row][3 * col + 2] = 1;
    }

    void fillBackwardSlash(int[][] m, int row, int col) {
        m[3 * row][3 * col] = 1;
        m[3 * row + 1][3 * col + 1] = 1;
        m[3 * row + 2][3 * col + 2] = 1;
    }

}

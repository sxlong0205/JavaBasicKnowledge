---
zmathjax: true
toc: true
categories:
 - LeetCode
tags:
 - 刷题笔记
---

#### [剑指 Offer 12. 矩阵中的路径](https://leetcode-cn.com/problems/ju-zhen-zhong-de-lu-jing-lcof/)

请设计一个函数，用来判断在一个矩阵中是否存在一条包含某字符串所有字符的路径。路径可以从矩阵中的任意一格开始，每一步可以在矩阵中向左、右、上、下移动一格。如果一条路径经过了矩阵的某一格，那么该路径不能再次进入该格子。例如，在下面的3×4的矩阵中包含一条字符串“bfce”的路径（路径中的字母用加粗标出）。

<!--more-->

[["a","b","c","e"],
["s","f","c","s"],
["a","d","e","e"]]

但矩阵中不包含字符串“abfb”的路径，因为字符串的第一个字符b占据了矩阵中的第一行第二个格子之后，路径不能再次进入这个格子。

**示例1 ：**

```
输入：board = [["A","B","C","E"],["S","F","C","S"],["A","D","E","E"]], word = "ABCCED"
输出：true
```

**示例2:**

```
输入：board = [["a","b"],["c","d"]], word = "abcd"
输出：false
```

**限制：**

-   `1 <= board.length <= 200`
-   `1 <= board[i].length <= 200`

来源：力扣（LeetCode）
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

### 题解：

本题一看是在二维数组中寻找一条符合条件的路径，最先想到的就是深度优先搜索遍历。具体来说，就是从一个点开始遍历，分别向上、下、左、右发散遍历，如果找到符合条件的字符串，则返回`true`，否则返回`false`。

具体代码如下：

```java
class Solution {
    public boolean exist(char[][] board, String word) {
        for (int i = 0; i < board.length; i++) {
            for (int j = 0; j < board[0].length; j++) {
                if (board[i][j] == word.charAt(0) && dfs(board, word, i, j, 0))
                    return true;
            }
        }
        return false;
    }

    private boolean dfs(char[][] board, String word, int i, int j, int start) {
      	//边界条件，如果索引越界或者当前位置不满足条件，则返回false
        if (i >= board.length || i < 0 || j >= board[0].length || j < 0 || board[i][j] != word.charAt(start))
            return false;

      	//已经找到满足条件的字符串
        if (start == word.length() - 1)
            return true;

      	//这里可以减少创建标记数组的开销，直接在搜索之前先将当前位置置为符号，递归后再恢复
        char temp = board[i][j];
        board[i][j] = '$';
        boolean result = dfs(board, word, i - 1, j, start + 1) || dfs(board, word, i + 1, j, start + 1)
                || dfs(board, word, i, j - 1, start + 1) || dfs(board, word, i, j + 1, start + 1);
        board[i][j] = temp;
        return result;
    }
}
```


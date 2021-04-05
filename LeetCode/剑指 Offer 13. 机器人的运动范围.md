---
zmathjax: true
toc: true
categories:
 - LeetCode
tags:
 - 刷题笔记
---

#### [剑指 Offer 13. 机器人的运动范围](https://leetcode-cn.com/problems/ji-qi-ren-de-yun-dong-fan-wei-lcof/)

地上有一个`m`行`n`列的方格，从坐标 `[0,0]` 到坐标 `[m-1,n-1]` 。一个机器人从坐标 `[0, 0]` 的格子开始移动，它每次可以向左、右、上、下移动一格（不能移动到方格外），也不能进入行坐标和列坐标的数位之和大于`k`的格子。例如，当`k`为`18`时，机器人能够进入方格 `[35, 37 `，因为`3+5+3+7=18`。但它不能进入方格 `[35, 38]`，因为`3+5+3+8=19`。请问该机器人能够到达多少个格子？

<!--more-->

**示例 1：**

```
输入：m = 2, n = 3, k = 1
输出：3
```

**示例 2：**

```
输入：m = 3, n = 1, k = 0
输出：1
```

**提示：**

- `1 <= n,m <= 100`
- `0 <= k <= 20`

来源：力扣（LeetCode）
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。

### 题解：

一看到在矩形棋盘中的路径，首先想到`DFS`，因为这里只给了长和宽，没办法用特殊符号标记，所以没有办法省略`visited`数组。计算行坐标和列坐标的数位之和很简单，就是取模将各个位上的数字相加即可。由于采用递归地方式进行遍历，所以只需要考虑向右，向下走的情况即可，如果向上或者向左走，就会产生路径重复。我们DFS需要返回的结果就是当前位置(`1`)加上向右遍历和向下遍历的结果之和。

具体代码如下：

```java
class Solution {
    public int movingCount(int m, int n, int k) {
        //创建标记数组
        boolean[][] visited = new boolean[m][n];
        return dfs(0, 0, m, n, k, 0, visited);
    }

    private int dfs(int i, int j, int m, int n, int k, int count, boolean[][] visited) {
        //如果越界，或者行和列和大于k，或者已经被访问过，那么直接返回0
        if (i >= m || j >= n || visited[i][j] || k < sum(i, j))
            return 0;

        //将当前位置标记为已经访问过
        visited[i][j] = true;

        //向右向下遍历
        int right = dfs(i, j + 1, m, n, k, count + 1, visited);
        int down = dfs(i + 1, j, m, n, k, count + 1, visited);

        //返回结果
        return right + down + 1;
    }


    //计算行坐标和列坐标的数位之和
    private int sum(int m, int n) {
        int result = 0;
        while (m != 0) {
            result += m % 10;
            m /= 10;
        }
        while (n != 0) {
            result += n % 10;
            n /= 10;
        }
        return result;
    }
}
```


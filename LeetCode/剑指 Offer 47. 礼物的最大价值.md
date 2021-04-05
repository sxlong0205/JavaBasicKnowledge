---
zmathjax: true
toc: true
categories:
 - LeetCode
tags:
 - 刷题笔记
---

#### [剑指 Offer 47. 礼物的最大价值](https://leetcode-cn.com/problems/li-wu-de-zui-da-jie-zhi-lcof/)

在一个 `m*n` 的棋盘的每一格都放有一个礼物，每个礼物都有一定的价值（价值大于 0）。你可以从棋盘的左上角开始拿格子里的礼物，并每次向右或者向下移动一格、直到到达棋盘的右下角。给定一个棋盘及其上面的礼物的价值，请计算你最多能拿到多少价值的礼物？

<!--more-->

**示例1：**

```
输入: 
[
  [1,3,1],
  [1,5,1],
  [4,2,1]
]
输出: 12
解释: 路径 1→3→5→2→1 可以拿到最多价值的礼物
```

提示：

- `0 < grid.length <= 200`
- `0 < grid[0].length <= 200`

来源：力扣（LeetCode）
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

### 题解：

本题有两种解法，一种是动态规划，一种是深度优先搜索遍历。对于动态规划，在当前位置的最大值，取决于该位置的上边和右边的值中较大的值，加上当前位置上的值。这里需要注意的是，我们应该先初始化第一行和第一列，每一行当前位置的最大值仅取决于该位置左边相邻的值，每一列当前位置的最大值仅取决于该位置上边相邻的值，然后向右下角进行搜索即可，最后最大值就是右下角的值。

具体代码如下：

```java
class Solution {
    public int maxValue(int[][] grid) {
        for (int i = 1; i < grid.length; i++) {
            grid[i][0] += grid[i - 1][0];
        }
        for (int i = 1; i < grid[0].length; i++) {
            grid[0][i] += grid[0][i - 1];
        }

        for (int i = 1; i < grid.length; i++) {
            for (int j = 1; j < grid[0].length; j++) {
                grid[i][j] += Math.max(grid[i - 1][j], grid[i][j - 1]);
            }
        }
        return grid[grid.length - 1][grid[0].length - 1];
    }
}
```

如果用常规的深度优先搜索遍历会超时，所以需要一个记忆数组用于存放之前已经遍历过的位置，具体做法就是先递归到最右下角，然后往`(0,0)`方向开始递归返回值(DFS和动态规划正好是相反的过程)，最后返回起点值即为所求值。

具体代码如下：

```java
class Solution {
    int[][] memo;

    public int maxValue(int[][] grid) {
        memo = new int[grid.length][grid[0].length];
        return dfs(grid, 0, 0);
    }

    private int dfs(int[][] grid, int row, int column) {
        if (memo[row][column] > 0) {
            return memo[row][column];
        }

        int rightVal = grid[row][column], downVal = grid[row][column];
        //如果没到最右边一直向右递归
        if (column + 1 < grid[0].length)
            rightVal += +dfs(grid, row, column + 1);

        //如果没到最下边一直向下递归
        if (row + 1 < grid.length)
            downVal += dfs(grid, row + 1, column);

        //存储当前位置的较大值
        memo[row][column] = Math.max(rightVal, downVal);
        return memo[row][column];

    }
}
```




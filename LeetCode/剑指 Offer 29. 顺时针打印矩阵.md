---
zmathjax: true
toc: true
categories:
 - LeetCode
tags:
 - 刷题笔记
---

#### [剑指 Offer 29. 顺时针打印矩阵](https://leetcode-cn.com/problems/shun-shi-zhen-da-yin-ju-zhen-lcof/)

输入一个矩阵，按照从外向里以顺时针的顺序依次打印出每一个数字。

<!--more-->

**示例1：**

```
输入：matrix = [[1,2,3],[4,5,6],[7,8,9]]
输出：[1,2,3,6,9,8,7,4,5]
```

**示例2：**

```
输入：matrix = [[1,2,3,4],[5,6,7,8],[9,10,11,12]]
输出：[1,2,3,4,8,12,11,10,9,5,6,7]
```

**限制：**

- `0 <= matrix.length <= 100`
- `0 <= matrix[i].length <= 100`

来源：力扣（LeetCode）
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

### 题解：

本题代码不好写，但是思路比较好想，就是一圈一圈打印，由此思路，我们可以设置两个点，即方框左上角的点和右下角的点，每打印一圈，左上角的点向右下角缩，右下角的点向左上角缩，这样循环就可以打印完所有的点。这里还需要考虑两种特殊情况，如果左上角点的行和右下角点的行相等，直接递增打印这一行即可，同理若处于同一列，递增打印这一列即可。

具体代码如下：

```java
class Solution {
    int[] result;
    int index = 0;

    public int[] spiralOrder(int[][] matrix) {
        if (matrix.length == 0) return new int[]{};
        int leftRow = 0;
        int leftColumn = 0;
        int rightRow = matrix.length - 1;
        int rightColumn = matrix[0].length - 1;
        result = new int[matrix.length * matrix[0].length];

        //左上角的点向右下角缩，右下角的点向左上角缩
        while (leftRow <= rightRow && leftColumn <= rightColumn) {
            printEdge(matrix, leftRow++, leftColumn++, rightRow--, rightColumn--);
        }
        return result;
    }

    private void printEdge(int[][] matrix, int leftRow, int leftColumn, int rightRow, int rightColumn) {
        //行相等
        if (leftRow == rightRow) {
            for (int i = leftColumn; i <= rightColumn; i++) {
                result[index++] = matrix[leftRow][i];
            }
            //列相等
        } else if (leftColumn == rightColumn) {
            for (int i = leftRow; i <= rightRow; i++) {
                result[index++] = matrix[i][leftColumn];
            }
        } else {
            //按照上、右、下、左的顺序打印即可
            int curColumn = leftColumn;
            int curRow = leftRow;

            while (curColumn != rightColumn) {
                result[index++] = matrix[leftRow][curColumn++];
            }

            while (curRow != rightRow) {
                result[index++] = matrix[curRow++][rightColumn];
            }

            while (curColumn != leftColumn) {
                result[index++] = matrix[rightRow][curColumn--];
            }

            while (curRow != leftRow) {
                result[index++] = matrix[curRow--][leftColumn];
            }
        }
    }
}
```


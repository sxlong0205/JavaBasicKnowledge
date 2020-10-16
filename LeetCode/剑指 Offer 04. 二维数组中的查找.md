---
zmathjax: true
toc: true
categories:
 - LeetCode
tags:
 - 刷题笔记
---

#### [剑指 Offer 04. 二维数组中的查找](https://leetcode-cn.com/problems/er-wei-shu-zu-zhong-de-cha-zhao-lcof/)

在一个 `n * m` 的二维数组中，每一行都按照从左到右递增的顺序排序，每一列都按照从上到下递增的顺序排序。请完成一个函数，输入这样的一个二维数组和一个整数，判断数组中是否含有该整数。

<!--more-->

**示例 ：**

现有矩阵 `matrix` 如下：

```
[
  [1,   4,  7, 11, 15],
  [2,   5,  8, 12, 19],
  [3,   6,  9, 16, 22],
  [10, 13, 14, 17, 24],
  [18, 21, 23, 26, 30]
]
```

给定 target = `5`，返回 `true`。

给定 target = `20`，返回 `false`。

**限制：**

```
0 <= n <= 1000
0 <= m <= 1000
```

来源：力扣（LeetCode）
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

### 题解：

本题最直接的解法就是暴力破解，这个不做过多解释，大家应该都能想到。

具体代码如下：

```java
class Solution {
    public boolean findNumberIn2DArray(int[][] matrix, int target) {
        for (int i = 0; i < matrix.length; i++) {
            for (int j = 0; j < matrix[0].length; j++) {
                if (matrix[i][j] == target)
                    return true;
            }
        }
        return false;
    }
}
```

本题由于横纵都是有序集合，所以一定有优化的空间，一看到有序的数组，我们本能地反应出要用二分查找，我们对每个小数组进行二分查找，如果找到了`target`则返回`true`，否则对下一个小数组进行二分查找，要是都没有找到，就返回`false`

具体代码如下:

```java
class Solution {
    public boolean findNumberIn2DArray(int[][] matrix, int target) {
        for (int i = 0; i < matrix.length; i++) {
            if (Arrays.binarySearch(matrix[i], target) >= 0)
                return true;
            else
                continue;
        }
        return false;
    }
}
```

最后一种方法是借鉴官方做法，我们从二维数组的右上角判断该位置数字和`target`值的大小，如果该位置数字等于`target`则返回`true`；如果该位置数组小于`target`，我们递增到下一行同样的位置比较大小；如果该位置数字大于`target`，我们需要向左遍历该子数组，判断`target`是否存在于这个子数组中，如果存在返回`true`，否则返回`false`

具体代码如下：

```java
class Solution {
    public boolean findNumberIn2DArray(int[][] matrix, int target) {
        if (matrix.length == 0 || matrix[0].length == 0)
            return false;
        int m = matrix.length;
        int n = matrix[0].length;
        for (int i = 0; i < m; i++) {
            if (matrix[i][n - 1] == target) {
                return true;
            } else if (matrix[i][n - 1] < target) {
                continue;
            } else {
                for (int j = n - 1; j >= 0; j--) {
                    if (matrix[i][j] == target)
                        return true;
                }
            }
        }
        return false;
    }
}
```


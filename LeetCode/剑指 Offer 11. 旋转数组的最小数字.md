---
zmathjax: true
toc: true
categories:
 - LeetCode
tags:
 - 刷题笔记
---

#### [剑指 Offer 11. 旋转数组的最小数字](https://leetcode-cn.com/problems/xuan-zhuan-shu-zu-de-zui-xiao-shu-zi-lcof/)

把一个数组最开始的若干个元素搬到数组的末尾，我们称之为数组的旋转。输入一个递增排序的数组的一个旋转，输出旋转数组的最小元素。例如，数组` [3,4,5,1,2] `为 `[1,2,3,4,5] `的一个旋转，该数组的最小值为`1`。

<!--more-->

**示例 1:**

```
输入：[3,4,5,1,2]
输出：1
```

**示例 2：**

```
输入：[2,2,2,0,1]
输出：0
```

来源：力扣（LeetCode）
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

### 题解：

本题由于官方测试用例规模小，所以最直接的想法就是遍历整个数组，把`numbers[0]`当做哨兵，如果后面的元素有小于`numbers[0]`的，返回第一个检索到的数值，如果没有，则`numbers[0]`就是该序列最小数，直接返回。当然用二分查找也是可以的，如果时间复杂度超了的话，我们就要考虑二分的方法。

具体实现代码如下：

```java
class Solution {
    public int minArray(int[] numbers) {
        for (int i = 1; i < numbers.length; i++) {
            if (numbers[i] < numbers[0]) {
                return numbers[i];
            }
        }
        return numbers[0];
    }
}
```










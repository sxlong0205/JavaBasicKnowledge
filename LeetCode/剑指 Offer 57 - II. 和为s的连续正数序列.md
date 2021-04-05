---
zmathjax: true
toc: true
categories:
 - LeetCode
tags:
 - 刷题笔记
---

#### [剑指 Offer 57 - II. 和为s的连续正数序列](https://leetcode-cn.com/problems/he-wei-sde-lian-xu-zheng-shu-xu-lie-lcof/)

输入一个正整数 target ，输出所有和为 target 的连续正整数序列（至少含有两个数）。

序列内的数字由小到大排列，不同序列按照首个数字从小到大排列。

<!--more-->

**示例1：**

```
输入：target = 9
输出：[[2,3,4],[4,5]]
```

**示例2:**

```
输入：target = 15
输出：[[1,2,3,4,5],[4,5,6],[7,8]]
```

**限制：**

- `1 <= target <= 10^5`

来源：力扣（LeetCode）
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

### 题解：

本题其实也很好想，就是滑动窗口，因为数组是从小到大的顺序，我们通过改变窗口的大小，来判断窗口内的数字和是否满足题目所要求的条件，最后将符合条件的数组加入到结果数组即可。

具体代码如下：

```java
class Solution {
    public int[][] findContinuousSequence(int target) {
        List<int[]> list = new ArrayList<>();

        for (int left = 1, right = 1, sum = 0; right < target; right++) {
            sum += right;
            //如果sum比target大，将left右移，缩小窗口
            while (sum > target) {
                sum -= left;
                left++;
            }

            //如果窗口内的数字满足条件，将数组中的数字添加到list即可
            if (sum == target) {
                int[] temp = new int[right - left + 1];
                for (int i = 0; i < temp.length; i++) {
                    temp[i] = left + i;
                }

                list.add(temp);
            }
        }

        //将list转换为int[][]
        int[][] result = new int[list.size()][];
        for (int i = 0; i < list.size(); i++) {
            result[i] = list.get(i);
        }
        return result;
    }
}
```


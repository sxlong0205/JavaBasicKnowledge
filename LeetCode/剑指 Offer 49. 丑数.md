---
zmathjax: true
toc: true
categories:
 - LeetCode
tags:
 - 刷题笔记
---

#### [剑指 Offer 49. 丑数](https://leetcode-cn.com/problems/chou-shu-lcof/)

我们把只包含质因子 2、3 和 5 的数称作丑数（Ugly Number）。求按从小到大的顺序的第 n 个丑数。

<!--more-->

**示例 :**

```
输入: n = 10
输出: 12
解释: 1, 2, 3, 4, 5, 6, 8, 9, 10, 12 是前 10 个丑数。
```

**说明:** 

1.  `1` 是丑数。
2.  `n` **不超过**1690。

来源：力扣（LeetCode）
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

### 题解：

本题说实话，没啥意思，就是先把可能结果全算出来然后返回需要的结果，美其名曰动态规划、堆，其实就是面向测试用例编程。这里用动态规划的思想构造结果数据，因为丑数是以2、3、5为质因子的，所以使用三个指针，分别是对应质数2、3、5，每次取三个指针之一乘以对应质数存入相应的位置。

具体代码如下：

```java
class Solution {
    public int nthUglyNumber(int n) {
        int[] nums = new int[1690];
        nums[0] = 1;
        int p2 = 0, p3 = 0, p5 = 0, temp = 0;

        for (int i = 1; i < 1690; i++) {
            temp = Math.min(Math.min(nums[p2] * 2, nums[p3] * 3), nums[p5] * 5);
            nums[i] = temp;

            if (temp == nums[p2] * 2) p2++;
            if (temp == nums[p3] * 3) p3++;
            if (temp == nums[p5] * 5) p5++;
        }
        return nums[n - 1];
    }
}
```


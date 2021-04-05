---
zmathjax: true
toc: true
categories:
 - LeetCode
tags:
 - 刷题笔记
---

#### [剑指 Offer 61. 扑克牌中的顺子](https://leetcode-cn.com/problems/bu-ke-pai-zhong-de-shun-zi-lcof/)

从扑克牌中随机抽5张牌，判断是不是一个顺子，即这5张牌是不是连续的。2～10为数字本身，A为1，J为11，Q为12，K为13，而大、小王为 0 ，可以看成任意数字。A 不能视为 14。

<!--more-->

**示例1：**

```
输入: [1,2,3,4,5]
输出: True
```

**示例 2：**

```
输入: [0,0,1,2,5]
输出: True
```

**限制：**

数组长度为 5 

数组的数取值为 [0, 13] .

来源：力扣（LeetCode）
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

### 题解：

本题有个最直观的解法，就是先对给定数组进行排序，然后遍历数组，看看是否满足条件。具体来说，统计数组中0的个数，如果相邻两个数组相差`1`，直接跳过，如果大于`1`，判断差值和大小王个数，如果差值大于大小王个数，直接返回`false`，表示无法通过大小王弥补成一个顺子，如果小于大小王个数，则用大小王填补，同时让大小王个数减去差值。需要特别注意的是，如果出现除了`0`之外相邻两个数字相等时，无法组成顺子，直接返回`false`。

具体代码如下：

```java
class Solution {
    public boolean isStraight(int[] nums) {
        Arrays.sort(nums);
        int count = 0;

        for (int i = 0; i < nums.length - 1; i++) {
            if (nums[i] == 0) {
                count++;
            } else if (nums[i + 1] == nums[i]) {
                return false;
            } else if (nums[i + 1] - nums[i] == 1) {
                continue;
            } else if (nums[i + 1] - nums[i] - 1 <= count) {
                count -= (nums[i + 1] - nums[i]);
            } else if (nums[i + 1] - nums[i] - 1 > count) {
                return false;
            }
        }
        return true;
    }
}
```


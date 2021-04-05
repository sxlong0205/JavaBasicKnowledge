---
zmathjax: true
toc: true
categories:
 - LeetCode
tags:
 - 刷题笔记
---

#### [剑指 Offer 42. 连续子数组的最大和](https://leetcode-cn.com/problems/lian-xu-zi-shu-zu-de-zui-da-he-lcof/)

输入一个整型数组，数组中的一个或连续多个整数组成一个子数组。求所有子数组的和的最大值。

要求时间复杂度为O(n)。

<!--more-->

**示例：**

```
输入: nums = [-2,1,-3,4,-1,2,1,-5,4]
输出: 6
解释: 连续子数组 [4,-1,2,1] 的和最大，为 6。
```

**提示：**

-   `1 <= arr.length <= 10^5`
-   `-100 <= arr[i] <= 100`

来源：力扣（LeetCode）
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

### 题解：

本题由于要求局部的连续子数组的最大和，可以立马想到动态规划的方式来解题。因为只需要返回值，我们可以直接在原数组上进行操作，具体来说，如果当前元素的前一个元素小于零，那么加上一个负数势必不能保证当前和最大，所以如果出现这种情况直接跳过；如果当前元素的前一个元素大于零，那么就让当前元素加上前一个位置的值，将新值赋给当前位置。同时创建一个整型变量用来记录当前的连续子数组的最大和，最后返回该变量即可。

具体代码如下：

```java
class Solution {
    public int maxSubArray(int[] nums) {
        if (nums.length == 1) return nums[0];
        
        int result = nums[0];

        for (int i = 1; i < nums.length; i++) {
            if (nums[i - 1] > 0) {
                nums[i] += nums[i - 1];
                result = Math.max(result, nums[i]);
            }else {
                result = Math.max(result, nums[i]);
            }
        }
        return result;
    }
}
```


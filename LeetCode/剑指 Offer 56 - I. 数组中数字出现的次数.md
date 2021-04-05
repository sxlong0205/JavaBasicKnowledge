---
zmathjax: true
toc: true
categories:
 - LeetCode
tags:
 - 刷题笔记
---

#### [剑指 Offer 56 - I. 数组中数字出现的次数](https://leetcode-cn.com/problems/shu-zu-zhong-shu-zi-chu-xian-de-ci-shu-lcof/)

一个整型数组 `nums` 里除两个数字之外，其他数字都出现了两次。请写程序找出这两个只出现一次的数字。要求时间复杂度是O(n)，空间复杂度是O(1)。

<!--more-->

**示例1：**

```
输入：nums = [4,1,4,6]
输出：[1,6] 或 [6,1]
```

**示例2:**

```
输入：nums = [1,2,10,4,1,4,3,3]
输出：[2,10] 或 [10,2]
```

来源：力扣（LeetCode）
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

### 题解：

这道题和[136. 只出现一次的数字](https://leetcode-cn.com/problems/single-number/)思路一致，就是通过全员异或，找出只出现了一次的数字，但是这题有个问题，数组中有两个只出现了一次的数字，那么进行全员异或的话，最后的结果是两个只出现了一次数字的异或结果。如何将两个数字分开是我们需要考虑的，一个很自然而然的方法就是将数字分组，将两个只出现一次的数字放在不同的分组里面，这样对两个数组分别全员异或，就能得到所求值。那么如何分组呢？我们思考，两个数字异或，如果某一位为`1`，说明在这个位置上两个数字不相等，那么就用这个位来区分。具体来说，就是数组中每个数字都和这个固定位为`1`的数字比较，如果当前数字和该数相与为`0`分为一组，不为`0`分为另外一组。

具体代码如下：

```java
class Solution {
    public int[] singleNumbers(int[] nums) {
        int result = 0;
        for (int num : nums) {
            result ^= num;
        }

        int mask = 1;
        while ((result & mask) == 0) {
            mask <<= 1;
        }
        
        int left = 0;
        int right = 0;
        for (int num : nums) {
            if ((num & mask) == 0) {
                left ^= num;
            }else {
                right ^= num;
            }
        }
        
        return new int[]{left, right};
    }
}
```


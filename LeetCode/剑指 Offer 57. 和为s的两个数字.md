---
zmathjax: true
toc: true
categories:
 - LeetCode
tags:
 - 刷题笔记
---

#### [剑指 Offer 57. 和为s的两个数字](https://leetcode-cn.com/problems/he-wei-sde-liang-ge-shu-zi-lcof/)

输入一个递增排序的数组和一个数字s，在数组中查找两个数，使得它们的和正好是s。如果有多对数字的和等于s，则输出任意一对即可。

<!--more-->

**示例1：**

```
输入：nums = [2,7,11,15], target = 9
输出：[2,7] 或者 [7,2]
```

**示例2:**

```
输入：nums = [10,26,30,31,47,60], target = 40
输出：[10,30] 或者 [30,10]
```

**限制：**

- `1 <= nums.length <= 10^5`
- `1 <= nums[i] <= 10^6`

来源：力扣（LeetCode）
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

### 题解：

本题最简单的也是最有效的方法就是双指针，当然有大神通过花里胡哨的二分效果也不错，但是我觉得双指针使我们最应该学习的。

具体来说就是定义两个指针，一个指向头，一个指向尾，每次判断两个指针所指值之和与`target`的大小，

- 如果等于，直接返回两个指针指向的值即可；
- 如果`target`小于两指针指向值之和，让右指针向前移；
- 如果`target`大于两指针指向值之和，让左指针后移。

由于数组是经过排序的，所以这种方式可以很容易找到满足条件的值。

具体代码如下：

```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        int left = 0, right = nums.length - 1;
        
        while (left < right) {
            if (nums[left] + nums[right] == target) {
                return new int[]{nums[left], nums[right]};
            } else if (nums[left] + nums[right] < target) {
                left++;
            } else {
                right--;
            }
        }
        return new int[]{-1, -1};
    }
}
```


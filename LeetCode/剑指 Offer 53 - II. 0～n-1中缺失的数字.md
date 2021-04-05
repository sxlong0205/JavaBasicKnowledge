---
zmathjax: true
toc: true
categories:
 - LeetCode
tags:
 - 刷题笔记
---

#### [剑指 Offer 53 - II. 0～n-1中缺失的数字](https://leetcode-cn.com/problems/que-shi-de-shu-zi-lcof/)

一个长度为n-1的递增排序数组中的所有数字都是唯一的，并且每个数字都在范围0～n-1之内。在范围0～n-1内的n个数字中有且只有一个数字不在该数组中，请找出这个数字。

<!--more-->

**示例 1:**

```
输入: [0,1,3]
输出: 2
```

**示例 2:**

```
输入: [0,1,2,3,4,5,6,7,9]
输出: 8
```

**限制：**

```
1 <= 数组长度 <= 10000
```

来源：力扣（LeetCode）
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

### 题解：

本题一看到递增排序数组，那直接二分查找的基调就定了下来，然后再思考，满足条件的数组应该是什么样子。我们举个例子，数组为`[0,1,3]`，这是一个长度为`n - 1`的数组，完整的长度为`n`的数组应该是`[0,1,2,3]`，缺失了`2`，所以应该返回`2`。仔细观察，可以发现满足条件`nums[i] = i`的时候，`[0,i]`之间一定都是满足条件的，所以缺失值出现在`[i + 1, n - 1]`，当`nums[i] != i`时，缺失情况出现，此时`left`值即为缺失值，由于需要跳出循环，所以我们需要让右边界缩小。

具体代码如下：

```java
class Solution {
    public int missingNumber(int[] nums) {
        int left = 0, mid = 0, right = nums.length;
        while (left < right) {
            mid = left + ((right - left) >> 1);
            if (nums[mid] == mid) {
                left = mid + 1;
            } else {
                right = mid;
            }
        }
        return left;
    }
}
```


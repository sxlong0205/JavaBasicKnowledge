---
zmathjax: true
toc: true
categories:
 - LeetCode
tags:
 - 刷题笔记
---

#### [剑指 Offer 53 - I. 在排序数组中查找数字 I](https://leetcode-cn.com/problems/zai-pai-xu-shu-zu-zhong-cha-zhao-shu-zi-lcof/)

统计一个数字在排序数组中出现的次数。

<!--more-->

**示例 1:**

```
输入: nums = [5,7,7,8,8,10], target = 8
输出: 2
```

**示例 2:**

```
输入: nums = [5,7,7,8,8,10], target = 6
输出: 0
```

**限制：**

```
0 <= 数组长度 <= 50000
```

来源：力扣（LeetCode）
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

### 题解：

本题一看到排序数组四个大字，我啪的一下就站起来了，很快啊，直接二分查找，套用模板，这里唯一需要注意的一个细节就是，target有可能在nums数组中重复，只需要在找到目标值后，向前向后搜索，把所有满足要求的结果都找到。

具体代码如下：

```java
class Solution {
    public int search(int[] nums, int target) {
        if (nums.length == 0) return 0;
        int left = 0, right = nums.length, result = 0;
        int mid;
        while (left < right) {
            mid = left + (right - left) / 2;
            if (nums[mid] == target) {
                result++;
                int temp = mid - 1;
                while (temp >= 0 && nums[temp] == target) {
                    result++;
                    temp--;
                }
                temp = mid + 1;
                while (temp < nums.length && nums[temp] == target) {
                    result++;
                    temp++;
                }
                break;
            } else if (nums[mid] > target) {
                right = mid;
            } else {
                left = mid + 1;
            }
        }
        return result;
    }
}
```


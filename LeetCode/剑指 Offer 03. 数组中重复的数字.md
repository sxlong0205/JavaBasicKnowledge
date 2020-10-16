---
zmathjax: true
toc: true
categories:
 - LeetCode
tags:
 - 刷题笔记
---

#### [剑指 Offer 03. 数组中重复的数字](https://leetcode-cn.com/problems/shu-zu-zhong-zhong-fu-de-shu-zi-lcof/)

找出数组中重复的数字。


在一个长度为 n 的数组 nums 里的所有数字都在 0～n-1 的范围内。数组中某些数字是重复的，但不知道有几个数字重复了，也不知道每个数字重复了几次。请找出数组中任意一个重复的数字。

<!--more-->

**示例1 ：**

```
输入：
[2, 3, 1, 0, 2, 5, 3]
输出：2 或 3 
```

**限制：**

`2 <= n <= 100000`

来源：力扣（LeetCode）
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

### 题解：

本题最直接的解法就是暴力破解，这个不做过多解释，大家应该都能想到。

具体代码如下：

```java
class Solution {
    public int findRepeatNumber(int[] nums) {
        for (int i = 0; i < nums.length; i++) {
            for (int j = i + 1; j < nums.length; j++) {
                if (nums[i] == nums[j])
                    return nums[i];
            }
        }
        return -1;
    }
}
```

还有一种解法用到了`Set`集合的特性，遍历数组，判断数组中的每个数字是否都在`Set`集合中，如果存在直接返回，如果不存在则向集合中添加。

具体代码如下:

```java
class Solution {
    public int findRepeatNumber(int[] nums) {
        Set<Integer> result = new HashSet<>();
        for (int num : nums) {
            if (result.contains(num))
                return num;
            result.add(num);
        }
        return -1;
    }
}
```

至于很多题解说的原地置换的方法，我觉得有些取巧，就不再赘述。
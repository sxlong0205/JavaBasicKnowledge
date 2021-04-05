---
zmathjax: true
toc: true
categories:
 - LeetCode
tags:
 - 刷题笔记
---

#### [剑指 Offer 56 - II. 数组中数字出现的次数 II](https://leetcode-cn.com/problems/shu-zu-zhong-shu-zi-chu-xian-de-ci-shu-ii-lcof/)

在一个数组 `nums` 中除一个数字只出现一次之外，其他数字都出现了三次。请找出那个只出现一次的数字。

<!--more-->

**示例1：**

```
输入：nums = [3,4,3,3]
输出：4
```

**示例2:**

```
输入：nums = [9,1,7,9,7,9,7]
输出：1
```

**限制：**

- `1 <= nums.length <= 10000`
- `1 <= nums[i] < 2^31`

来源：力扣（LeetCode）
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

### 题解：

本题不讲有限状态机的做法，只从最直白的角度出发介绍两种解题方法。第一种就是使用Map将所有出现的数字作为Key，出现次数作为Value，最后查找Value为1的数字即可。

具体代码如下：

```java
class Solution {
    public int singleNumber(int[] nums) {
        Map<Integer, Integer> map = new HashMap<>();

        for (int num : nums) {
            map.put(num, map.getOrDefault(num, 0) + 1);
        }

        Set<Map.Entry<Integer, Integer>> entrySet = map.entrySet();
        for (Map.Entry<Integer, Integer> entry : entrySet) {
            if (entry.getValue() == 1)
                return entry.getKey();
        }
        return -1;
    }
}
```

另一种方法就是位运算，如果一个数组中一个数字出现了三次，那么他对应的二进制数字加和后可以被3整除，也就是对3取余为0，如果最后对3取余不为0，证明这位就是数组中唯一出现一次的数字对应的位置。通过这种方法，可以取得只出现一次数字的值。

具体代码如下：

```java
class Solution {
    public int singleNumber(int[] nums) {
        //整型最大32位，用32位数组存储
        int[] temp = new int[32];
        int result = 0;

        //这里统计数组中每个数字对应二进制一的个数
        for (int num : nums) {
            for (int i = 0; i < 32; i++) {
                temp[i] += num & 1;
                num >>>= 1;
            }
        }
        
        //最后统计只出现一次数字的数值
        for (int i = 31; i >= 0; i--) {
            result <<= 1;
            result |= (temp[i] % 3);
        }
        return result;
    }
}
```


---
zmathjax: true
toc: true
categories:
 - LeetCode
tags:
 - 刷题笔记
---

#### [剑指 Offer 66. 构建乘积数组](https://leetcode-cn.com/problems/gou-jian-cheng-ji-shu-zu-lcof/)

给定一个数组 A[0,1,…,n-1]，请构建一个数组 B[0,1,…,n-1]，其中 B 中的元素 B[i]=A[0]×A[1]×…×A[i-1]×A[i+1]×…×A[n-1]。不能使用除法。

<!--more-->

**示例：**

```
输入: [1,2,3,4,5]
输出: [120,60,40,30,24]
```

**提示：**

-   所有元素乘积之和不会溢出 32 位整数
-   `a.length <= 100000`

来源：力扣（LeetCode）
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

### 题解：

这种算术题目，我建议找一个通俗易懂的题解，然后记下来，因为这种题目面试要是出出来，想要在很短的时间内完成也是很困难的。这里推荐一位大佬的题解https://leetcode-cn.com/problems/gou-jian-cheng-ji-shu-zu-lcof/solution/mian-shi-ti-66-gou-jian-cheng-ji-shu-zu-biao-ge-fe/，其实基本的思想就是动态规划，维护两个乘积和。

具体代码如下：

```java
class Solution {
    public int[] constructArr(int[] a) {
        if (a.length == 0) return new int[]{};
        int[] left = new int[a.length];
      	int[] right = new int[a.length];
        b[0] = right[a.length - 1] = 1;

        for (int i = 1; i < a.length; i++) {
            left[i] = left[i - 1] * a[i - 1];
        }
        
        for (int i = a.length - 2; i >= 0; i--) {
            right[i] = right[i + 1] * a[i + 1];
        }
        
      	int result = new int[a.length];
      	for (int i = 0; i < a.length; i++) {
          	result[i] = left[i] * right[i];
        }
        return result;
    }
}
```


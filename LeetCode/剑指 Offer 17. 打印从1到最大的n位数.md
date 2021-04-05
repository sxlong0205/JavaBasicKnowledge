---
zmathjax: true
toc: true
categories:
 - LeetCode
tags:
 - 刷题笔记
---

#### [剑指 Offer 17. 打印从1到最大的n位数](https://leetcode-cn.com/problems/da-yin-cong-1dao-zui-da-de-nwei-shu-lcof/)

输入数字 `n`，按顺序打印出从 `1` 到最大的 `n` 位十进制数。比如输入 `3`，则打印出 `1、2、3` 一直到最大的 `3` 位数 `999`。

<!--more-->

**示例1：**

```
输入: n = 1
输出: [1,2,3,4,5,6,7,8,9]
```

来源：力扣（LeetCode）
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

### 题解：

本题想法非常直观，就是创建一个符合要求大小的数组，然后递增的填入数据即可。

具体代码如下：

```java
class Solution {
    public int[] printNumbers(int n) {
        int pow = (int) Math.pow(10, n);
        int[] result = new int[pow - 1];
        for (int i = 0; i < pow - 1; i++) {
            result[i] = i + 1;
        }
        return result;
    }
}
```


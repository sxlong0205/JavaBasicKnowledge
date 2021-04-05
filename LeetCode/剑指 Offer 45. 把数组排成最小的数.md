---
zmathjax: true
toc: true
categories:
 - LeetCode
tags:
 - 刷题笔记
---

#### [剑指 Offer 45. 把数组排成最小的数](https://leetcode-cn.com/problems/ba-shu-zu-pai-cheng-zui-xiao-de-shu-lcof/)

输入一个非负整数数组，把数组里所有数字拼接起来排成一个数，打印能拼接出的所有数字中最小的一个。

<!--more-->

**示例1：**

```
输入: [10,2]
输出: "102"
```

**示例2：**

```
输入: [3,30,34,5,9]
输出: "3033459"
```

**提示:**

-   0 < nums.length <= 100
    **说明:**

-   输出结果可能非常大，所以你需要返回一个字符串而不是整数
-   拼接起来的数字可能会有前导 0，最后结果不需要去掉前导 0

来源：力扣（LeetCode）
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

### 题解：

本题应该可以直接想到要排序，但是简单的升序排序会出现问题，比如`[3,30]`，如果单纯按照升序排序，得到的字符串是`"330"`，很显然有一个`"303"`比它更小。所以在排序中，需要将两个字符串拼接起来比较大小，即在每次遍历的过程中，需要比较`"330"`和`"303"`的大小，这样就不会出现上述问题。具体来说，先将所有的int类型数字转换为String类型，然后对String数组按照拼接后大小进行排序，最后组装字符串即可。

具体代码如下：

```java
class Solution {
    public String minNumber(int[] nums) {
        List<String> temp = new ArrayList<>();
        for (int num : nums) {
            temp.add(String.valueOf(num));
        }
        temp.sort((o1, o2) -> (o1 + o2).compareTo(o2 + o1));
        StringBuilder result = new StringBuilder();
        for (String s : temp) {
            result.append(s);
        }
        return result.toString();
    }
}
```


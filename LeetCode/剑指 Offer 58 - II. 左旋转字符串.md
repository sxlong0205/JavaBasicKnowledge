---
zmathjax: true
toc: true
categories:
 - LeetCode
tags:
 - 刷题笔记
---

#### [剑指 Offer 58 - II. 左旋转字符串](https://leetcode-cn.com/problems/zuo-xuan-zhuan-zi-fu-chuan-lcof/)

字符串的左旋转操作是把字符串前面的若干个字符转移到字符串的尾部。请定义一个函数实现字符串左旋转操作的功能。比如，输入字符串"abcdefg"和数字2，该函数将返回左旋转两位得到的结果"cdefgab"。

<!--more-->

**示例1：**

```
输入: s = "abcdefg", k = 2
输出: "cdefgab"
```

**示例2:**

```
输入: s = "lrloseumgh", k = 6
输出: "umghlrlose"
```

**限制：**

-   `1 <= k < s.length <= 10000`

来源：力扣（LeetCode）
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

### 题解：

本题我实在想不出什么高端操作，索性直接调用API。

具体代码如下：

```java
class Solution {
    public String reverseLeftWords(String s, int n) {
        StringBuilder sb = new StringBuilder();
        sb.append(s.substring(n, s.length()));
        sb.append(s.substring(0, n));
        return sb.toString();
    }
}
```


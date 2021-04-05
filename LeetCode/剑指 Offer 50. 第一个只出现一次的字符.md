---
zmathjax: true
toc: true
categories:
 - LeetCode
tags:
 - 刷题笔记
---

#### [剑指 Offer 50. 第一个只出现一次的字符](https://leetcode-cn.com/problems/di-yi-ge-zhi-chu-xian-yi-ci-de-zi-fu-lcof/)

在字符串 s 中找出第一个只出现一次的字符。如果没有，返回一个单空格。 s 只包含小写字母。

<!--more-->

**示例 :**

```
s = "abaccdeff"
返回 "b"

s = "" 
返回 " "
```

**限制：**

```
0 <= s 的长度 <= 50000
```

来源：力扣（LeetCode）
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

### 题解：

本题思路很简单，就是先遍历一遍字符串，算出每个字母出现的次数，然后在进行一次遍历，找到出现次数为`1`的字母返回即可。这里不管你是用`char`数组还是`Map`还是其他的都可以。

具体代码如下：

```java
class Solution {
    public char firstUniqChar(String s) {
        if (s == null) return ' ';
        char result = ' ';
        Map<Character, Integer> map = new LinkedHashMap<>();

        for (int i = 0; i < s.length(); i++) {
            char temp = s.charAt(i);
            map.put(temp, map.getOrDefault(temp, 0) + 1);
        }

        for (Character c : map.keySet()) {
            if (map.get(c) == 1) {
                result = c;
                break;
            }
        }
        return result;
    }
}
```


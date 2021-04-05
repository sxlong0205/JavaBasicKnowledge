---
zmathjax: true
toc: true
categories:
 - LeetCode
tags:
 - 刷题笔记
---

#### [剑指 Offer 58 - I. 翻转单词顺序](https://leetcode-cn.com/problems/fan-zhuan-dan-ci-shun-xu-lcof/)

输入一个英文句子，翻转句子中单词的顺序，但单词内字符的顺序不变。为简单起见，标点符号和普通字母一样处理。例如输入字符串"I am a student. "，则输出"student. a am I"。

<!--more-->

**示例1：**

```
输入: "the sky is blue"
输出: "blue is sky the"
```

**示例2:**

```
输入: "  hello world!  "
输出: "world! hello"
解释: 输入字符串可以在前面或者后面包含多余的空格，但是反转后的字符不能包括。
```

**示例 3：**

```
输入: "a good   example"
输出: "example good a"
解释: 如果两个单词间有多余的空格，将反转后单词间的空格减少到只含一个。
```

**说明：**

- 无空格字符构成一个单词。
- 输入字符串可以在前面或者后面包含多余的空格，但是反转后的字符不能包括。
- 如果两个单词间有多余的空格，将反转后单词间的空格减少到只含一个。

来源：力扣（LeetCode）
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

### 题解：

本题虽然花式方法层出不穷，但是大致都是通过分割数组，然后从后往前遍历，将每个单词添加进结果中实现的。我在这里介绍两种方法，第一种就是双指针，首先对字符串进行`trim`操作，将首位空格去除，然后两个指针从后往前遍历，一个指针`i`遇到不是空格的时候前移，然后`i`指针会停在第一个从后往前的空格位置上，将`(i+1,j+1)`子串添加进结果字符串，然后改变规则，`i`遇到是空格的时候前移，这样i会指向从后往前的第二个单词的最后一个字母上，让`j=i`，`i`继续下次循环。

具体代码如下：

```java
class Solution {
    public String reverseWords(String s) {
        if (s.length() == 0)
            return "";
        
        s = s.trim();
        StringBuilder stringBuilder = new StringBuilder();
        int i = s.length() - 1, j = s.length() - 1;
        
        while (i >= 0) {
            while (i >= 0 && s.charAt(i) != ' ') i--;
            stringBuilder.append(s.substring(i + 1, j + 1) + " ");
            while (i >= 0 && s.charAt(i) == ' ') i--;
            j = i;
        }
        
        //最后一个添加进的单词后面也会跟一个空格，所以需要进行trim将空格去掉
        return stringBuilder.toString().trim();
    }
}
```

基于上述思想，我们可以直接将字符串按照空格切分为不同的字符，如果是单词，就加入结果字符串，如果是空字符串，直接进行下一轮循环。

具体代码如下：

```java
class Solution {
    public String reverseWords(String s) {
        if (s.length() == 0)
            return "";
        
        s = s.trim();
        StringBuilder stringBuilder = new StringBuilder();
        
        String[] strs = s.split(" ");

        for (int i = strs.length - 1; i >= 0; i--) {
            if (strs[i].equals("")) continue;
            stringBuilder.append(strs[i] + " ");
        }
        
        return stringBuilder.toString().trim();
    }
}
```




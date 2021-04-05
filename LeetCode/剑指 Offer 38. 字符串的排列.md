---
zmathjax: true
toc: true
categories:
 - LeetCode
tags:
 - 刷题笔记
---

#### [剑指 Offer 38. 字符串的排列](https://leetcode-cn.com/problems/zi-fu-chuan-de-pai-lie-lcof/)

输入一个字符串，打印出该字符串中字符的所有排列。

你可以以任意顺序返回这个字符串数组，但里面不能有重复元素。

<!--more-->

**示例：**

```
输入：s = "abc"
输出：["abc","acb","bac","bca","cab","cba"]
```

**限制：**

```
1 <= s 的长度 <= 8
```

来源：力扣（LeetCode）
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

### 题解：

本题的难点并不在于如何求出全排列，而在于满足题目条条框框的返回值，本题解法可能不是最优的，但我感觉是比较好理解的。由于给定字符串会出现重复字符，所以我们需要使用`Set`对结果数组进行去重，利用`visited`数组可以进行剪枝操作。我们递归添加每个字符，当长度为`s`的长度时，证明完成了一个排列，直接添加到结果数组即可，如果不满足，递归地调用下一层，递归前后，需要用`visited`标记当前位置已经被访问。

具体代码如下：

```java
class Solution {
    Set<String> result = new HashSet<>();

    public String[] permutation(String s) {
        if (s.length() == 0)
            return new String[]{};

        boolean[] visited = new boolean[s.length()];
        backtrack(s, "", visited);
        return result.toArray(new String[result.size()]);
    }

    private void backtrack(String s, String temp, boolean[] visited) {
        if (temp.length() == s.length()) {
            result.add(temp);
            return;
        }

        for (int i = 0; i < s.length(); i++) {
            if (visited[i])
                continue;

            visited[i] = true;
            backtrack(s, temp + s.charAt(i), visited);
            visited[i] = false;
        }
    }
}
```


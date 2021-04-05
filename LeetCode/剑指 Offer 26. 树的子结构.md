---
zmathjax: true
toc: true
categories:
 - LeetCode
tags:
 - 刷题笔记
---

#### [剑指 Offer 26. 树的子结构](https://leetcode-cn.com/problems/shu-de-zi-jie-gou-lcof/)

输入两棵二叉树`A`和`B`，判断`B`是不是`A`的子结构。(约定空树不是任意一个树的子结构)

`B`是`A`的子结构， 即`A`中有出现和`B`相同的结构和节点值。

<!--more-->

例如:
给定的树 `A`：

```
     3
    / \
   4   5
  / \
 1   2
```

给定的树 B：

```
   4 
  /
 1
```

返回 `true`，因为 `B` 与 `A` 的一个子树拥有相同的结构和节点值。

**示例 1：**

```
输入：A = [1,2,3], B = [3,1]
输出：false
```

**示例 2：**

```
输入：A = [3,4,5,1,2], B = [4,1]
输出：true
```

**限制：**

- `0 <= 节点个数 <= 10000`

来源：力扣（LeetCode）
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

### 题解：

本题思路比较简单，要判断`B`是否为`A`的子结构，有两种可能，第一种是`A`的根结点就是`B`的根结点，那么只需要递归遍历左右子树即可，第二种情况就是`B`的根结点不在`A`的根结点上，这种情况需要递归地遍历，找到`B`的根结点在`A`中的位置，然后判断。

具体代码如下：

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    public boolean isSubStructure(TreeNode A, TreeNode B) {
        if (A == null || B == null)
            return false;
        return isSub(A, B) || isSubStructure(A.left, B) || isSubStructure(A.right, B);
    }

    private boolean isSub(TreeNode a, TreeNode b) {
        //如果b为空，证明B已经遍历完，即A中存在子结构B
        if (b == null)
            return true;

        //如果A遍历完或者两结点值不相等，那么返回false
        if (a == null || a.val != b.val)
            return false;

        return isSub(a.left, b.left) && isSub(a.right, b.right);
    }
}
```


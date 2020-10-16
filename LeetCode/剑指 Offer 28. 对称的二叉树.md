---
zmathjax: true
toc: true
categories:
 - LeetCode
tags:
 - 刷题笔记
---

#### [剑指 Offer 28. 对称的二叉树](https://leetcode-cn.com/problems/dui-cheng-de-er-cha-shu-lcof/)

给定一个二叉树，检查它是否是镜像对称的。

<!--more-->

例如，二叉树` [1,2,2,3,4,4,3] `是对称的。

    		1
       / \
      2   2
     / \ / \
    3  4 4  3

但是下面这个 `[1,2,2,null,3,null,3] `则不是镜像对称的:

    		1
       / \
      2   2
       \   \
       3    3
来源：力扣（LeetCode）
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。

### 题解：

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
    public boolean isSymmetric(TreeNode root) {
        if (root == null) return true;
        return tranverse(root.left, root.right);
    }

    public static boolean tranverse(TreeNode leftNode, TreeNode rightNode) {
        if (leftNode == null && rightNode == null) return true;
        if (leftNode == null || rightNode == null || leftNode.val != rightNode.val) return false;
        return tranverse(leftNode.left, rightNode.right) && tranverse(leftNode.right, rightNode.left);
    }
}
```


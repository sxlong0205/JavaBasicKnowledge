---
zmathjax: true
toc: true
categories:
 - LeetCode
tags:
 - 刷题笔记
---

#### [剑指 Offer 55 - I. 二叉树的深度](https://leetcode-cn.com/problems/er-cha-shu-de-shen-du-lcof/)

输入一棵二叉树的根节点，求该树的深度。从根节点到叶节点依次经过的节点（含根、叶节点）形成树的一条路径，最长路径的长度为树的深度。

例如：

给定二叉树 `[3,9,20,null,null,15,7]`，

<!--more-->

```
    3
   / \
  9  20
    /  \
   15   7
```

返回它的最大深度 3 。

**提示：**

1.  `节点总数 <= 10000`

来源：力扣（LeetCode）
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

### 题解：

本题其实不难，我们先拿一个结点来看，如何测算树的高度，是不是就是左子树的高度与右子树的高度中的较大值，加上当前这个结点的高度加一，就是这棵树的高度。于是，递归的遍历左子树和右子树，找出左右子树的高度值，它们当中的较大值加上根结点的一就是整棵树的高度。

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
    public int maxDepth(TreeNode root) {
        if (root == null) return 0;
        int left = maxDepth(root.left);
        int right = maxDepth(root.right);
        return Math.max(left, right) + 1;
    }
}
```


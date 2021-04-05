---
zmathjax: true
toc: true
categories:
 - LeetCode
tags:
 - 刷题笔记
---

#### [剑指 Offer 55 - II. 平衡二叉树](https://leetcode-cn.com/problems/ping-heng-er-cha-shu-lcof/)

输入一棵二叉树的根节点，判断该树是不是平衡二叉树。如果某二叉树中任意节点的左右子树的深度相差不超过1，那么它就是一棵平衡二叉树。

<!--more-->

**示例 1:**

给定二叉树 [3,9,20,null,null,15,7]

```
    3
   / \
  9  20
    /  \
   15   7
```

返回 true 。

**示例 2:**

给定二叉树 [1,2,2,3,3,null,null,4,4]

          1
         / \
        2   2
       / \
      3   3
     / \
    4   4

返回 false 。 

**限制：**

```
1 <= 树的结点个数 <= 10000
```

来源：力扣（LeetCode）
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

### 题解：

本题承接[剑指 Offer 55 - I. 二叉树的深度](https://leetcode-cn.com/problems/er-cha-shu-de-shen-du-lcof/)思路，计算出左右子树的高度，我们只需要判定左子树高度减去右子树高度的绝对值是否大于一就可以知道当前判定的树是否为平衡二叉树。这里唯一难想的就是如何将int的返回值转换为题目要求的boolean返回值。这里我们采用自底向上的思路，判定每个子树是否为平衡二叉树，如果左子树高度减去右子树高度的绝对值大于一，证明当前子树不是平衡二叉树，我们返回一个特定的值，给上层判定提供信息说你的子树已经不是平衡二叉树了，这里选用-1来传递信息。

具体代码如下：

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution {
     public boolean isBalanced(TreeNode root) {
       	//如果root为空，那肯定是平衡二叉树
        if (root == null) return true;
       	//如果返回值不等于-1，证明所有子树都是平衡二叉树
        return dfs(root) != -1;
    }

    int dfs(TreeNode node) {
        if (node == null) return 0;
        int left = dfs(node.left);
        int right = dfs(node.right);
      	//如果左右子树高度等于-1，证明子结构里面有非平衡二叉树，我们需要将-1向上传递
        if (left == -1 || right == -1 || Math.abs(left - right) > 1) {
            return -1;
        }
        return Math.max(left, right) + 1;
    }
}
```


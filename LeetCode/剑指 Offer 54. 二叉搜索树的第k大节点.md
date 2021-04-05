---
zmathjax: true
toc: true
categories:
 - LeetCode
tags:
 - 刷题笔记
---

#### [剑指 Offer 54. 二叉搜索树的第k大节点](https://leetcode-cn.com/problems/er-cha-sou-suo-shu-de-di-kda-jie-dian-lcof/)

给定一棵二叉搜索树，请找出其中第k大的节点。

<!--more-->

**示例 1:**

```
输入: root = [3,1,4,null,2], k = 1
   3
  / \
 1   4
  \
   2
输出: 4
```

**示例 2:**

```
输入: root = [5,3,6,2,4,null,null,1], k = 3
       5
      / \
     3   6
    / \
   2   4
  /
 1
输出: 4
```

**限制：**

```
1 ≤ k ≤ 二叉搜索树元素个数
```

来源：力扣（LeetCode）
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

### 题解：

本题一开始我绕了弯路，我一开始的想法是通过维护一个小顶堆，堆的大小为k，通过遍历二叉树，如果堆大小不足k，直接往进添加结点；如果堆大小为k，则比较当前结点值和堆顶结点值，如果当前结点值大于堆顶结点值，则将堆顶结点弹出，将当前结点加入小顶堆，这样最后直接返回堆顶元素的值即可。

很显然，上面思路绕了很大的弯路，需要遍历完整个二叉搜索树，没有利用到二叉搜索树中序遍历升序的特性，由于要找第k大的元素，我们可以直接逆中序遍历二叉树，设置一个counter用来记录当前是第几个结点，如果counter等于k，则直接返回即可。

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
    int counter;
    int result;

    public int kthLargest(TreeNode root, int k) {
        inOrder(root, k);
        return result;
    }

    private void inOrder(TreeNode root, int k) {
        if (root == null)
            return;
        inOrder(root.right, k);
        if (++counter == k) {
            result = root.val;
            return;
        }

        inOrder(root.left, k);
    }
}
```




---
zmathjax: true
toc: true
categories:
 - LeetCode
tags:
 - 刷题笔记
---

#### [剑指 Offer 34. 二叉树中和为某一值的路径](https://leetcode-cn.com/problems/er-cha-shu-zhong-he-wei-mou-yi-zhi-de-lu-jing-lcof/)

输入一棵二叉树和一个整数，打印出二叉树中节点值的和为输入整数的所有路径。从树的根节点开始往下一直到叶节点所经过的节点形成一条路径。

示例: 
给定如下二叉树，以及目标和` sum = 22`，

<!--more-->

```
              5
             / \
            4   8
           /   / \
          11  13  4
         /  \      \
        7    2      1
```

返回：

```
[
   [5,4,11,2],
   [5,8,4,5]
]
```

**提示：**

1. `节点总数 <= 10000`

来源：力扣（LeetCode）
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

### 题解：

本题思想就是深度优先搜索遍历，只不过在遍历的时候需要判断当前路径上的结点数值之和是否等于`sum`。

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
    //存放结果
    List<List<Integer>> result = new ArrayList<>();
    
    public List<List<Integer>> pathSum(TreeNode root, int sum) {
        //临时链表，用来存放满足条件的一条路径
        LinkedList<Integer> temp = new LinkedList<>();
        dfs(root, sum, temp);
        return result;
    }

    void dfs(TreeNode node, int sum, LinkedList<Integer> temp) {
        //当结点为空时返回
        if (node == null)
            return;

        //如果不为空，将当前结点的值添加到临时链表中，同时sum减去当前结点的值
        temp.add(node.val);
        sum = sum - node.val;

        //如果当前结点时叶子结点且该路径数值之和等于sum，那么将该条满足条件的路径添加到result数组中
        if (node.left == null && node.right == null && sum == 0) {
            result.add(new LinkedList<>(temp));
            temp.pollLast();
            return;
        }

        //递归遍历左右子树
        dfs(node.left, sum, temp);
        dfs(node.right, sum, temp);
        //最后需要将当前结点弹出以进行下条路径的遍历
        temp.pollLast();
    }
}
```


---
zmathjax: true
toc: true
categories:
 - LeetCode
tags:
 - 刷题笔记
---

#### [剑指 Offer 07. 重建二叉树](https://leetcode-cn.com/problems/zhong-jian-er-cha-shu-lcof/)

输入某二叉树的前序遍历和中序遍历的结果，请重建该二叉树。假设输入的前序遍历和中序遍历的结果中都不含重复的数字。

<!--more-->

例如，给出

```
前序遍历 preorder = [3,9,20,15,7]
中序遍历 inorder = [9,3,15,20,7]
```

返回如下的二叉树：

    	3
       / \
      9   20
        /  \
       15   7
**限制：**

```
0 <= 节点个数 <= 5000
```

来源：力扣（LeetCode）
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。

### 题解：

本题还是构造二叉树，基本思想就是根据`preorder`数组确定当前根节点的值，然后在`inorder`中寻找当前根节点值的位置，其左边为左子树，右边为右子树。这里需要注意的就是`preorder`递归区间的生成，我们可以依据`inorder`中根节点的索引来判断，左子树就是`[preLeft + 1, preLeft + leftSize]`，右子树就是`[preLeft + leftSize + 1, preRight]`，最终返回`node`即可。

具体代码如下：

```java
class Solution {
    public TreeNode buildTree(int[] preorder, int[] inorder) {
        return build(preorder, 0, preorder.length - 1, inorder, 0, inorder.length - 1);
    }

    TreeNode build(int[] preorder, int preLeft, int preRight, int[] inorder, int inLeft, int inRight) {
        if (preLeft > preRight)
            return null;

        int rootVal = preorder[preLeft];
        int index = -1;
        for (int i = inRight; i >= inLeft; i--) {
            if (inorder[i] == rootVal) {
                index = i;
                break;
            }
        }

      	 //用以确定区间
        int leftSize = index - inLeft;

        TreeNode node = new TreeNode(rootVal);
      	
        node.left = build(preorder, preLeft + 1, preLeft + leftSize, inorder, inLeft, index - 1);
        node.right = build(preorder, preLeft + leftSize + 1, preRight, inorder, index + 1, inRight);

        return node;
    }
}
```


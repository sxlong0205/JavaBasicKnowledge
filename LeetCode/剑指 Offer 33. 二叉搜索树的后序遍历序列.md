---
zmathjax: true
toc: true
categories:
 - LeetCode
tags:
 - 刷题笔记
---

#### [剑指 Offer 33. 二叉搜索树的后序遍历序列](https://leetcode-cn.com/problems/er-cha-sou-suo-shu-de-hou-xu-bian-li-xu-lie-lcof/)

输入一个整数数组，判断该数组是不是某二叉搜索树的后序遍历结果。如果是则返回 `true`，否则返回 `false`。假设输入的数组的任意两个数字都互不相同。

<!--more-->

参考以下这颗二叉搜索树：

```
     5
    / \
   2   6
  / \
 1   3
```

示例1:

```shi l
输入: [1,6,3,2,5]
输出: false
```

示例2:

```
输入: [1,3,2,6,5]
输出: true
```

**提示：**

1.  `数组长度 <= 1000`

来源：力扣（LeetCode）
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

### 题解：

本题我们可以从构建二叉树的角度出发，想想利用中序和后序遍历构建二叉树的过程。此题可以类比该过程，后序遍历数组最后一个元素是该二叉树的根结点，第一个大于根结点的数值，到根结点前一个数值是该二叉搜索树的右子树，第一个大于根结点数值的前面就是该树的左子树。我们只需要判断在右子树中有没有小于根结点的数值，如果有则不满足二叉搜索树的条件(这里只判断右子树是因为我们在寻找第一个大于根结点数值的时候，无形之中已经判断了所有前面的数值小于根结点)。递归遍历所有子树即可判断出该树是不是二叉搜索树。

具体代码如下：

```java
class Solution {
    public boolean verifyPostorder(int[] postorder) {
        return postOder(postorder, 0, postorder.length - 1);
    }

    private boolean postOder(int[] postorder, int begin, int end) {
      	//begin大于end说明该子区间所有数均满足要求
        if (begin >= end)
            return true;

        int mid = begin;
      	//寻找第一个大于根结点的数值
        while (postorder[mid] < postorder[end]) {
            mid++;
        }
      	
        int pointer2 = mid;
      	//判断右子区间中是否有数值小于根结点数值
        while (pointer2 < end) {
            if (postorder[pointer2] < postorder[end]) {
                return false;
            }
            pointer2++;
        }

      	//递归判断左子树和右子树是否满足条件
        return postOder(postorder, begin, mid - 1) && postOder(postorder, mid, end - 1);
    }
}
```


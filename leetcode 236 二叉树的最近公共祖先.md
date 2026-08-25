# leetcode 236 二叉树的最近公共祖先
这题可以这样考虑。我们在左子树和右子树里找结点`p`和`q`。那么就会有几种情况：

- `p`和`q`在两棵不同子树里。那么说明它们最近公共祖先就是`root`。
- `p`和`q`在相同的子树里。比如说他们都在左子树里，那么他们的最近公共祖先一定也在左子树。递归到左子树继续搜索。

那么我们可以这样规定函数的返回值：

- 如果`root`树里只有`p`或者`q`，那就返回`p`或者`q`。
- 如果`p`或者`q`都有，那就返回它们的最近公共祖先。这是一定可以做到的。因为`p`和`q`如果在同一棵子树，就会在那棵子树里继续找，这样找下去，一定会出现`p`和`q`在不同子树的情况。于是最近公共祖先就找到了。
- 如果都没有，就返回`NULL`。

```c++
class Solution {
public:
    TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
        if(root == NULL || root == p || root == q) return root;
        // root 是空，或者找到了 p，或者找到了 q

        TreeNode* left = lowestCommonAncestor(root->left, p, q);	// 找左子树
        TreeNode* right = lowestCommonAncestor(root->right, p, q);	// 找右子树

        if(left && right) return root;	
        // 如果两个子树都有返回值，说明一棵树是 p，一棵树是 q。那答案就是root
        if(right == NULL) return left; // 右边什么都没有，答案就是左子树查找结果
        if(left == NULL) return right; // 左边什么也没有，答案就是右子树查找结果

        return NULL;	// 什么也没找到，返回 NULL
    }
};
```

时间复杂度是<img src="./assets/formulas/formula-387008096a41.svg" alt="O(n)">。每个结点最多访问一次，每次访问的工作量是<img src="./assets/formulas/formula-4a137b861e8d.svg" alt="O(1)">。

# leetcode 543 二叉树的直径

对于每个结点，统计经过它的直径。计算方法是`左子树深度 + 右子树深度 + 2`。

递归求每个结点左右子树的最大深度，同时用一个全局变量维护最大直径。

递归过程中更新全局最大值。注意代码里的深度按边数计算，所以空子树深度初始化为`-1`。

```c++
class Solution {
    int ans = 0;

    int depth(TreeNode* root){
        int res = 0, lh = -1, rh = -1;

        if(root->left) lh = depth(root->left);
        if(root->right) rh = depth(root->right);

        res = max(lh, rh) + 1;
        ans = max(ans, lh + rh + 2);

        return res;
    }
public:
    int diameterOfBinaryTree(TreeNode* root) {
        depth(root);

        return ans;
    }
};
```

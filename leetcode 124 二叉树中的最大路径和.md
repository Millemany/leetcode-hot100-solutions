# leetcode 124 二叉树中的最大路径和

dfs。`dfs(root)`计算出经过`root`的最大路径，然后更新全局变量最优解。

经过`root`的最大路径，就是

```c++
从root->left出发到树叶的最大路径 + root->val + 从root->right出发到树叶的最大路径
```

而某一个结点到树叶的最大路径，计算方法就是

```c++
root到树叶的最大路径 = max(root->left到树叶的最大路径, root->right到树叶的最大路径)
```

这可以作为 dfs 的返回值进行递归计算。

时间复杂度$O(n)$，空间复杂度$O(n)$。

```c++
class Solution {
public:
    int dfs(TreeNode* root, int& ans){
        if(root == nullptr) return 0;

        int left_val = max(0, dfs(root->left, ans));
        int right_val = max(0, dfs(root->right, ans));

        ans = max(ans, left_val + right_val + root->val);

        return max(left_val + root->val, right_val + root->val);
    }

    int maxPathSum(TreeNode* root) {
        int res = INT_MIN;
        dfs(root, res);
        return res;
    }
};
```

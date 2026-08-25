# leetcode 98 验证二叉搜索树

递归。维护每个结点允许的取值区间`(low, high)`。

进入左子树时，上界变成当前结点值；进入右子树时，下界变成当前结点值。区间必须是开区间，因为二叉搜索树不能有相等的结点。

边界要用`long long`，防止结点值本身等于`INT_MIN`或`INT_MAX`。

```c++
class Solution {
    bool work(TreeNode* node, long long low,long long high){
        if(node == nullptr) return true;

        if(node->val <= low || node->val >= high) return false;
        return work(node->left, low, node->val) && work(node->right, node->val, high);
    }
public:
    bool isValidBST(TreeNode* root) {
        return work(root, LONG_MIN, LONG_MAX);
    }
};
```

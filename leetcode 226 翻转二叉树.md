# leetcode 226 翻转二叉树

递归翻转左右子树，然后交换当前结点的左右孩子。

时间复杂度<img src="./assets/formulas/formula-387008096a41.svg" alt="O(n)">，递归空间复杂度<img src="./assets/formulas/formula-387008096a41.svg" alt="O(n)">。

```c++
class Solution {
public:
    TreeNode* invertTree(TreeNode* root) {
        if(root){
            TreeNode* l = invertTree(root->left);
            TreeNode* r = invertTree(root->right);	// 左右树递归
            root->right = l, root->left = r; 		// 翻转
        }
        return root;
    }
};
```

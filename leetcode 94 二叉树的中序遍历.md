# leetcode 94 二叉树的中序遍历

迭代中序遍历。

先不断向左走并把沿途结点压栈。走到空结点后弹出栈顶并记录答案，再切换到该结点的右子树。

时间复杂度$`O(n)`$，空间复杂度$`O(n)`$。

```c++
class Solution {
public:
    vector<int> inorderTraversal(TreeNode* root) {
        vector<int> res;
        stack<TreeNode*> st;

        TreeNode* cur = root;
        while(cur || st.size()){
            while(cur){  // 处理左子树：一直左走，全部压栈
                st.push(cur);
                cur = cur->left;
            }

            cur = st.top();
            st.pop();   // 当前弹出的结点就是左子树已经全部处理完的结点
            res.push_back(cur->val);

            cur = cur->right;   // 切换到右树
        }
        return res;
    }
};
```

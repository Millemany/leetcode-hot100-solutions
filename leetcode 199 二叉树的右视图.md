# leetcode 199 二叉树的右视图

实际上就是返回每一层的最右侧值。层序遍历可以解决。

```c++
class Solution {
public:
    vector<int> rightSideView(TreeNode* root) {
        queue<TreeNode*> q;
        vector<int> res;

        if(root){
            q.push(root);
            int cnt = q.size();

            while(q.size()){
                TreeNode* t = q.front();
                q.pop();
                cnt --;

                if(t->left) q.push(t->left); 
                if(t->right) q.push(t->right);

                if(cnt == 0){
                    res.push_back(t->val);
                    cnt = q.size();
                }
            }
        }
        return res;
    }
};
```


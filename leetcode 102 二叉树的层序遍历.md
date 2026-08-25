# leetcode 102 二叉树的层序遍历

BFS。用哈希表记录每个结点所在层数，当队首结点的层数和当前结点不同时，说明当前层已经遍历完，把这一层的答案加入结果。

时间复杂度<img src="./assets/formulas/formula-387008096a41.svg" alt="O(n)">，空间复杂度<img src="./assets/formulas/formula-387008096a41.svg" alt="O(n)">。

```c++
class Solution {
public:
    vector<vector<int>> levelOrder(TreeNode* root) {
        vector<vector<int>> res;
        vector<int> ans;

        if(!root) return res;

        unordered_map<TreeNode*, int> mp;
        mp[root] = 0;

        queue<TreeNode*> q;
        q.push(root);

        while(q.size()){
            TreeNode* t = q.front();
            q.pop();
            ans.push_back(t->val);

            if(q.empty() || mp[t] != mp[q.front()]){ // 当前层遍历完了
                res.push_back(ans);
                ans.clear();
            }

            if(t->left){
                q.push(t->left);
                mp[t->left] = mp[t] + 1;	// 记录当前的层数
            }
            if(t->right){
                q.push(t->right);
                mp[t->right] = mp[t] + 1;
            }
        }
        return res;
    }
};
```

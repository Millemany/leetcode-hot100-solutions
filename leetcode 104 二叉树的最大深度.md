# leetcode 104 二叉树的最大深度

层序遍历。每次先记录当前队列长度，只处理这一层的结点。处理完一层后，深度加一。

和普通 BFS 的区别在于，一次把一层的结点全部弹出。用`sz`记录这一层的结点的数量。

时间复杂度<img src="./assets/formulas/formula-387008096a41.svg" alt="O(n)">，空间复杂度<img src="./assets/formulas/formula-387008096a41.svg" alt="O(n)">。

```c++
class Solution {
public:
    int maxDepth(TreeNode* root) {
        if(!root) return 0;

        queue<TreeNode*> q;
        q.push(root);
        int res = 0;

        while(q.size()){
            int sz = q.size();
            while(sz){
                TreeNode* node = q.front();
                q.pop();
                if(node->left) q.push(node->left);
                if(node->right) q.push(node->right);
                sz --;
            }
            res ++;
        }

        return res;
    }
};
```

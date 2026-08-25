# leetcode 101 对称二叉树

用队列成对存放需要互相比较的结点。

每次取出两个结点。如果只有一个为空或者值不同，就不是对称树。继续入队时，要按照`左树的左孩子和右树的右孩子`、`左树的右孩子和右树的左孩子`成对入队。

```c++
class Solution {
public:
    bool isSymmetric(TreeNode* root) {
        if(!root) return true;
        queue<TreeNode*> q;
        q.push(root->left), q.push(root->right);

        while(q.size()){
            TreeNode* a = q.front(); q.pop();
            TreeNode* b = q.front(); q.pop();

            if((!a && b) || (a && !b)) return false;
            if(a && b){
                if(a->val != b->val) return false;
                q.push(a->left), q.push(b->right); // 一次入队两个结点
                q.push(a->right), q.push(b->left);
            }
        }
        return true;
    }
};
```

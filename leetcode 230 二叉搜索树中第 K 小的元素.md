# leetcode 230 二叉搜索树中第 K 小的元素

1. 中序遍历。

   使用中序遍历搜索，搜索到的第 k 个元素就是答案。

   这里可以用递归写法，也可以不用。这里给出不用递归，自己维护栈的写法。

   ```c++
   class Solution {
   public:
       int kthSmallest(TreeNode* root, int k) {
           stack<TreeNode*> stk;
           
           while(root || stk.size()){
               while(root){
                   stk.push(root);
                   root = root->left;	// 左节点压栈
               }
               
               root = stk.top();
               stk.pop();	// 弹出当前处理的结点
               
               k --;
               if(k == 0) return root->val;
               
               root = root->right;	// 转到右节点
           }
           
           return -1;
       }   
   };
   ```

2. 迭代

   如果提前能够知道某棵子树的结点数量，那么我们就可以判断：

   - 如果`root->left`子树结点数量等于`k - 1`，那么`root`就是排名第 k 的结点。
   - 如果`root->left`子树结点数量大于`k - 1`，说明第 k 小的元素在`root->left`这棵树里面。此时就有`root = root->left`。
   - 如果`root->left`子树结点数量小于`k - 1`，说明第 k 小的元素在`root->right`这棵树里面，并且是右子树里面排名第`k - 左子树结点数 - 1`的元素。所以就有`root = root->right`，且`k = k - mp[root->left] - 1`。

   ```c++
   class Solution {
       unordered_map<TreeNode*, int> mp;
   
       void work(TreeNode* v){
           if(!v){
               mp[v] = 0;
               return;
           }
           
           work(v->left), work(v->right);
           mp[v] = mp[v->left] + mp[v->right] + 1;
       }
   public:
       int kthSmallest(TreeNode* root, int k) {
           work(root);
           
           while(root){
               if(mp[root->left] == k - 1) return root->val;
               else if(mp[root->left] > k - 1) root = root->left;
               else{
                   k = k - mp[root->left] - 1;
                   root = root->right;
               } 
           }
           return -1;
       }   
   };
   ```

   
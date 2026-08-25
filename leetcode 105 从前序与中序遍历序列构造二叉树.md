# leetcode 105 从前序与中序遍历序列构造二叉树

1. 递归

   因为`preorder`和`inorder`都没有重复元素，所以可以采取递归做法。

   前序遍历序列的结构是 根 + 左子树 + 右子树，中序遍历序列结构是 左子树 + 根 + 右子树。

   所以前序遍历序列第一个元素就是根，然后在中序序列里找，找到根之后，左右子树的元素就都确定了。

   确定了左右子树的结点数量，就可以确定前序里面的左右子树。最后递归就可以了。

   时间和空间复杂度都是$O(n)$。

   ```c++
   class Solution {
       TreeNode* build(vector<int>& preorder, int pl, int pr, vector<int>& inorder, int il, int ir){
           if(pl > pr || il > ir) return nullptr;
   
           int k = il;
           while(inorder[k] != preorder[pl]) k ++;	// 	确定中序里根的位置
   
           TreeNode* root = new TreeNode(preorder[pl]);
           int left_num = k - il, right_num = ir - k;	// 左右子树结点数量
           root->left = build(preorder, pl + 1, pl + left_num, inorder, il, k - 1);
           root->right = build(preorder, pl + left_num + 1, pr, inorder, k + 1, ir);
   
           return root;
       }
   public:
       TreeNode* buildTree(vector<int>& preorder, vector<int>& inorder) {
           int n = preorder.size();
           return build(preorder, 0, n - 1, inorder, 0, n - 1);
       }
   };
   ```

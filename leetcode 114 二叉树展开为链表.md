# leetcode 114 二叉树展开为链表

1. 递归

   - 分别递归左子树和右子树。
- 找到左子树的最后一个结点。
   - 把右子树插到左子树屁股后面，左子树变成右子树。

   时间复杂度<img src="./assets/formulas/formula-387008096a41.svg" alt="O(n)">。空间复杂度也是<img src="./assets/formulas/formula-387008096a41.svg" alt="O(n)">。

   代码暂略


2. 空间复杂度<img src="./assets/formulas/formula-4a137b861e8d.svg" alt="O(1)">的做法（不算递归空间）

   这种做法的具体流程是，对于每个结点：

   - 找到左子树的最右结点
   - 把右子树插到左树最右结点的屁股后面
   - 把左树挪到右树，左树置空
   - 当前遍历结点变成右孩子
   
   这种做法就是每次把一个结点整理好，然后再整理它的孩子。
   
   ```c++
   class Solution {
   public:
       void flatten(TreeNode* root) {
           if(root){
               TreeNode* t = root->left;
               while(t && t->right) t = t->right;	// 先找到左子树的最右结点
   
               if(t){	// t 不空就说明左子树不空
                   t->right = root->right;
                   root->right = root->left;
                   root->left = nullptr;
               }
               flatten(root->right);
           }
       }
   };
   ```
   
   


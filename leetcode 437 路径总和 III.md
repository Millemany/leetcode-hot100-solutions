# leetcode 437 路径总和 III

1. 递归：自顶向下

   这种递归类似于dp的思路。某棵树中和为固定值的路径`pathSum(root, targetSum)`，可以分为两部分：

   - 路径中有当前根`root`
   - 路径中没有当前根`root`

   没有`root`的路径数可以用递归表示，用`pathSum(root->left, targetSum) + pathSum(root->right, targetSum)`即可。

   有`root`的路径数可以另写一个递归函数`dfs(root, targetSum)`求。求法也很简单，就是

   `dfs(root, targetSum) = (root->val == targetSum) + dfs(root->left, targetSum - root->val) + dfs(root->right, targetSum - root->val)`

   总结起来，就是

   `pathSum(root, targetSum) = dfs(root, targetSum) + pathSum(root->left, targetSum) + pathSum(root->right, targetSum)`

   这是自顶向下的方法，因此时间复杂度最差是$O(n^2)$。如果当前的树退化成链表的话，每dfs一个结点，就要遍历一遍它下面的所有结点，每dfs一次就是$O(n)$。

   ```c++
   class Solution {
       int dfs(TreeNode* node, long long sum){ // 一定要注意这里是 long long
           if(node == nullptr) return 0;
   
           return (node->val == sum) + dfs(node->left, sum - node->val) + dfs(node->right, sum - node->val);
       }
   public:
       int pathSum(TreeNode* root, int targetSum) {
           if(root == nullptr) return 0;
   
           return dfs(root, targetSum) + pathSum(root->left, targetSum) + pathSum(root->right, targetSum);
       }
   };
   ```

2. 递归：自底向上

   上面说的`dfs(node, sum)`意思是以`node`为最上层结点，和为`sum`的路径数量。

   这里还有一种方法，让`dfs(node, targetSum)`表示和为`targetSum`的，且最下层结点在**以`node`为根的子树里面**的路径数量。

   那么就有`dfs(node, targetSum) = dfs(node->left, targetSum) + dfs(node->right, targetSum) + 以node结尾的路径数`

   下面考虑怎么求出以`node`结尾的，且和为`targetSum`的路径数量。这里可以考虑用前缀和的方法。

   用一个参数`sum`维护从根结点到`node`的结点之和。那么以`node`为结尾的路径数，就是`node`祖宗结点里前缀和为`sum - targetSum`的数量。这个前缀和可以用哈希表维护。

   这种方法时间复杂度是$O(n)$。

   ```c++
   class Solution {
       unordered_map<long long, int> mp;
       // mp[sum] 表示当前结点位置，前缀和为 sum 的路径个数
   
       int dfs(TreeNode* node, long long sum, int targetSum){
           if(node == nullptr) return 0;
   
           int res = 0;
   
           sum += node->val;	// 计算当前的前缀和
           res += mp[sum - targetSum];	// 累加结果
   
           mp[sum] ++;	// 前缀和计数器加一
           res += dfs(node->left, sum, targetSum) + dfs(node->right, sum, targetSum);
           mp[sum] --;	// 维护现场，把当前结点的前缀和计数去掉
   
           return res;
       }
   public:
       int pathSum(TreeNode* root, int targetSum) {
           mp[0] = 1;	// 如果 root 值和 targetSum 一样，必须能够计算。所以要初始化 mp[0] = 1
           return dfs(root, 0, targetSum);
       }
   };
   ```

   

   


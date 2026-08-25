# leetcode 300 最长递增子序列

1. DP

   用`f[i]`表示以`i`结尾的最长递增子序列的长度。所以答案就是`max(f[0], f[1], ..., f[n - 1])`。

   时间复杂度是$O(n^2)$。

   ```c++
class Solution {
   public:
    int lengthOfLIS(vector<int>& nums) {
           int n = nums.size();
           vector<int> f(n, 1);
   
           int res = 1;
   
           for(int i = 1; i < n; i ++){
               for(int j = 0; j < i; j ++){
                   if(nums[j] < nums[i]) f[i] = max(f[i], f[j] + 1);
               }
               res = max(res, f[i]);
           }
   
           return res;
       }
   };
   ```

2. 贪心 + 二分

   维护一个`tail`数组。`tail[i]`表示长度为`i`的最长递增子序列的最小结尾值。

   比如`nums`数组是`1, 5, 2, ...`。从前往后遍历。

   遍历到`1`的时候，此时有`tail = [1]`（下标从 1 开始）。

   遍历到`3`的时候，有`tail = [1, 5]`。

   遍历到`2`的时候，由于`1, 2`的结尾值`2`比`1, 5`的结尾值`5`小，因此变成`tail = [1, 2]`。这意思是说，虽然`1, 5`和`1, 2`都是目前最长的递增子序列，但我们选择维护`1, 2`而非`1, 5`。因为前者结尾更小，更有潜力向后拓展。

   此后遍历的时候，**二分**找到`tail`里面大于等于`nums[i]`的最小值，然后顶替它就可以了。

   最后答案就是`tail`数组的长度。

   时间复杂度是$O(n\log n)$。

   ```c++
   class Solution {
   public:
       int lengthOfLIS(vector<int>& nums) {
           int n = nums.size();
           vector<int> tail;
           tail.push_back(INT_MIN);	
           // 为了让 tail 有效的下标从 1 开始，先放进一个最小值
   
           for(int i = 0; i < n; i ++){
               int l = 0, r = tail.size() - 1;
               while(l < r){
                   int mid = (l + r) >> 1;
                   if(tail[mid] < nums[i]) l = mid + 1;
                   else r = mid;
               }
               if(tail[r] >= nums[i]) tail[r] = nums[i];
               else tail.push_back(nums[i]);
           }
   
           return tail.size() - 1; // 不能算预先放进去的最小值
       }
   };
   ```

   

   
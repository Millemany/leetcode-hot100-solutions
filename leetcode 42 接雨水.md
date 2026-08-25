# leetcode 42 接雨水

1. DP

   考虑每个格子。每个格子存水的高度是他左边最高点和右边最高点的最小值。因此可以维护两个数组`lefth`和`righth`。`lefth[i]`和`righth[i]`分别表示`i`左边的最大值和右边的最大值。

   那么在**当前格子能存水的情况下**，`min(lefth[i], right[i]) - height[i]`的值就是这个格子存水的数量。如果这个值是负的，说明就不能存水。因此真正存水的数量是`max(min(lefth[i], right[i]) - height[i], 0)`。

   求解`lefth`和`righth`都可以用DP完成。也就是`lefth[i] = max(lefth[i - 1], height[i - 1])`。`righth`同理。

   时间复杂度是$`O(n)`$。

   ```c++
   class Solution {
   public:
       int trap(vector<int>& height) {
           const int N = height.size();
   
           vector<int> lefth(N, 0), righth(N, 0);
           
           for(int i = 1; i < N - 1; i ++){
               lefth[i] = max(lefth[i - 1], height[i - 1]);
           }
           for(int i = N - 2; i >= 1; i --){
               righth[i] = max(righth[i + 1], height[i + 1]);
           }
           
           int res = 0;
           for(int i = 1; i < N - 1; i ++){
               res += max(min(lefth[i], righth[i]) - height[i], 0);
           }
           return res;
       }
   };
   ```

2. 单调栈

   对于一个独立的水坑，计算其容积有两种方法。上面说的dp是纵向切割，也就是每个单元格纵向能积攒多少高度的水。此外还可以横向切割，也就是看每个深度能积攒多宽的水。

   从这个角度看，想要知道每个水坑的容积，就要确定其左右边界。

   **左边界**：观察可以看出，对于每个位置，其所在水坑的左边界就是它左边所有的值中，比它大的值里离它最近的一个。单调栈正好可以解决这种问题。也就是说，维护一个递减的单调栈，栈顶元素`stk[top]`的下一个值`stk[top - 1]`就是`stk[top]`所处水坑的左边界。

   **右边界**：右边界也是它右边所有值里面，比它大且离它最近的一个。对于`stk[top]`来说，这个值就是能够让它弹出栈的值。也就是说，如果当前元素`height[i]`比`height[stk[top]]`更大，就要把`stk[top]`弹出。这时候位置`i`就是`stk[top]`所在水坑的右边界。`stk[top]`所在的水域体积即可算出。

   注意，为了方便算出水域的宽度，单调栈里存的是下标，而不是高度值本身。

   具体来说，遍历每个元素，讨论它是不是右边界：

   ```c++
   for i in [0, height.size() - 1]:
   	while i是右边界:
   		弹栈
   		计算水坑体积
      	i 入栈
   ```

   时间复杂度是$`O(n)`$。

   完整代码如下：

   ```c++
   class Solution {
   public:
       int trap(vector<int>& height) {
       	stack<int> stk;
           
           int res = 0;
           for(int i = 0; i < height.size(); i ++){
               while(stk.size() && height[i] > height[stk.top()]){
                   // 如果 i 是右边界，起码栈不能是空的，并且高度大于栈顶元素高度
                   int pos = stk.top();
                   stk.pop();
                   
                   if(stk.empty()) break;
                   // 弹出一个元素栈就空了，说明没有左边界
                   // 说明 i 也不是右边界，直接退出
                   
                   int li = stk.top();
                   int h = min(height[li], height[i]) - height[pos];
                   int w = i - li - 1;
                   
                   res += h * w;
               }
         		stk.push(i);
           }
           
           return res;
       }
   };
   ```

3. 双指针

   双指针方法可以看成DP方法的加强。

   双指针算法的核心在于：当前位置的雨水由左右最高柱子的较小值决定，因此始终移动最高柱子较小的一侧。因为这一侧的雨水量已经可以确定，而另一侧即使以后出现更高的柱子，也不会影响这一侧的答案。

   比如对于一对`l`和`r`，`l`及其左侧最高值是`h[l]`，`r`及其右侧最高值是`h[r]`，且`h[l] < h[r]`，那么可知如果`height[l + 1] < h[l]`，则`l + 1`处的雨水高度一定是`h[l]`。

   因为根据DP方法的结论，对于`l + 1`这个位置，它左侧最大高度就是`h[l]`。而它右侧最大高度绝不会小于`h[r]`。因此它两边最大高度的最小值就是`h[l]`。

   于是这题可以使用双指针。如果`h[l] < h[r]`，那么可确定`l + 1`位置雨水情况，同时`l`右移一步，继续判断。如果`h[r]`更小，那就确定`r - 1`雨水情况，同时`r`左移一步。

   ```c++
   class Solution {
   public:
       int trap(vector<int>& height) {
       	int res = 0;
           
           int l = 0, r = height.size() - 1;
           int hl = height[l], hr = height[r];
          	while(l < r){
               if(hl < hr){
                   if(height[l + 1] < hl) res += hl - height[l + 1];
                   else hl = height[l + 1];
                   
                   l ++;
               }
               else{
                   if(height[r - 1] < hr) res += hr - height[r - 1];
                   else hr = height[r - 1];
                   
                   r --;
               }
           }
           return res;
       }
   };
   ```

   

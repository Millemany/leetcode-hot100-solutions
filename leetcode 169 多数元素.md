# leetcode 169 多数元素

Boyer-Moore 投票算法。

维护两个变量`x`和`cnt`。初始两个变量都是`0`。依次遍历每个元素：

- 如果`cnt == 0`，则令`x = nums[i]`。
- 反之，
  - 若`x == nums[i]`，则`cnt ++`；
  - 若`x != nums[i]`，则`cnt --`。

遍历结束之后的`x`就是答案。

这个算法的思想就是，如果答案是`a`，那么让数组里`a`和`非a`元素一一抵消，剩下的元素就是答案`a`。

具体证明略。

时间复杂度是$`O(n)`$。

```c++
class Solution {
public:
    int majorityElement(vector<int>& nums) {
        int x = 0, cnt = 0;
        for(auto t: nums){
            if(cnt == 0){
                x = t, cnt = 1;
            }
            else{
                if(x == t) cnt ++;
                else cnt --;
            }
        }
        return x;
    }
};
```


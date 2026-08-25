# leetcode 53 最大子数组和

跟leetcode 560几乎完全一样，甚至更简单。就是前缀和问题。

维护一个变量`min_pre`表示当前得到的最小前缀和，另一个变量`pre`表示当前位置算出来的前缀和。那么当遍历到下一个位置`i`的时候，可以算出新前缀和`pre = pre + nums[i]`，然后`res = max(res, pre - min_pre)`就可以更新最大子数组和。最后`min_pre = min(min_pre, pre)`更新最小前缀和即可。

```c++
class Solution {
public:
    int maxSubArray(vector<int>& nums) {
        int pre = 0, min_pre = 0;
        int res = -2e9;

        for(auto x: nums){
            pre += x;
            res = max(res, pre - min_pre);
            min_pre = min(min_pre, pre);
        }
        return res;
    }
};
```


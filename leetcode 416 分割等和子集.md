# leetcode 416 分割等和子集

01背包问题。从数组中能不能找出若干元素，其和为`sum / 2`。其中`sum`是`nums`里所有元素之和。

用`f[i, s]`表示前`i`个元素里能不能找出若干元素，其和为`s`。那么有：

```c++
f[i, s] = f[i - 1, s] || f[i - 1, s - nums[i]];
```

可以用滚动数组优化空间。时间复杂度<img src="./assets/formulas/formula-84614e269da7.svg" alt="O(mn)">，其中<img src="./assets/formulas/formula-c54a860e226a.svg" alt="m = \mathrm{sum}/2">。

```c++
class Solution {
public:
    bool canPartition(vector<int>& nums) {
        int sum = 0;
        for(auto t: nums) sum += t;
        if(sum % 2) return false;	// 和为奇数，一定没有答案

        vector<bool> f(sum / 2 + 1, false);
        f[0] = true;

        for(auto t: nums){
            for(int i = sum / 2; i >= t; i --){ // 从后往前遍历
                f[i] = f[i] || f[i - t];
            }
        }
        return f[sum / 2];
    }
};
```


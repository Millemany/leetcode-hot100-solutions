# leetcode 152 乘积最大子数组

用`f[i]`表示以`nums[i]`结尾的乘积最大值，`g[i]`表示以`nums[i]`结尾的乘积最小值，那么`f[i]`有可能下面几种情况：

- `nums[i] > 0`，且`f[i - 1] >= 1`。那么有`f[i] = f[i - 1] * nums[i]`
- `nums[i] > 0`，且`f[i - 1] <= 0`。那么有`f[i] = nums[i]`
- `nums[i] < 0`，且`g[i - 1] <= -1`。那么有`f[i] = g[i - 1] * nums[i]`
- `nums[i] < 0`，且`g[i - 1] >= 0`。那么有`f[i] = nums[i]`
- `nums[i] == 0`。则`f[i] = 0`

因此`f[i]`的取值就是`f[i - 1] * nums[i]`、`g[i - 1] * nums[i]`与`nums[i]`三种情况，并且是三种情况最大值。同样，`g[i]`的取值就是三者的最小值。

不断维护`f[i - 1]`和`g[i - 1]`就可以了，因此只用两个变量就可以解决问题。

时间复杂度是<img src="./assets/formulas/formula-387008096a41.svg" alt="O(n)">。

```c++
class Solution {
public:
    int maxProduct(vector<int>& nums) {
        int res = INT_MIN;

        int pmin = 1, pmax = 1;
        // pmin 就是前 i - 1 个元素的最小值
        // pmax 就是前 i - 1 个元素的最大值
        for(auto t: nums){
            int ans = max(t, max(pmin * t, pmax * t));
            res = max(res, ans);
            
            pmin = min(t, min(pmin * t, pmax * t));
            pmax = ans;
        }

        return res;
    }
};
```


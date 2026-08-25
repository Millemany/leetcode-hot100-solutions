# leetcode 238 除了自身以外数组的乘积

经典前缀和问题。但这里是前缀积和后缀积。维护一个前缀积数组`pre`和后缀积`pro`。其中

`pre[i] = nums[0] * nums[1] * ... *nums[i]`

`pro[i] = nums[i] * nums[i + 1] * ... * nums[n - 1]`

如果答案数组是`res`，那么就有`res[i] = pre[i - 1] * pro[i + 1]`

```c++
class Solution {
public:
    vector<int> productExceptSelf(vector<int>& nums) {
        int n = nums.size();
        vector<int> pre(n, 0), pro(n, 0);
        pre[0] = nums[0], pro[n - 1] = nums[n - 1];

        for(int i = 1; i < n; i ++){
            pre[i] = pre[i - 1] * nums[i];
            pro[n - i - 1] = pro[n - i] * nums[n - i - 1];
        }

        vector<int> res(n, 1);
        for(int i = 0; i < n; i ++){
            if(i) res[i] *= pre[i - 1];
            if(i < n - 1) res[i] *= pro[i + 1];
        }

        return res;
    }
};
```



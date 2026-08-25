# leetcode 560 和为 K 的子数组

前缀和是一个能够在$O(1)$时间内求出任意一个子数组元素之和的方法。令前缀和数组为`s[N]`，那么对于当前的元素`a[i]`，所有以它结尾的和为k的子数组`[j,i]`必然满足`s[i] - s[j - 1] == k`。所以我们只需要知道对于每个位置`i`，它前面有多少元素，其前缀和为`s[i] - k`就可以了。

如果遍历`i`之前的元素来求，那总时间复杂度是$O(n^2)$，可能还会超时。因此可以在求前缀和的**同时**维护一个`unordered_map<int, int> mp`，`mp[t]`表示在当前位置`i`前面有多少前缀和为`t`的元素，那么`mp[s[i] - k]`就是以`a[i]`结尾的目标子数组的个数。

```c++
class Solution {
public:
    int subarraySum(vector<int>& nums, int k) {
    	unordered_map<int, int> mp;
        mp[0] = 1;
        
        int res = 0;
        
        int s = 0; // 当前前缀和
        // 这题实际上不需要一个前缀和数组，因为求每个元素前缀和的同时就能把答案都算出来。
        for(auto x: nums){
            s += x;
            if(mp.count(s - k)) res += mp[s - k];
            mp[s] = mp.count(s) ? mp[s] + 1 : 1;
        }
        return res;
    }
};
```


# leetcode 1 两数之和

哈希表存放数字及其下标。

依次遍历元素，先查看`target - nums[i]`是否在哈希表里。若存在则直接返回两数下标，否则把当前数字和下标存在哈希表里。

可能会出现相同数字不同下标的情况。但因为答案只有两个数，所以相同的数字存一个位置就行了。

时间复杂度$`O(n)`$。

```c++
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        unordered_map<int, int> mp;

        int n = nums.size();
        for(int i = 0; i < n; i ++){
            int x = target - nums[i];
            if(mp.count(x)) return {i, mp[x]};

            mp[nums[i]] = i;
        }
        return {};
    }
};
```


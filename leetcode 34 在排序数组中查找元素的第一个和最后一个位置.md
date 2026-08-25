# leetcode 34 在排序数组中查找元素的第一个和最后一个位置

二分两遍，分别查找`>= target`的最小位置和`<= target`的最大位置。两个二分写法略有不同。

注意要判断空数组的情况。

时间复杂度$`O(\log n)`$。

```c++
class Solution {
public:
    vector<int> searchRange(vector<int>& nums, int target) {
        vector<int> res;
        res.push_back(-1), res.push_back(-1);
        int n = nums.size();
        
        int l = 0, r = n - 1;
        while(l < r){
            int mid = (l + r) >> 1;
            if(nums[mid] < target) l = mid + 1;
            else r = mid;
        }
        if(r < 0 || nums[r] != target) return res;	
        // r < 0 说明 nums 数组是空的。根本就不会二分
        
        res[0] = r;

        l = 0, r = n - 1;
        while(l < r){
            int mid = (l + r + 1) >> 1;
            if(nums[mid] <= target) l = mid;
            else r = mid - 1;
        }
        res[1] = r;
        
        return res;
    }
};
```


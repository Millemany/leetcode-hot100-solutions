# leetcode 35 搜索插入位置

先提前筛选出`target`不在`nums`包括区间里的情况，然后使用二分查找。

找的是`>=target`的最小值，因此注意二分的具体实现方法。

时间复杂度是$`O(\log n)`$。

```c++
class Solution {
public:
    int searchInsert(vector<int>& nums, int target) {
        if(target < nums.front()) return 0;
        if(target > nums.back()) return nums.size();

        int l = 0, r = nums.size() - 1;

        while(l < r){
            int mid = (l + r) >> 1;
            if(nums[mid] < target) l = mid + 1;
            else r = mid;
        }
        return r;
    }
};
```


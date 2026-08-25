# leetcode 153 寻找旋转排序数组中的最小值

参看 [leetcode 33](./leetcode 33 搜索旋转排序数组.md) 。本题是其前半部分内容。

 ```c++
class Solution {
public:
    int findMin(vector<int>& nums) {
        int n = nums.size();
        int l = 0, r = n - 1;

        while(l < r){
            int mid = (l + r) >> 1;
            if(nums[mid] >= nums[0]) l = mid + 1;
            else r = mid;
        }

        return nums[0] < nums[r] ? nums[0] : nums[r];
    }

};
 ```


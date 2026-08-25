# leetcode 15 三数之和

先排序，然后枚举三元组中最小的数`nums[i]`。用双指针查找和为`0 - nums[i]`的数。

因为`nums[i]`是最小值，所以令左指针`l = i + 1`，右指针`r = n - 1`。

如果`nums[l] + nums[r] < 0 - nums[i]`，则说明`nums[l]`永远不会是答案（因为当前的`nums[r]`已经是它能配对的最大值，此时`nums[l] + nums[r]`还是太小，说明没有能满足`nums[l]`的`nums[r]`存在了）。`l ++`。

如果`nums[l] + nums[r] > 0 - nums[i]`，则同理，`r --`。

如果`nums[l] + nums[r] == 0 - nums[i]`，则`l`和`r`都要变化，并且要变到不同的值上去。

这个思路和 [leetcode 11 盛最多水的容器](<./leetcode 11 盛最多水的容器.md>) 是类似的。

时间复杂度$`O(n^2)`$。

```c++
class Solution {
public:
    vector<vector<int>> threeSum(vector<int>& nums) {
        sort(nums.begin(), nums.end());
        int n = nums.size();
        vector<vector<int>> res;

        for(int i = 0; i < n && nums[i] <= 0; i ++){
            if(i && nums[i] == nums[i - 1]) continue;	// 跳过 nums[i] 相同的值
            int s = 0 - nums[i];

            int l = i + 1, r = n - 1;
            while(l < r){
                int t = nums[l] + nums[r];

                if(t < s) l ++;
                else if(t > s) r --;
                else{
                    res.push_back({nums[i], nums[l], nums[r]});

                    do{
                        l ++;
                    }while(l < n && nums[l] == nums[l - 1]);

                    do{
                        r --;
                    }while(r > i && nums[r] == nums[r + 1]);
                }
            }
        }
        return res;
    }
};
```

# leetcode 283 移动零

用`j`指向下一个非零元素应该放置的位置，初始`j = 0`。

遍历数组，遇到非零元素就和`nums[j]`交换，然后让`j`后移。这样非零元素的相对顺序不会改变，零会被逐渐交换到末尾。

时间复杂度<img src="./assets/formulas/formula-387008096a41.svg" alt="O(n)">，空间复杂度<img src="./assets/formulas/formula-4a137b861e8d.svg" alt="O(1)">。

```c++
class Solution {
public:
    void moveZeroes(vector<int>& nums) {
        for(int i = 0, j = 0; i < nums.size(); i ++){
            if(nums[i]){
                swap(nums[i], nums[j]);
                j ++;
            }
        }
    }
};
```

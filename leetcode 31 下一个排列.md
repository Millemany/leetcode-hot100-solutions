# leetcode 31 下一个排列

找规律 + 模拟。

举个例子，比如`1 4 9 5 3 2`，下一个排列就是`1 5 2 3 4 9`。

1. 可以看到`9 5 3 2`是一个递减序列，而`4`打破了这个递减规律，因此需要把`4`换掉。

2. 替换方法就是从`9 5 3 2`里面找到大于`4`的最小数字，也就是`5`。然后和`4`交换，变成`1 5 9 4 3 2`。

3. 此时`9 5 3 2`变成`9 4 3 2`，依旧是递减序列。把它反转过来，变成递增序列，也就是`1 5 2 3 4 9`。

按照上面的三个步骤模拟就可以了。时间复杂度<img src="./assets/formulas/formula-387008096a41.svg" alt="O(n)">。

```c++
class Solution {
public:
    void nextPermutation(vector<int>& nums) {
        int n = nums.size();

        int i = n - 2;
        while(i >= 0 && nums[i] >= nums[i + 1]) i --; // 1. 找到递减序列的边界

        if(i >= 0){
            int j = n - 1;
            while(nums[j] <= nums[i]) j --;
            swap(nums[i], nums[j]);	// 2. 交换
        }// 如果 i < 0，说明整个序列都是递减的，也就是字典序的最后一个序列。到时候全体反转就行了

        reverse(nums.begin() + i + 1, nums.end());	// 3. 反转
    }
};
```




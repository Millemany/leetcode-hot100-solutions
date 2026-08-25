# leetcode 41 缺失的第一个正数

首先明确，如果`nums`的长度是`n`，那么答案一定在`[1, n + 1]`区间内。如果`nums`的元素就是`[1, n]`共`n`个元素，那么答案就是`n + 1`。反之，`nums`一定在`[1, n]`内缺至少一个元素，因此答案一定在`[1, n]`内。

所以只要考虑`[1, n]`的元素在`nums`里的分布情况。我们可以想办法重新规整`nums`。如果`nums[i]`属于`[1, n]`区间，那么就让它移动到`nums[i] - 1`下标的位置去。也就是说如果`nums`里有数字1，就让它移动到0位置。有数字2，就移动到1位置，以此类推。

规整完毕之后，再重新遍历数组。遇到的第一个`nums[i] != i + 1`的位置，就说明元素`i + 1`缺失了。答案就是`i + 1`。如果没有元素缺失，那答案就是`n + 1`。

至于怎么规整`nums`，就判断对于当前的`nums[i]`，需不需要把它送到`nums[i] - 1`位置。如果`nums[i]`不在`[1, n]`内，那就不用管了。如果`nums[i] - 1`位置的值已经是`nums[i]`了，那也不用管了。所以规整`nums`的代码就是：

```c++
for(int i = 0; i < n; i ++)
	while(nums[i] >= 1 && nums[i] <= n && nums[nums[i] - 1] != nums[i]) 
        swap(nums[i], nums[nums[i] - 1]);
```

全部代码如下：

```c++
class Solution {
public:
    int firstMissingPositive(vector<int>& nums) {
        int n = nums.size();
        
        for(int i = 0; i < n; i ++)
            while(nums[i] >= 1 && nums[i] <= n && nums[i] != nums[nums[i] - 1])
                swap(nums[i], nums[nums[i] - 1]);
        
        for(int i = 0; i < n; i ++)
        	if(nums[i] != i + 1) return i + 1;
      	
        return n + 1;
    }
};
```


# leetcode 45 跳跃游戏 II

在 [leetcode 45 跳跃游戏](./leetcode 45 跳跃游戏.md) 的基础上，添加`step`和`ed`两个变量。

`step`表示跳到**下一个**位置需要的最少步数。`ed`表示在`step`数能跳到的最远位置。

初始的时候`step`和`ed`都是`0`，因为还没有跳。

从左到右遍历数组，一旦当前位置`i`与`ed`，表示跳到下一个位置所需的最少步数就要加一。因此就要更新：

```c++
step ++;
ed = d;
```

因为一定能跳到终点，因此最终的`step`就是答案。

时间复杂度是$O(n)$。

```c++
class Solution {
public:
    int jump(vector<int>& nums) {
        int step = 0, ed = 0;
        int d = 0;

        for(int i = 0; i < nums.size() - 1; i ++){
            // i 最远是 nums.size() - 2 就可以了
            // 因为最后一个位置根本不会跳
            d = max(d, i + nums[i]); // 从当前位置跳。d 表示跳到的最远距离

            if(i == ed){	// 如果当前遍历到了 step 步能跳到的最远位置，就更新 step 和 ed
                step ++;
                ed = d;
            }
        }

        return step;
    }
};
```




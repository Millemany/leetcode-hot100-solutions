# leetcode 198 打家劫舍

对于每间房子都有偷和不偷两种抉择。

用`f[i, 0]`表示从第 0 间房屋搜刮到第 i 间房屋，并且不偷第 i 间房屋，能获得的最大财富。

`f[i, 1]`表示从第 0 间房屋搜刮到第 i 间房屋，并且偷了第 i 间房屋，能获得的最大财富。

那么显然有

```c++
f[i, 0] = max(f[i - 1, 0], f[i - 1, 1]);
f[i, 1] = f[i - 1, 0] + nums[i];
```

最后的答案就是

```c++
max(f[n - 1, 0], f[n - 1, 1]);
```

由于每次计算`f[i]`都只用到了`f[i - 1]`的值，所以我们可以不用数组，而只用两个变量维护`f[i - 1]`的值，每次更新即可。

时间复杂度是$O(n)$。

```c++
class Solution {
public:
    int rob(vector<int>& nums) {
        int p = 0, q = 0;	// p 表示 f[i - 1, 0]；q 表示 f[i - 1, 1]
        for(auto x: nums){
            int np = max(p, q);	// np 表示 f[i, 0]
            int nq = p + x;		// nq 表示 f[i, 1]
            p = np, q = nq;
        }
        return max(p, q);
    }
};
```


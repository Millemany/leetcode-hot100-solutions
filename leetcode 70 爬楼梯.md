# leetcode 70 爬楼梯

动态规划。如果`f[n]`表示爬到 n 级台阶的方案数，那就有`f[n] = f[n - 1] + f[n - 2]`。其中`f[0] == f[1] == 1`。

具体操作可以只用两个变量维护`f[i - 1]`和`f[i - 2]`，算出`f[i]`之后再更新`f[i - 1]`和`f[i - 2]`即可。

时间复杂度$O(n)$。

```c++
class Solution {
public:
    int climbStairs(int n) {
        if(n < 2) return 1;

        int a = 1, b = 1;	// a 代表 f[i - 2]， b 代表 f[i - 1]
        for(int i = 2; i <= n; i ++){
            int res = a + b;
            a = b; 
            b = res;
        }
        return b;
    }
};
```


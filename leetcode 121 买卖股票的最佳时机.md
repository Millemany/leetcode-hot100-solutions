# leetcode 121 买卖股票的最佳时机

从后往前遍历每个元素。用一个变量`v`维护某个元素后面的全部元素的最大值，`v - prices[i]`就是在当前位置买入能获得的最大利润。

```c++
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        int n = prices.size();

        int v = prices[n - 1];

        int res = 0;
        for(int i = n - 2; i >= 0; i --){
            v = max(prices[i + 1], v);
            res = max(res, v - prices[i]);
        }

        return res;
    }
};
```


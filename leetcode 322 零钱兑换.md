# leetcode 322 零钱兑换

本题思路参考 [leetcode 279 完全平方数](<./leetcode 279 完全平方数.md>) ，两题都是完全背包问题，思路完全一致。

时间复杂度是<img src="./assets/formulas/formula-84614e269da7.svg" alt="O(mn)">，其中<img src="./assets/formulas/formula-62c66a7a5dd7.svg" alt="m">是钱币种类数，<img src="./assets/formulas/formula-1b16b1df538b.svg" alt="n">是总金额。

```c++
class Solution {
public:
    int coinChange(vector<int>& coins, int amount) {
        int m = coins.size();
        vector<int> f(amount + 1, amount + 1);
        f[0] = 0;

        for(int i = 0; i < m; i ++){
            for(int v = coins[i]; v <= amount; v ++){
                f[v] = min(f[v], f[v - coins[i]] + 1);
            }
        }

        if(f[amount] == amount + 1) return -1; // 最终硬币数大于amount，说明无解
        else return f[amount];
    }
};
```


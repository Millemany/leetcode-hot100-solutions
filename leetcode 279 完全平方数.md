# leetcode 279 完全平方数

这是一个完全背包问题。

本题相当于有一个容积为 n 的背包，以及体积为<img src="./assets/formulas/formula-ea08d341594f.svg" alt="(1^2, 2^2,3^2,\cdots)">的物品，每个物品有无限个。求从这些物品里挑出最少多少件能填满背包。

因为最小的物品体积是 1，所以一定有答案。

用`f[v, i]`表示用前`i`个物品（也就是体积从<img src="./assets/formulas/formula-aa2778de234d.svg" alt="1^2">到<img src="./assets/formulas/formula-fc66c01638c4.svg" alt="i^2">）填满容积为`v`的背包的最少物品数。根据完全背包问题的性质，有
<p align="center"><img src="./assets/formulas/formula-9998ff064e48.svg" alt="f(v, i) = \min(f(v, i - 1), f(v-i^2, i) + 1)"></p>
<img src="./assets/formulas/formula-bafed72f4217.svg" alt="f(v, i - 1)">表示不选用第 i 个物品时候的最小物品数。<img src="./assets/formulas/formula-3a44fa0705fa.svg" alt="f(v-i^2,i) + 1">表示选用第 i 个物品时候的最小物品数，这里使用了递归的表示方法。

时间复杂度是<img src="./assets/formulas/formula-9a6cca306462.svg" alt="O(n\sqrt n)">，因为一共有<img src="./assets/formulas/formula-ccadf00762a5.svg" alt="\sqrt n">个物品。

---

本题可以使用滚动数组优化空间。因为计算<img src="./assets/formulas/formula-12d5cd0fa806.svg" alt="f(\cdot, i)">只会用到<img src="./assets/formulas/formula-5619e4935019.svg" alt="f(\cdot, i-1)">的值，所以用一个长度为<img src="./assets/formulas/formula-60910b501a51.svg" alt="n + 1">的数组，维护截至目前填充各体积所用的最小物品数就可以了。

因此代码结束后，答案就是`f[n]`。

---

下面说一下初始化的问题。初始化<img src="./assets/formulas/formula-4b90967675e9.svg" alt="f(v)">表示用 0 个物品填充容积为<img src="./assets/formulas/formula-4c94485e0c21.svg" alt="v">的背包，最少要多少个物品。因此有<img src="./assets/formulas/formula-29d6ff7d2cec.svg" alt="f(0) = 0">。而当 <img src="./assets/formulas/formula-4c94485e0c21.svg" alt="v"> 不为 0 的时候，是根本不可能实现的，因此<img src="./assets/formulas/formula-4b90967675e9.svg" alt="f(v)">应当是无穷大。

而实际上，我们知道<img src="./assets/formulas/formula-f16aa1455281.svg" alt="f(v,i)">永远不会大于<img src="./assets/formulas/formula-3c7d72ff421b.svg" alt="f(n, 1) = n">，因此把<img src="./assets/formulas/formula-5ba882a3261d.svg" alt="f(v)(v\ne0)">初始化成<img src="./assets/formulas/formula-60910b501a51.svg" alt="n + 1">就可以了。

```c++
class Solution {
public:
    int numSquares(int n) {
        vector<int> f(n + 1, n + 1);
        f[0] = 0;

        for(int i = 1; i * i <= n; i ++){
            int x = i * i;
            for(int v = x; v <= n; v ++){
                f[v] = min(f[v], f[v - x] + 1);
            }
        }

        return f[n];
    }
};
```


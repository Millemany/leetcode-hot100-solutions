# leetcode 62 不同路径

`f[i][j]`表示走到`(i, j)`位置的路径数。所以有`f[i][j] = f[i - 1][j] + f[i][j - 1]`。

可以用滚动数组优化。时间复杂度<img src="./assets/formulas/formula-84614e269da7.svg" alt="O(mn)">。

```c++
class Solution {
public:
    int uniquePaths(int m, int n) {
        vector<int> f(n, 1);

        for(int i = 1; i < m; i ++){
            for(int j = 0; j < n; j ++){
                if(j) f[j] += f[j - 1];
            }
        }

        return f[n - 1];

    }
};
```






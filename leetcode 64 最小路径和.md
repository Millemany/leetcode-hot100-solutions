# leetcode 64 最小路径和

同理 [leetcode 62 不同路径](./leetcode 62 不同路径.md)。时间复杂度$`O(mn)`$。

```c++
class Solution {
public:
    int minPathSum(vector<vector<int>>& grid) {
        int n = grid.size(), m = grid[0].size();

        for(int i = 0; i < n; i ++){
            for(int j = 0; j < m; j ++){
                int a = INT_MAX, b = INT_MAX;
                if(i) a = grid[i - 1][j];
                if(j) b = grid[i][j - 1];
                if(i || j) grid[i][j] += min(a, b);
            }
        }

        return grid[n - 1][m - 1];
    }
};
```


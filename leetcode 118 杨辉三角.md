# leetcode 118 杨辉三角

对于第`i`行第`j`列元素`f[i, j]`，有`f[i, j] = f[i - 1, j - 1] + f[i - 1, j]`。

时间复杂度$`O(n^2)`$，与生成元素数量的数量级相同。

```c++
class Solution {
public:
    vector<vector<int>> generate(int numRows) {
        vector<vector<int>> res;

        for(int i = 0; i < numRows; i ++){
            vector<int> row;
            if(i == 0) row.push_back(1);
            else{
                for(int j = 0; j <= i; j ++){
                    int v = 0;
                    if(j) v += res[i - 1][j - 1];
                    if(j != i) v += res[i - 1][j];
                    row.push_back(v);
                }
            }
            res.push_back(row);
        }
        return res;
    }
};
```


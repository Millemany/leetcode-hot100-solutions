# leetcode 73 矩阵置零

用矩阵的第一行和第一列作为标记数组。

遍历第一遍，如果`matrix[i][j]`为 0$`(i ,j 都不为0)`$，就把`matrix[i][0]`和`matrix[0][j]`置为 0。

而这样做会导致无法分辨出原来第一行和第一列到底有没有 0 ，因此还要先遍历一遍第一行和第一列，用两个变量记录分别是否有 0。

然后遍历第二遍，如果`matrix[i][0] == matrix[0][j] == 0`，则有`matrix[i][] = matrix[][j] = 0`。

最后看第一行（第一列）是否有 0。有的话就要把第一行（第一列）全部置 0。

时间复杂度$`O(mn)`$，空间复杂度$`O(1)`$。

```c++
class Solution {
public:
    void setZeroes(vector<vector<int>>& matrix) {
        bool firstRow = false, firstCol = false;

        int n = matrix.size(), m = matrix[0].size();
        for(int i = 0; i < n; i ++) if(matrix[i][0] == 0) firstCol = true;
        for(int j = 0; j < m; j ++) if(matrix[0][j] == 0) firstRow = true;

        for(int i = 1; i < n; i ++){
            for(int j = 1; j < m; j ++){
                if(matrix[i][j] == 0){
                    matrix[i][0] = matrix[0][j] = 0;
                }
            }
        }

        for(int i = 1; i < n; i ++){
            if(matrix[i][0] == 0){
                for(int j = 1; j < m; j ++) matrix[i][j] = 0;
            }
        }

        for(int j = 1; j < m; j ++){
            if(matrix[0][j] == 0){
                for(int i = 1; i < n; i ++) matrix[i][j] = 0;
            }
        }

        if(firstRow){
            for(int j = 0; j < m; j ++) matrix[0][j] = 0;
        }

        if(firstCol){
            for(int i = 0; i < n; i ++) matrix[i][0] = 0;
        }
    }
};
```

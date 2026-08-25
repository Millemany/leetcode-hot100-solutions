# leetcode 48 旋转图像

找规律可以发现，旋转图像就是把`matrix[i][j]`的元素移动到`matrix[j][n - 1 - i]`，其中`n`是方阵边长。

此外进一步发现，`(i, j)`, `(j, n - 1 - i)`,  `(n - 1 - i, n - 1 - j)`, `(n - 1 - j, i)`四个元素会依次轮换位置。因此按照此规律模拟即可。

只要操作矩阵四分之一的元素即可。具体来说，只操作第`[0, n / 2 - 1]`行的元素，其中对每一行操作第`[i, n - 1 - i]`列的元素。这也是可以研究规律发现的。

```c++
class Solution {
public:
    void rotate(vector<vector<int>>& matrix) {
        int n = matrix.size();

        for(int i = 0; i <= n / 2 - 1; i ++){
            for(int j = i; j < n - i - 1; j ++){
                int tmp = matrix[i][j];

                matrix[i][j] = matrix[n - 1 - j][i];
                matrix[n - 1 - j][i] = matrix[n - 1 - i][n - 1 - j];
                matrix[n - 1 - i][n - 1 - j] = matrix[j][n - 1 - i];
                matrix[j][n - 1 - i] = tmp;
            }
        }
    }
};
```




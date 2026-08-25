# leetcode 74 搜索二维矩阵

两遍二分。

第一遍二分，用每一行的最后一个数查找，确定`target`在哪一行里面（或者任何一行都不可能有）。时间复杂度$O(\log n)$。

第二遍二分，在确定的这一行里面查找。时间复杂度$O(\log m)$。

总共是$O(\log mn)$。

``` c++
class Solution {
public:
    bool searchMatrix(vector<vector<int>>& matrix, int target) {
        int n = matrix.size();
        int l = 0, r = n - 1;
        while(l < r){
            int mid = (l + r) >> 1;
            if(matrix[mid].back() < target) l = mid + 1;
            else r = mid;
        }

        if(target < matrix[r].front() || target > matrix[r].back())
            return false;
        
        int m = matrix[r].size();
        int a = 0, b = m - 1;
        while(a < b){
            int mid = (a + b) >> 1;
            if(matrix[r][mid] < target) a = mid + 1;
            else b = mid;
        }
        
        return matrix[r][b] == target;
    }
};
```


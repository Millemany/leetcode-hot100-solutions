# leetcode 240 搜索二维矩阵 II

1. 暴力搜索。<img src="./assets/formulas/formula-84614e269da7.svg" alt="O(mn)">。

2. 对每一行进行二分查找。时间复杂度<img src="./assets/formulas/formula-14961d3abb17.svg" alt="O(m\log n)">。

   ```c++
   class Solution {
       bool bsearch(const vector<int>& v, int t){
           int l = 0, r = v.size() - 1;
           if(t < v[l] || t > v[r]) return false;
   
           while(l < r){
               int mid = (l + r + 1) >> 1;
   
               if(v[mid] <= t) l = mid;
               else r = mid - 1;
           }
           return v[r] == t;
       }
   public:
       bool searchMatrix(vector<vector<int>>& matrix, int target) {
           int n = matrix.size();
           bool res = false;
   
           for(int i = 0; i < n; i ++) res = res || bsearch(matrix[i], target);
   
           return res;
       }
   };
   ```

3. 可以从右上角`matrix[0][m - 1]`开始查找。这个元素满足其左边的元素都比它小，下面的元素都比它大。

   如果`matrix[0][m - 1] < target`，则第0行全部被排除，开始比较第一行，也就是`matrix[1][m - 1]`。

   如果`matrix[0][m - 1] > target`，则第m - 1列全都被排除，开始比较第m - 2列，也就是`matrix[0][m - 2]`。

   之后以此类推。

   通过这种方法可以一次排除掉一行或者一列。

   如果被比较的元素叫做`matrix[i][j]`，那么`(i, j)`最多往下走`n`步，往左走`m`步。时间复杂度是<img src="./assets/formulas/formula-f51e2807542f.svg" alt="O(m + n)">。

   ```c++
   class Solution {
   public:
       bool searchMatrix(vector<vector<int>>& matrix, int target) {
           int n = matrix.size(), m = matrix[0].size();
   
           int i = 0, j = m - 1;
           while(i < n && j >= 0){
               if(matrix[i][j] == target) return true;
               else if(matrix[i][j] < target) i ++;
               else j --;
           }
           return false;
       }
   };
   ```

   

   

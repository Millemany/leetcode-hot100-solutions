# leetcode 200 岛屿数量

1. dfs。时间复杂度是<img src="./assets/formulas/formula-84614e269da7.svg" alt="O(mn)">。

   ```c++
class Solution {
       void dfs(vector<vector<char>>& v, int x, int y, int n, int m){
        if(x < 0 || x >= n || y < 0 || y >= m) return;
           if(v[x][y] != '1') return;
        v[x][y] = '2';
   
        int dx[] = {-1, 0, 1, 0}, dy[] = {0, 1, 0, -1};
   
           for(int i = 0; i < 4; i ++) 
               dfs(v, x + dx[i], y + dy[i], n, m);
       }
   public:
       int numIslands(vector<vector<char>>& grid) {
           int res = 0;
           int n = grid.size(), m = grid[0].size();
   
           for(int i = 0; i < n; i ++){
               for(int j = 0; j < m; j ++){
                   if(grid[i][j] == '1'){
                       res ++;
                       dfs(grid, i, j, n, m);
                   }
               }
           }
           return res;           
       }
   };
   ```
   
2. bfs。时间复杂度是<img src="./assets/formulas/formula-84614e269da7.svg" alt="O(mn)">。

   ```c++
   class Solution {
       void bfs(vector<vector<char>>& v, int x, int y, int n, int m){
           int dx[] = {-1, 0, 1, 0}, dy[] = {0, 1, 0, -1};
   
           queue<pair<int, int>> q;
           q.push({x, y});
           v[x][y] = '2';
   
           while(q.size()){
               auto t = q.front(); 
               q.pop();
   
               for(int i = 0; i < 4; i ++){
                   int nx = t.first + dx[i], ny = t.second + dy[i];
   
                   if(nx < 0 || nx >= n || ny < 0 || ny >= m) continue;
                   if(v[nx][ny] != '1') continue;
   
                   q.push({nx, ny});
                   v[nx][ny] = '2';
               }
           }
       }
   public:
       int numIslands(vector<vector<char>>& grid) {
           int res = 0;
           int n = grid.size(), m = grid[0].size();
   
           for(int i = 0; i < n; i ++){
               for(int j = 0; j < m; j ++){
                   if(grid[i][j] == '1'){
                       res ++;
                       bfs(grid, i, j, n, m);
                   }
               }
           }
           return res;           
       }
   };
   ```

   

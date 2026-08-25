# leetcode 54 螺旋矩阵

普通模拟。按照“右下左上”的顺序遍历矩阵。如果当前方向走不通，就依此顺序换一个方向。对于遍历过的位置，把它的值改成矩阵取值范围之外的值，用来标记已经访问过了。

时间复杂度$`O(mn)`$。

```c++
class Solution {
public:
    vector<int> spiralOrder(vector<vector<int>>& matrix) {
        vector<int> res;
        int dx[] = {0, 1, 0, -1}, dy[] = {1, 0, -1, 0}; // 右下左上 的下标步进
        int n = matrix.size(), m = matrix[0].size();

        int x = 0, y = 0, cnt = 0;
        int dir = 0; // 当前方向
        while(true){
            res.push_back(matrix[x][y]);
            matrix[x][y] = 114514;
            cnt ++;

            if(cnt == n * m) break;	// 元素遍历完就可以退出了

            int nx = x + dx[dir], ny = y + dy[dir];
            while(nx < 0 || nx >= n || ny < 0 || ny >= m || matrix[nx][ny] == 114514){
                dir = (dir + 1) % 4; // 改变方向
                nx = x + dx[dir], ny = y + dy[dir];
            }

            x = nx, y = ny;
        }
        return res;
    }
};
```


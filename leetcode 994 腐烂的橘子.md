# leetcode 994 腐烂的橘子

多起点的 bfs 题目。把起始的时候所有腐烂橘子的位置都放进队伍里就行了。这就是相当于虚拟原点。

```c++
class Solution {
public:
    int orangesRotting(vector<vector<int>>& grid) {
        queue<pair<int, int>> q;
        int res = -1, cnt = 0;
        int n = grid.size(), m = grid[0].size();

        for(int i = 0; i < n; i ++){
            for(int j = 0; j < m; j ++){
                if(grid[i][j] == 2){
                    q.push({i, j});
                    cnt ++;
                }
            }
        }

        while(q.size()){
            auto t = q.front();
            q.pop();
            cnt --;

            int dx[] = {-1, 0, 1, 0}, dy[] = {0, -1, 0, 1};

            for(int i = 0; i < 4; i ++){
                int nx = t.first + dx[i], ny = t.second + dy[i];
                if(nx < 0 || nx >= n || ny < 0 || ny >= m) continue;
                if(grid[nx][ny] != 1) continue;

                q.push({nx, ny});
                grid[nx][ny] = 2;
            }

            if(cnt == 0){
                res ++;
                cnt = q.size();
            }
        }

        for(int i = 0; i < n; i ++)
            for(int j = 0; j < m; j ++)
                if(grid[i][j] == 1) return -1;	// 还有没烂的橘子，就要返回 -1
		
        // 没有没烂的橘子
        return max(res, 0);	// 如果 res 是 -1，说明开局就没有烂橘子，答案就是 0。
    }
};
```


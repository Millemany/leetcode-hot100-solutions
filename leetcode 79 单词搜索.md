# leetcode 79 单词搜索

暴搜

```c++
class Solution {
    int n, m;
    bool dfs(int u, vector<vector<char>>& b, string word, int x, int y){
        if(b[x][y] != word[u]) return false;
        if(u == word.size() - 1) return true;

        b[x][y] = '$';

        int dx[] = {-1, 0, 1, 0}, dy[] = {0, -1, 0, 1};
        for(int i = 0; i < 4; i ++){
            int nx = x + dx[i], ny = y + dy[i];
            if(nx < 0 || nx >= n || ny < 0 || ny >= m) continue;
            if(b[nx][ny] == '$') continue;
            if(dfs(u + 1, b, word, nx, ny)) return true;
        }
        b[x][y] = word[u];
        return false;
    }
public:
    bool exist(vector<vector<char>>& board, string word) {
        n = board.size(), m = board[0].size();

        for(int i = 0; i < n; i ++)
            for(int j = 0; j < m; j ++)
                if(dfs(0, board, word, i, j)) return true;

        return false;
    }
};
```
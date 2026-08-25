# leetcode 51 N 皇后

对每一行进行暴搜。查看每一行的每一个格点是否可放皇后。

如果这个格点所在的列和两条对角线都没被占过，那就可以放。

```c++
class Solution {
    vector<vector<string>> res;
    vector<string> ans;

    bool col[10], p[18], q[18]; // p 和 q 分别是两条对角线

    void dfs(int u, int n){	// u 是当前遍历的行
        if(u == n){
            res.push_back(ans);
            return;
        }

        for(int j = 0; j < n; j ++){ // j 是当前遍历的列
            if(col[j] == 0 && p[u + j] == 0 && q[n - 1 + u - j] == 0){
                ans[u][j] = 'Q';
                col[j] = p[u + j] = q[n - 1 + u - j] = 1;

                dfs(u + 1, n);

                ans[u][j] = '.';
                col[j] = p[u + j] = q[n - 1 + u - j] = 0;
            }
        }
    }
public:
    vector<vector<string>> solveNQueens(int n) {
        for(int i = 0; i < n; i ++)
            ans.push_back(string(n, '.'));

        dfs(0, n);
        return res;
    }
};
```


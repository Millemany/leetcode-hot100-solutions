# leetcode 1143 最长公共子序列

`f[i][j]`表示`text1`前`i`个字符（`text1[0 ~ i - 1]`）和`text2`前`j`个字符（`text2[0 ~ j - 1]`）最长公共子序列的长度。

显然，`f[i][j] = max(f[i - 1][j], f[i][j - 1])`。

如果`text1[i - 1] == text2[j - 1]`，则还需要考虑`f[i][j] = max(f[i][j], f[i - 1][j - 1] + 1)`。

时间复杂度$`O(mn)`$。

```c++
class Solution {
public:
    int longestCommonSubsequence(string text1, string text2) {
        int n = text1.size(), m = text2.size();
        vector<vector<int>> f(n + 1, vector<int>(m + 1));

        for(int i = 1; i <= n; i ++){
            for(int j = 1; j <= m; j ++){
                f[i][j] = max(f[i - 1][j], f[i][j - 1]);
                if(text1[i - 1] == text2[j - 1]) f[i][j] = max(f[i][j], f[i - 1][j - 1] + 1);
            }
        }
        return f[n][m];
    }
};
```




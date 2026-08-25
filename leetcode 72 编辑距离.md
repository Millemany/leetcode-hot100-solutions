# leetcode 72 编辑距离

用`f[i][j]`表示把`word1`前`i`个字符（也就是下标`0 ~ i - 1`）变成`word2`前`j`个字符的最少操作数。有这么几种方法：

- 把`word1`的最后一个字符删掉，再把`word1.substr(0, i - 1)`变成`word2.substr(0, j)`。

  这种操作的步骤数是`f[i - 1][j] + 1`。

- 把`word2`的最后一个字符删掉，再把`word1.substr(0, i)`变成`word2.substr(0, j - 1)`。

  这种操作的步骤数是`f[i][j - 1] + 1`。

- 若`word1`的最后一个字符与`word2`的最后一个字符不同，就把`word1`的最后一个字符替换成`word2`的最后一个字符，再把`word1.substr(0, i - 1)`变成`word2.substr(0, j - 1)`。

  这种操作的步骤数是`f[i - 1][j - 1] + 1`。

- 若`word1`的最后一个字符与`word2`的最后一个字符相同，直接把`word1.substr(0, i - 1)`变成`word2.substr(0, j - 1)`。

  这种操作的步骤数是`f[i - 1][j - 1]`。

下面说`f`的初始化。

`f[i][0] = i`。此时说明`word1`长度是`i`，`word2`长度是`0`。那么唯一的做法就是把`word1`每个字符都删去，操作数是`i`。

`f[0][i] = i`。道理相同。

时间复杂度是$O(mn)$，`m`和`n`分别是两个字符的长度。

```c++
class Solution {
public:
    int minDistance(string word1, string word2) {
        int n = word1.size(), m = word2.size();

        vector<vector<int>> f(n + 1, vector<int>(m + 1));

        for(int i = 1; i <= n; i ++) f[i][0] = i;
        for(int i = 1; i <= m; i ++) f[0][i] = i;	// 初始化

        for(int i = 1; i <= n; i ++){
            for(int j = 1; j <= m; j ++){
                f[i][j] = min(f[i - 1][j - 1], min(f[i - 1][j], f[i][j - 1])) + 1;
                if(word1[i - 1] == word2[j - 1]) f[i][j] = min(f[i][j], f[i - 1][j - 1]);
            }
        }

        return f[n][m];
    }
};
```


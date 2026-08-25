# leetcode 5 最长回文子串

`f[j][i]`表示字符串`s[j, i]`是不是回文串。

如果`i - j <= 1`，则只要`s[j] == s[i]`就是回文串。

否则，**还**需要满足`f[j + 1][i - 1] == true`。

时间复杂度是$`O(n^2)`$。

```c++
class Solution {
public:
    string longestPalindrome(string s) {
        int n = s.size();
        vector<vector<bool>> f(n, vector<bool>(n));

        int p = 0, l = 0;	// 保存最优结果的左边界和字符串长度

        for(int len = 1; len <= n; len ++){    // 按长度遍历
            for(int j = 0; j + len - 1 < n; j ++){	// 左边界
                int i = j + len - 1;				// 右边界
                if(s[j] == s[i]) f[j][i] = (len <= 2 || f[j + 1][i - 1]);
                if(f[j][i]) p = j, l = len;	// 更新最优结果
            }
        }
  
        return s.substr(p, l);
    }
};
```






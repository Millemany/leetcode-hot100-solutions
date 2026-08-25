# leetcode 139 单词拆分

`f[i]`表示从开头长为`i`的字符串是否可拆分。

具体方法就是从 0 开始遍历到`i - 1`。如果存在`j`，同时满足`f[j] == true`且`s.substr(j, i - j)`在词典表内，那么就有`f[i] = true`。

时间复杂度是$`O(n^2)`$。

```c++
class Solution {
public:
    bool wordBreak(string s, vector<string>& wordDict) {
        int n = s.size();
        vector<bool> f(n + 1, false);
        f[0] = true;

        unordered_set<string> sa;
        for(auto s: wordDict) sa.insert(s);

        for(int i = 1; i <= n; i ++){
            for(int j = 0; j < i; j ++){
                if(f[j]){
                    f[i] = sa.count(s.substr(j, i - j));
                    if(f[i]) break;
                }
            }
        }

        return f[n];
    }
};
```


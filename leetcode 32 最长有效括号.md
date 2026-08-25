# leetcode 32 最长有效括号

`f[i]`表示以`s[i]`结尾的最长有效括号长度。

显然如果`s[i] == '('`，则`f[i] = 0`。

反之若`s[i] == ')'`，则分情况讨论：

- 如果`i == 0`，则`f[i] = 0`。

- 如果`i > 0`且`s[i - 1] == '('`。则有`f[i] = 2 + f[i - 2]`。

- 如果`i > 0`且`s[i - 1] == ')'`。则须考虑`s[i - f[i - 1] - 1]`是否为`(`。

  也就是说需要跳过`i - 1`结尾的最长有效括号，再考虑前一个字符。

  - 如果是的话，则有`f[i] = 2 + f[i - 1] + f[i - f[i - 1] - 1]`。
  - 否则，`f[i] = 0`。

时间复杂度$O(n)$。

```c++
class Solution {
public:
    int longestValidParentheses(string s) {
        int n = s.size();
        vector<int> f(n, 0);

        int res = 0;

        for(int i = 1; i < n; i ++){
            if(s[i] == ')'){
                if(i - 1 >= 0 && s[i - 1] == '('){
                    f[i] = 2;
                    if(i - 2 >= 0) f[i] += f[i - 2];
                }
                else{
                    int pi = i - f[i - 1] - 1;
                    if(pi >= 0 && s[pi] == '('){
                        f[i] = f[i - 1] + 2; 
                        if(pi - 1 >= 0) f[i] += f[pi - 1];
                    } 
                }
            }
            res = max(res, f[i]);
        }
        return res;
    }
};
```


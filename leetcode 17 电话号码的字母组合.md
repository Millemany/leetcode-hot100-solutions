# leetcode 17 电话号码的字母组合

普通的暴搜。

```c++
class Solution {
    string tb[10];
    string ans;
    vector<string> res;

    void dfs(string digits, int u){
        if(u == digits.size()){
            res.push_back(ans);
            return;
        }

        string str = tb[digits[u] - '0'];
        
        if(str.size() == 0) dfs(digits, u + 1);
        for(auto s: str){
            ans.push_back(s);
            dfs(digits, u + 1);
            ans.pop_back();
        }
    }
public:
    vector<string> letterCombinations(string digits) {
        tb[2] = "abc";
        tb[3] = "def";
        tb[4] = "ghi";
        tb[5] = "jkl";
        tb[6] = "mno";
        tb[7] = "pqrs";
        tb[8] = "tuv";
        tb[9] = "wxyz";

        dfs(digits, 0);

        return res;
    }
};
```


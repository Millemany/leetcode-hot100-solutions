# leetcode 131 分割回文串

暴搜。

从起点开始依次遍历子串，如果是回文串就切割，以此类推，一直到结尾。

```c++
class Solution {
    vector<vector<string>> res;
    vector<string> ans;

    bool work(string& s){	// 判断字符串是否回文
        string t = s;
        reverse(t.begin(), t.end());
        return s == t;
    }

    void dfs(string& s, int u){	// 从下标 u 开始暴搜字符串
        if(u == s.size()){
            res.push_back(ans);
            return;
        }

        for(int i = u; i < s.size(); i ++){
            string sub = s.substr(u, i - u + 1);
            if(work(sub)){
                ans.push_back(sub);
                dfs(s, i + 1);
                ans.pop_back();
            }
        }
    }
public:
    vector<vector<string>> partition(string s) {
        dfs(s, 0);
        return res;
    }
};
```




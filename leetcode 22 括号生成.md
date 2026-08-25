# leetcode 22 括号生成

暴搜。

如果当前左括号数量小于$n$，就可以放左括号。

如果当前右括号数量小于左括号，就可以放右括号。

时间复杂度应该是$O(nX)$，其中$X$是答案数。根据数学知识可知时间复杂度是$O(\frac{4^n}{\sqrt n})$。

```c++
class Solution {
    vector<string> res;
    string ans;

    void dfs(int u, int left, int right, int n){ 
        // u 是遍历深度，也是当前放置字符的数量
        // left 和 right 分别是当前已经放置的左括号和右括号的数量
        if(u == n * 2){
            res.push_back(ans);
            return;
        }

        if(left < n){
            ans.push_back('(');
            dfs(u + 1, left + 1, right, n);
            ans.pop_back();
        }

        if(right < left){
            ans.push_back(')');
            dfs(u + 1, left, right + 1, n);
            ans.pop_back();
        }

    }
public:
    vector<string> generateParenthesis(int n) {
        dfs(0, 0, 0, n);
        return res;
    }
};
```


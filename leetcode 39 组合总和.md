# leetcode 39 组合总和

先对当前的元素遍历多个，然后在遍历下一个元素一个到多个，以此类推。

```c++
class Solution {
    vector<vector<int>> res;
    vector<int> ans;

    void dfs(vector<int>& candidates, int u, int target){
        if(target == 0){
            res.push_back(ans);
            return;
        }

        for(int i = u; i < candidates.size(); i ++){
            if(candidates[i] > target) return;

            ans.push_back(candidates[i]);
            dfs(candidates, i, target - candidates[i]);
            ans.pop_back();
        }
    }
public:
    vector<vector<int>> combinationSum(vector<int>& candidates, int target) {
        sort(candidates.begin(), candidates.end());
        dfs(candidates, 0, target);

        return res;
    }
};
```


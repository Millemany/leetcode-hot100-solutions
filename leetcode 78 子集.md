# leetcode 78 子集

对于所有的元素，有选和不选两种选择。

时间复杂度是<img src="./assets/formulas/formula-fc432f7de52c.svg" alt="O(n2^n)">。<img src="./assets/formulas/formula-e8a3fed33f2f.svg" alt="2^n">是子集个数，搜索到每个子集的时间复杂度是<img src="./assets/formulas/formula-387008096a41.svg" alt="O(n)">。

```c++
class Solution {
    vector<int> ans;
    vector<vector<int>> res;

    void dfs(vector<int>& nums, int u){
        if(u == nums.size()){
            res.push_back(ans);
            return;
        }

        dfs(nums, u + 1);	// 不选

        ans.push_back(nums[u]);
        dfs(nums, u + 1);	// 选
        ans.pop_back();
    }
public:
    vector<vector<int>> subsets(vector<int>& nums) {
        dfs(nums, 0);
        return res;
    }
};
```


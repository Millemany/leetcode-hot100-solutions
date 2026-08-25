# leetcode 46 全排列

暴搜。依次枚举当前位置放哪个还未使用的数字，搜索完成后恢复现场。

代码中把已经使用的数字临时改成`1e9`进行标记。题目保证原数组中不会出现这个值。

```c++
class Solution {
    void dfs(vector<int>& nums, vector<int>& ans, vector<vector<int>>& res){
        // ans 长度代表遍历深度
        int n = nums.size();

        if(ans.size() == n){
            res.push_back(ans);
            return;
        }

        for(int i = 0; i < n; i ++){ // 遍历当前在 ans 后面追加什么元素
            if(nums[i] != 1e9){ 
                ans.push_back(nums[i]);

                int tmp = nums[i];
                nums[i] = 1e9;
                dfs(nums, ans, res);
                nums[i] = tmp;
                ans.pop_back();
            }
        }
    }
public:
    vector<vector<int>> permute(vector<int>& nums) {
        vector<int> ans;
        vector<vector<int>> res;
        dfs(nums, ans, res);
        return res;
    }
};
```

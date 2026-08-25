# leetcode 56 合并区间

经典模板题，模拟即可。

```c++
class Solution {
public:
    vector<vector<int>> merge(vector<vector<int>>& intervals) {
        vector<vector<int>> res;
        sort(intervals.begin(), intervals.end());

        int st = -2e9, ed = -2e9;
        for(auto x: intervals){
            if(x[0] > ed){
                if(st != -2e9) res.push_back({st, ed});
                st = x[0], ed = x[1];
            }
            else ed = max(ed, x[1]);
        }
        if(st != -2e9) res.push_back({st, ed});
        return res;
    }
};
```


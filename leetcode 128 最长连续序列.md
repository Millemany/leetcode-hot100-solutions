# leetcode 128 最长连续序列

先把所有数字放进哈希集合。

从**不存在更小值的数字**开始向后枚举，这样每段连续序列只会被统计一次。

时间复杂度$O(n)$，因为每个元素只会被访问一次。空间复杂度$O(n)$。

```c++
class Solution {
public:
    int longestConsecutive(vector<int>& nums) {
        unordered_set<int> sa;
        for(auto x: nums) sa.insert(x);

        int res = 0;
        for(auto x: sa){
            if(sa.count(x - 1)) continue;

            int cnt = 1;
            for(int i = 1; sa.count(x + i); i ++){
                cnt ++;
            }
            res = max(res, cnt);
        }
        return res;
    }
};
```

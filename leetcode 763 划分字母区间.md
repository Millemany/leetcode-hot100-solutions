# leetcode 763 划分字母区间

字符串只由小写字母组成，因此比较好办。

先遍历一遍字符串，找到每个字母出现的最大下标。

再遍历一遍字符串。用变量`ed`维护当前确定子串的右边界，`st`维护开头。显然对于每一个字符，`ed`和**该字符出现最远位置**的最大值就应该是新的右边界。因此就可以不断更新`ed`，直到当前遍历位置`i`与`ed`相同，就可以切割。

时间复杂度是<img src="./assets/formulas/formula-387008096a41.svg" alt="O(n)">。

```c++
class Solution {
public:
    vector<int> partitionLabels(string s) {
        vector<int> pos(26);	// 记录每个字符的最远位置
        vector<int> res;
        
        int n = s.size();
        for(int i = 0; i < n; i ++) pos[s[i] - 'a'] = i;

        for(int i = 0, st = 0, ed = 0; i < n; i ++){
            ed = max(ed, pos[s[i] - 'a']);

            if(i == ed){
                res.push_back(ed - st + 1);
                st = ed + 1;
            }
        }

        return res;
    }
};
```




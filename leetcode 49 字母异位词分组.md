# leetcode 49 字母异位词分组

哈希。

相同字母的异位词，它们排序之后的结果都是相同的。因此可以用排序之后的结果检索。

时间复杂度是$O(nm \log m)$，其中$m$是每个字符串的最大长度。

```c++
class Solution {
public:
    vector<vector<string>> groupAnagrams(vector<string>& strs) {
        unordered_map<string, vector<string>> mp;

        for(auto t: strs){
            auto k = t;
            sort(k.begin(), k.end());
            mp[k].push_back(t);
        }

        vector<vector<string>> res;
        for(auto [k, s]: mp) res.push_back(s);

        return res;
    }
};
```

也可以统计每个字符出现的顺序进行哈希，这样时间复杂度就是$O(nm)$。

```c++
class Solution {
public:
    vector<vector<string>> groupAnagrams(vector<string>& strs) {
        unordered_map<string, vector<string>> mp;

        for(auto t: strs){
            auto k = string(26, 0);
            for(auto c: t) k[c - 'a'] ++;
            mp[k].push_back(t);
        }

        vector<vector<string>> res;
        for(auto [k, s]: mp) res.push_back(s);

        return res;
    }
};
```

因为字符串最大长度是 100，因此我采用一个长为26的字符串统计每个字符出现的个数。比官方题解做法代码好写得多。
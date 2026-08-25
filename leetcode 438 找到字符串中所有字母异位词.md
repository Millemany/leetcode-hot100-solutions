# leetcode 438 找到字符串中所有字母异位词

`s`中所有`p`异位词的子串，必定是和`p`长度相等的子串。因此遍历`s`中与`p`长度相等的子串，判断其是否与`p`异位即可。遍历所有子串，很容易想到维护一个长度与`p`相等的滑动窗口，每次向右移动一格。因此遍历所有与`p`等长子串的时间复杂度是<img src="./assets/formulas/formula-387008096a41.svg" alt="O(n)">。

判断两个长度相等的字符串（仅由小写字母组成）是否异位，一个很好的方法就是统计所有小写字母出现在这两个子串中的次数。当且仅当所有小写字母出现的次数在这两个串中都相等的时候，这两个字符串才是互相异位的。

如果每次都要统计一遍两个串里字母出现数量，那么时间复杂度就是<img src="./assets/formulas/formula-4343234bc647.svg" alt="O(m)">，其中<img src="./assets/formulas/formula-62c66a7a5dd7.svg" alt="m">是`p`的长度。总共时间复杂度是<img src="./assets/formulas/formula-84614e269da7.svg" alt="O(mn)">，可能超时。

而滑动窗口每次向右移动一格，都是移除了最左边的字符，填入了最右边的字符。因此新滑动窗口的各字符数量，就是在上一个窗口的基础上增一减一即可。这样判断异位串的时间复杂度就变成了<img src="./assets/formulas/formula-bc8096326017.svg" alt="O(26)">，不会超时。

```c++
class Solution {
public:
    vector<int> findAnagrams(string s, string p) {
    	vector<int> res;
        int st[26] = {0}, pt[26] = {0};
        
        for(auto x: p) pt[x - 'a'] ++; 
        
        for(int l = 0, r = p.size() - 1; r < s.size(); l++, r ++){
            if(l == 0){
                for(int i = l; i <= r; i ++) st[s[i] - 'a'] ++;
            }
            else{
                st[s[l - 1] - 'a'] --, st[s[r] - 'a'] ++;
            }
            
            bool b = true;
            for(int i = 0; i < 26; i ++) b = b && (st[i] == pt[i]);
            
            if(b) res.push_back(l);
        }
        return res;
    }
};
```




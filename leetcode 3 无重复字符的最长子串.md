# leetcode 3 无重复字符的最长子串

考虑以某元素为开头的字串。比如`abcdefg`。这个字串没有重复字符。

现在接着往后遍历，发现下面一个字符是`d`。也就是现在字串变成了`abcdefgd`。

此时就可以断定，这个`a`开头的最长字串长度是7。并且以`b`,`c`,`d`为开头的最长字串长度分别是6,5,4，一定小于`a`开头的字串长度。所以`b`,`c`,`d`可以直接跳过了，从`e`再开始考虑。

这种思路可以用双指针实现。用`i`维护字串的右边界，在循环中每次加一。`j`维护字串的左边界。一旦遇到了有重复的字符，就开始循环跳过。

```c++
class Solution {
public:
    int lengthOfLongestSubstring(string s) {
        int res = 0;
        unordered_set<int> sa;	// 用来保存当前处理的子串里的字符
        
    	for(int i = 0, j = 0; i < s.size(); i ++){
            // 此时 s[i] 还没有进入到子串中。要先处理好左边界才能把 s[i] 放进去
            while(j < i && sa.count(s[i])) sa.erase(s[j ++]); 
            // 如果当前字串里有 s[i]，就一直移动左边界，直到子串里没有 s[i]
            sa.insert(s[i]);	// 正式把 s[i] 加入到子串
            res = max(res, i - j + 1);
        }
        return res;
    }
};
```




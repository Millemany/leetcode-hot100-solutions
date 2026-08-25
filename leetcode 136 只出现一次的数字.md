# leetcode 136 只出现一次的数字

令答案`res = 0`。对数组中每个元素依次异或即可。相同数字异或就是 0，而任何数字和 0 异或都是它本身。

时间复杂度<img src="./assets/formulas/formula-387008096a41.svg" alt="O(n)">，空间复杂度<img src="./assets/formulas/formula-4a137b861e8d.svg" alt="O(1)">。

```c++
class Solution {
public:
    int singleNumber(vector<int>& nums) {
        int res = 0;
        for(auto t: nums) res = res ^ t;
        return res;
    }
};
```


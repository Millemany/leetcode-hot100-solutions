# leetcode 189 轮转数组

本题有很多种解法，最优解也有很多种。这里给出一种代码最简单，并且非常好理解的。

先翻转整个数组，再分别翻转前$k$个元素和剩余元素，就能把后$k$个元素移动到数组开头。

`k`可能大于数组长度，所以要取模。

时间复杂度$O(n)$，空间复杂度$O(1)$。但是复杂度常数项可能比较大。

```c++
class Solution {
public:
    void rotate(vector<int>& nums, int k) {
        int n = nums.size();

        reverse(nums.begin(), nums.end());
        reverse(nums.begin(), nums.begin() + (k % n));
        reverse(nums.begin() + (k % n), nums.end());
    }
};
```

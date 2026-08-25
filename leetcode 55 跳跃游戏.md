# leetcode 55 跳跃游戏

逐个遍历元素。用一个变量`d`表示从当前遍历过的所有位置能够跳到的最远距离。因此遍历的位置不能超过`d`的范围。如果最后`d`达到或者超过了数据末尾，就说明可以跳到；否则就说明不可以。

时间复杂度是$`O(n)`$。

```c++
class Solution {
public:
    bool canJump(vector<int>& nums) {
        int i = 0, d = 0;
        int n = nums.size();
        
        for(int i = 0; i <= d; i ++){
            d = max(d, i + nums[i]);
            if(d >= n - 1) return true;
        }
		
        return false;
    }
};
```
